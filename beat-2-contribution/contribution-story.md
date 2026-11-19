# Contribution: Expand and collapse all packet categories

**Contribution Number:** [1]
**Student:** Nyla Crespo
**GitHub Username:** ncrespo5
**Issue:** https://github.com/WorldconVotingSystems/nomnom/issues/358
**Pull Request:** https://github.com/WorldconVotingSystems/nomnom/pull/536

---

## Toolkit

**Unit 5: Issue-scout setup and ownership checks**

November 18, 2026. The issue-scout setup carries forward the issue-selection rubric and adds searches for small Python parser and CLI work. An exploratory GitHub scan surfaced issues with no listed assignee, but their threads showed existing claims or a competing pull request. The revised search strategy prioritizes zero-comment results, and the rubric still checks the thread and open pull requests before an issue is selected. When the project shifted to frontend work, CodePath’s saved HTML/UI issue list supplied the candidates. The direct rubric review checked NomNom #358 against the issue timeline and open pull requests.

**Unit 6: [one line on the tool work]**

[2-4 sentences: the voice-guard, the repo-memory file. What broke or
fell short, and what changed because of it. "Nothing broke" counts when
it is true - say how you know.]

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

**Claim:** https://github.com/WorldconVotingSystems/nomnom/issues/358#issuecomment-6997163269

NomNom #358 appeared in CodePath’s saved HTML/UI issue list. It proposes two controls on one existing page. At selection time the issue was open and unassigned, with no prior comments, no linked PR in its timeline, and no matching open PR in the repository. The repository is active and its developer guide describes a pull-request contribution workflow.

**Toolkit**

- Tool: issue-scout (your scout: your search strategy, your rubric),
  and how you used it
- What it produced: [the scan and its verdict on this issue, described]
- Difficulties: [where it fell short, or "none met" if none did]
- What changed: [what you patched or would update, or "nothing"]

---

## Understanding the Issue

**Problem Description**

Packet downloads are grouped by award category. Viewing the finalist downloads across multiple categories requires opening each category individually.

**Expected Behavior**

Page-level **Expand All** and **Collapse All** buttons should open or close all finalist download groups together. Individual category buttons should continue to work.

**Current Behavior**

The packet template loops through the categories. A category with finalist subsections gets its own Bootstrap collapse control. The page has no control for opening or closing all of those groups.

**Affected Components**

`src/nomnom/hugopacket/templates/hugopacket/index.html` renders the page and responds to Bootstrap collapse events. `src/nomnom/hugopacket/templates/hugopacket/bits/section.html` renders each category button and its collapsible finalist group.

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

