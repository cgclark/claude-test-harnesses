# <Harness name>

> One sentence: what it lets Claude verify on its own, that it otherwise could not.

**Applies to:** <platforms / project types> · **Needs:** <tools, OS versions, hardware>

## Why it exists

What Claude does by default without this harness: what it can't observe, what it leaves the human to
check by hand, or what it doesn't mention. Give the concrete failure that led to building it.

## What it does

The loop in 3–6 steps: input → the thing under test → a capture Claude can read → pass/fail.

## Recipe

Steps another Claude instance can follow in a project it has never seen. Commands go in fenced blocks.
Use placeholders (`<App>`, `<scheme>`, `<device>`), not this Mac's paths.

## Traps

Each trap that cost real time, with its fix. One bullet each.

## What it does not cover

What stays with the human (stage 3: devices, field tests, other people).

## Loading this into Claude

A short paragraph to paste into a project's CLAUDE.md or a skill so the harness becomes that
project's default way of testing.
