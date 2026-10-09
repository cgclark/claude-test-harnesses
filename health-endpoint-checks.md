# Health-endpoint checks

> Lets Claude confirm that each service behind a tunnel and reverse proxy answers at every hop (backend, proxy, public URL), and that the ways around the gate are refused.

**Applies to:** several local services published through one tunnel and one reverse proxy (built for a Caddy proxy behind an ngrok tunnel, fronting a notification relay and a voice-handoff service) · **Needs:** `curl`, the services' health paths, the public hostname

## Why it exists

By default Claude checks one URL, sees a 200 and moves on. It doesn't check which hop answered, and it doesn't check that the routes meant to be closed are closed. Checking each hop takes a minute and locates a failure to backend, proxy or tunnel.

A 200 only proves that something answered on that route. On one system every health endpoint stayed green through six separate faults that kept any push from being sent. For proving that the real path carries traffic, use the an end-to-end check of the whole chain.

## What it does

1. Hit each service's health path at three hops: the backend's own loopback port, the proxy on loopback, the public tunnel URL.
2. Compare. The first hop that differs is the broken one.
3. Check that the bypasses fail: a gated path reached without the edge credential, and a backend port reached from another machine.

## Recipe

```bash
curl -s -o /dev/null -w '%{http_code}\n' http://127.0.0.1:<svc-port>/healthz                 # backend
curl -s -o /dev/null -w '%{http_code}\n' http://127.0.0.1:<proxy-port>/<prefix>/healthz       # proxy
curl -s -o /dev/null -w '%{http_code}\n' https://<tunnel-host>/<prefix>/healthz               # tunnel
```

Bypass checks. Each should fail:

```bash
curl -s -o /dev/null -w '%{http_code}\n' https://<tunnel-host>/<gated-path>                   # expect 403: no edge header
curl -s -o /dev/null -w '%{http_code}\n' -H '<edge-header>: wrong' https://<tunnel-host>/<gated-path>   # expect 403
curl -s -o /dev/null -w '%{http_code}\n' -H '<edge-header>;' https://<tunnel-host>/<gated-path>        # empty value, expect 403
curl -s --max-time 3 http://<machine-lan-address>:<svc-port>/healthz                          # from another machine: expect connection refused
```

Use the header name your proxy actually requires. The tunnel URL bypasses the identity gate in front of it, so the proxy must require a secret only the gate injects. Without that check the gate does nothing.

## Traps

- **A 200 doesn't prove the path.** See above and the chain doctor.
- **"Anything under 500 is up" shows a 401 or 404 as healthy.** A status page probing auth-protected routes this way can't tell "reachable" from "broken but answering". Probe a real health path and expect its exact code and body.
- **A retired route can still answer.** A removed prefix fell through to the root catch-all and returned 403, while the status page and the README still listed the service. Remove the probe and the registry entry in the same change as the route.
- **Check one of each route type.** A package-manager upgrade replaced the proxy's binary under the running process. After that every static-file route returned 403 while reverse-proxy routes kept working, so app sync looked fine and every shared link failed. Restart the proxy after upgrades, and probe a file route as well as a proxied one.
- **A host:port site address breaks the tunnel.** In Caddy, writing the site as `127.0.0.1:<port>` makes the host a matcher, so requests carrying the tunnel's hostname get 400. Keep the site address host-agnostic (`:<port>`) and restrict the socket with `bind 127.0.0.1 ::1`.
- **Bind backends to loopback.** If a backend listens on all interfaces, the LAN can skip the proxy and its checks. The connection-refused check above catches this.
- **Some tunnels serve a browser interstitial** to unknown clients. Scripts may need the provider's skip header. A browser test passing doesn't mean a device client gets through.
- **Keep the checks read-only.** A real submission to some services notifies the user's phone. Health paths only, unless the user agrees.

## What it does not cover

Whether a request that passes health does its job end to end (the chain doctor). Whether the gate's identity login works for the human, which they confirm in their own browser.

## Loading this into Claude

> After any change to `<proxy config>` or a service behind it, curl each service's health path at the backend, the proxy and `https://<tunnel-host>`, and report the code at each hop. Then confirm the bypasses fail: gated paths on the raw tunnel with no or wrong edge header return 403, and backend ports refuse connections from the LAN. Never call a 200 proof that the service works. Use the chain doctor for that.
