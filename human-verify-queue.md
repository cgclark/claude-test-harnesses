# Human-only verify queue

> Lets Claude keep working when a check needs a person, a device or a headset: it writes the check down in one file, with the exact steps and what a pass looks like, and moves on, so the person can clear several checks in one sitting.

**Applies to:** any project where some checks need hardware, a real account or a person's judgement (devices, headsets, controllers, ray-tracing GPUs, Siri, field tests) · **Needs:** a Markdown file in the repo and a rule in the project's `CLAUDE.md`

## Why it exists

By default, when Claude reaches something it can't check, it stops and asks in the thread: "can you run it
on the Mac and tell me?" Then it waits. Each ask costs the person a context switch, and each answer comes
back without the details Claude needed. Or Claude reports the work as done when it only compiled.

Built for the Quake 3 port, where the ray-tracing page needs a hardware ray-tracing Mac, spatial taps need a
Vision Pro, and controller checks need a pad in hand. A voice project (Circus) uses the same idea inline,
tagging steps in its module list.

## What it does

1. Claude finishes everything it can verify itself (build, simulator, captures, logs).
2. Whatever is left goes into `VERIFY-QUEUE.md` under the hardware it needs: what to do, what a pass looks
   like, what to look at if it fails, and what it unblocks.
3. Claude carries on with work that doesn't depend on it. Nothing becomes a question in the thread.
4. The person works through the queue in one pass and reports results; Claude deletes passed entries and
   turns failures into work items.
5. Until its entry comes back, a queued item is reported as **done, unverified**.

## Recipe

**1. The file.** Group entries by what they need, not by date:

```markdown
# Verify queue — needs hardware only a person has

Each entry: what to do, what PASS looks like, what it unblocks. Delete an entry when it passes;
move it to OPEN-ITEMS.md if it fails.

## On the Mac build
## On the headset
## With a controller
## On a phone
```

**2. An entry.** Write it so someone who hasn't read the thread can do it in two minutes:

```markdown
- [ ] **Mouse stays captured in a match** (built <commit>, not seen). Needs a build from <commit> or later.
  1. Start a match, click into the window, move the mouse well past the screen edge; open and close the menu.
  **PASS:** no cursor over the game; looking never stops at an edge; in the menu the cursor is free again.
  **If it fails:** the log line "mouse: captured …" says why; `log show --last 5m --predicate '<predicate>'`.
  **Already checked here:** compiles on all targets; the log line appears in the simulator.
  **Unblocks:** <roadmap item>.
```

Name the minimum build. A check run on an older build reads as a failure ("a build from before X shows a
smaller model"). Say what the simulator already proved, so the person only does the part it can't.

**3. The rule in `CLAUDE.md`:**

```markdown
## Not blocking on the person
Anything needing hardware only the person has goes to VERIFY-QUEUE.md with exact steps and a PASS line.
It does not become a question in the thread. Never report a queued item as done: it is
"done, unverified" until its entry comes back.
```

**4. Inline tags, for a step list.** Circus's module list marks the steps an autonomous run can't finish
alone, each with a "Done when":

```markdown
- [Device] Action button opens the mode and starts listening. *Done when:* works 9 of 10 tries.
- [Person] Pick the entry paths to keep. *Done when:* decision written in this file.
```

An autonomous run does everything around these steps, leaves them listed, and moves to the next step.
`[Device]` is hardware, `[Person]` is a decision or an action only the person can take. Gather them into a
queue when a session ends.

## Traps

- **The queue stops being short.** The file said "short, current, and cleared as it is worked", and grew to
  about 1,600 lines, mostly RESOLVED and DONE sections that were never deleted, around 20 open items. A
  person can't do a pass over that. Delete an entry the moment it passes; history belongs in git and the
  changelog.
- **Don't queue what the simulator can check.** One entry was marked "verified in the iPad simulator" and
  still sat in the queue. Only checks that genuinely need the hardware go in.
- **Vague pass lines come back as "looks fine".** "Check the banner" can't fail. "Same or different from
  the reference, and if different: colour, motion or geometry" can.
- **Put blocking questions first.** When one queued fact blocks several entries (do the touch
  controls appear on a device at all?), put it first and mark the entries it blocks.
- **A superseded entry stays and misleads.** Writing "SUPERSEDES the entry above" left both in place. Replace
  the old entry instead.
- **Address the hardware, not a name.** Entries headed with the person's name don't travel to another project
  or another person. Use the device or role.

## What it does not cover

The checks themselves. The queue is where hardware checks, field tests, comfort in a headset, real accounts,
Siri by voice and judgement calls wait; someone still has to do them. It doesn't schedule anything, and it
doesn't replace building a harness when the same check keeps coming back. A check that comes back often is
worth a harness.

## Loading this into Claude

> Don't ask me to check things one at a time. Anything you can't verify yourself (it needs `<devices>`, a
> controller, a headset, or my decision) goes into `VERIFY-QUEUE.md` under the hardware it needs: exact
> steps, the minimum build, a PASS line that can fail, what you already checked, what it unblocks. Then keep
> working. Report those items as "done, unverified". When I report results, delete passed entries and turn
> failures into work items. In step lists, tag `[Device]` and `[Person]` steps, finish everything around them,
> and list them at the end.