Source baseline inspected on macOS arm64 at [upstream commit `22d531f`](https://github.com/WorldconVotingSystems/nomnom/commit/22d531f04da7748ac0daee7f5d7d8e59981d1f77). The [developer setup](https://github.com/WorldconVotingSystems/nomnom/blob/main/docs/docs/dev/bootstrap.md) uses Python 3.13, `uv`, `just`, and Docker Compose. The development server ran on port 8000. The local Yugo Awards election was set to Voting Preview, and the seeded admin account was given a local member profile so the packet page would load.

**Steps to Reproduce**

1. Run `just bootstrap` and `just serve` with Docker Desktop running. In Django admin, set the seeded Yugo Awards election to **Voting Preview** and give the local admin account a member profile.
2. Add two top-level packet sections, each with one child section representing a finalist. Open `/p/yugo-awards/` while signed in.
3. Use one category’s **Show all downloads** button. That category opens while the other stays closed. On the baseline, the top of the page has no controls to open or close both groups together.

**Reproduction Evidence**

- **Commit showing reproduction:** [Fork baseline `22d531f`](https://github.com/ncrespo5/nomnom/commit/22d531f04da7748ac0daee7f5d7d8e59981d1f77).
- **Screenshots/logs:** The local baseline packet returned HTTP 200 with Test Category A and Test Category B, each with one sample finalist. The rendered page had individual category buttons and no bulk controls.
- **My findings:** The bulk controls can use the same Bootstrap collapse groups as the individual buttons.

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

The packet page renders one Bootstrap collapse group per category with finalist downloads. Each category has an associated button, and the page’s `shown.bs.collapse` and `hidden.bs.collapse` handlers update that button’s text and styling. The page had no way to show or hide all of those groups together.

**Proposed Solution**

Add two packet-level buttons that use Bootstrap’s existing collapse instances. Target finalist groups and preserve individual category toggles and always-visible packet downloads.

**Implementation Plan**

1. Add **Expand All** and **Collapse All** above the categories in the packet index template.
2. Call Bootstrap’s `show()` and `hide()` methods on finalist groups. Show the controls only when at least one group and Bootstrap are available.
3. Verify the controls with two sample categories and check the existing category labels and ARIA state.

The implementation stayed within the packet index template. The test setup expanded to include two local categories with one finalist each because the default fixture had only a flat section. The buttons remain hidden until the page finds both a collapsible category and Bootstrap.

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

At baseline `22d531f`, source inspection found a collapse button per category and no page-level controls. A local Node and jsdom fixture loaded the changed template’s actual script and Bootstrap 5.3.3. With two categories, it verified **Expand All** from a mixed state, **Collapse All**, individual toggles, and synchronization of button labels and `aria-expanded`. An unrelated collapse stayed open, and the bulk controls stayed hidden when categories or Bootstrap were absent. The fix was also checked on the page rendered by the local Django app, using the Bootstrap bundle served by that app. The browser check confirmed that both finalists appeared with **Expand All** and hid with **Collapse All**. The full repository test suite has not been run.

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

**November 18, 2026**

Claimed NomNom #358 in its GitHub thread. The local branch `fix/358-packet-category-controls` contains the one-template change in commit `507fdd3`. The fixture confirmed that each category’s existing Bootstrap events still update its individual button. The tested template was published to the fork in commit [`b0cb8e6`](https://github.com/ncrespo5/nomnom/commit/b0cb8e68deb582bd3923381265ee4591e0a943c5). The PR targets NomNom’s `main` branch.

Local verification hit three setup blockers. The bootstrap script split the checkout path at a space, Docker Compose could not find the installed credential helper on `PATH`, and the packet view required a member profile for the local admin. Running the environment helper directly, adding Docker’s CLI directory to `PATH`, and creating the local profile let the app render the packet. Two test categories then made it possible to compare the original and updated page.

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** https://github.com/WorldconVotingSystems/nomnom/pull/536

**PR Description:** The PR adds **Expand All** and **Collapse All** to the packet page and keeps the individual category buttons in sync. It links issue #358 and records the local Django browser check and automated checks.

**Maintainer Feedback:**

- November 18, 2026: None yet.

**Status:** Awaiting review.

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

I learned how Bootstrap’s collapse events keep the individual buttons in sync, including their labels and `aria-expanded` state.

**Challenges Overcome**

The hardest part was getting a local packet that actually exercised the feature. The default sample section had no nested categories.

**What I'd Do Differently Next Time**

Next time, I’d check the seeded data and account permissions before spending time debugging the page.

---

## Resources Used

- [NomNom #358](https://github.com/WorldconVotingSystems/nomnom/issues/358) describes the requested packet behavior.
- [NomNom developer setup](https://github.com/WorldconVotingSystems/nomnom/blob/main/docs/docs/dev/bootstrap.md) documents bootstrapping, seeded data, and the local server.
- [NomNom packet section template at the baseline](https://github.com/WorldconVotingSystems/nomnom/blob/22d531f04da7748ac0daee7f5d7d8e59981d1f77/src/nomnom/hugopacket/templates/hugopacket/bits/section.html) shows the individual category control and its collapse target.
