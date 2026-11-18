# Voice guide: how I talk upstream

## Who I am in threads

I’m a computer science student contributing to PathReview through CodePath. I like to understand what’s causing a bug before deciding how to fix it. In an issue thread, I want people to know what I tried, what happened, and what I’m checking next.

## Rules I write by

### Rule: Say what I’m taking on.

Name the issue and the first thing I’ll investigate.

- Wrong: "I’ll fix the parser."
- Right: "I’d like to work on #55. I’ll start with the five SkillExtractor cases that fail on the original code."

### Rule: Give the result and the setup.

Include enough detail for someone else to check my result.

- Wrong: "I reproduced it. The tests failed.”
- Right: “On macOS arm64 with Python 3.12.1, the original SkillExtractor suite reported 13 passes and 5 expected failures.”

### Rule: Label a hunch as a hunch.

Say what I suspect and how I’ll check it.

- Wrong: “The regex is definitely the reason TypeScript is missing.”
- Right: “The exported interface case fails. I suspect the detector is missing that declaration pattern, so I’ll trace which signals it checks.”

### Rule: Commit to the next step.

Give a concrete action I can follow through on.

- Wrong: “I’ll have the whole fix ready tonight.”
- Right: "I’ll verify the change against the five failing cases and share the results.”

## Things I never post

- A deadline I haven’t scoped.
- “All tests pass” when I ran only the focused test file.
- A guess about the cause stated as a confirmed finding.
- A reproduction claim without the command I ran or the result I saw.
