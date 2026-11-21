---
title: "Code Is Cheap, Verification Is Hard"
date: 2026-11-05T09:00:00+08:00
draft: false
summary: "Notes from my DevFest Perth 2026 talk on harness engineering: why reliable AI coding agents have less to do with the model and more to do with the verification system wrapped around it."
categories:
  - "Speaking"
event: "DevFest Perth 2026"
location: "Perth, WA"
image: "post1-14.jpg"
imageAlt: "Speaking at DevFest Perth 2026"
imageCaption: "DevFest Perth 2026 // Harness Engineering"
# imageTone: "editorial"
externalUrl: "https://docs.google.com/presentation/d/e/2PACX-1vQeq450yx8odJVZcbXmFpLbROMT9bHzHkfIL8cSc0KCTLdwH9fdE2dAD_CAsijBwnpz9qOgjlsFBk-t/pub"
externalLabel: "View Slides"
---

At DevFest Perth 2026, I talked about building harnesses around AI models to produce reliable, verifiable work in a self-improving loop. An agent can generate thousands of lines of Python or Rust in thirty seconds now, but checking if it actually works still takes most of the afternoon.

I started by asking the room who knew what an AI harness was. Unsurprisingly, only a couple of hands went up. Next I asked who'd been using Opus, Fable, GPT or Gemini to write code, then who'd been using Claude Code, Antigravity, Cursor or Codex. Most of the room was already using a harness without knowing it! Tools like Claude Code and Antigravity are harnesses built by the frontier labs around their models.

## The model matters less than the system around it

In the talk I called this the "two clocks" problem: generating code takes seconds, whilst verifying it still takes hours or days. Replying in chat with "are you sure this is right?" doesn't help, because the model just grades its own guess. A handy way to frame it is hardware: the LLM is a raw CPU and the **harness** is its operating system (instructions, permissions, memory, scripts, hooks, retry caps). Building one comes down to normal software engineering habits, no ML PhD required.

I learnt this auditing 208 of my sessions across [RocketFlag](https://rocketflag.app/?utm_source=codebrew&utm_medium=referral&utm_campaign=news-devfest-perth-2026) (my Go and React SaaS) and a client's clinical Rails app. Compressing around 111 MB of transcripts to 440 KB of friction signals showed almost every broken rule was already in `AGENTS.md` or memory files (including 29 buried in `.claude/`, invisible once I switched to Antigravity). Moving rules from prose into real harness mechanics (with the exact same models underneath) cut follow-up turns from 8.4 to 4.6 and PR close-outs from 7.1 to 3.8.

![JK presenting at DevFest Perth 2026](post1-04.jpg "JK presenting at DevFest Perth 2026")

## The seven dimensions of trust

A single accuracy number doesn't say much about production readiness. In the talk I walked through seven dimensions for evaluating a harness:

**1. Outcome correctness.** Passing unit tests doesn't mean the app works. After 15-plus Rails sessions where tests went green while the UI was broken, we added a handback gate requiring proof in a signed-in Chrome browser (with a screenshot) before closing frontend work.

**2. Process quality.** The path to a fix matters too. One session took 108 turns scattering debug prints instead of checking live server logs, flagging a missing guardrail.

**3. Efficiency.** Raw token spend misses rework, so success-adjusted cost (`C_succ`) is a better guide. A pricier model with a branch-check script and close-out skill costs less than a cheaper one that fails three times.

**4. Reliability.** Single runs can be luck, so `pass^k` (the odds all `k` runs succeed) is a truer test. An 80% rate drops to around 33% over five runs (`0.8^5`), which is why we scripted our rebase, CI polling, and review-bot loop.

**5. Robustness.** Day-to-day prompts are often vague. When I paste a rough Slack bug note asking "is this worth fixing?", our harness routes it to diagnose-only and blocks code edits automatically via a tool hook until I say go.

**6. Safety.** Written rules fade once context gets compressed in long sessions (agents broke our browser rule across 10-plus sessions). Dual-encoding pairs a text rule with hard blocks on commands like `rm -rf`, `DROP TABLE`, or unwanted tools in config.

**7. Fairness.** Average pass rates hide gaps across repos. A harness can handle small TypeScript UI changes reliably while struggling on multi-tenant Rails queries or legacy migrations where linters and characterisation tests are thinner.

![Spider chart visualising the 7 Dimensions of Trust](7-dimensions.png "A slide from the presentation showing the 7 Dimensions of Trust")

## Where to start

This work started after Google put [google-research/harness2](https://github.com/google-research/harness2) up on GitHub a month or so ago. Reading it and the research around it hit close to home in my day to day. Whilst I'd already built skills and so forth for longer tasks, thinking about the whole harness took it much further.

A good starting point is wiring up mechanical sensors first (linters, tests, schema checks, permission gates) and pulling twenty messy log failures into a golden dataset, while keeping humans on specs and acceptance criteria so junior devs still build judgement.

The slides and speaker notes are [here](https://docs.google.com/presentation/d/e/2PACX-1vQeq450yx8odJVZcbXmFpLbROMT9bHzHkfIL8cSc0KCTLdwH9fdE2dAD_CAsijBwnpz9qOgjlsFBk-t/pub). If your team wants AI coding agents working reliably in production, I help teams set this up through [Code Brew Studio](/#contact).

![JK presenting at DevFest Perth 2026](post1-15.jpg "JK presenting at DevFest Perth 2026")