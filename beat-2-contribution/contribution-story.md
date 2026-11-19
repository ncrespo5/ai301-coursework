# Contribution: Expand and collapse all packet categories

**Contribution Number:** [1]
**Student:** Nyla Crespo
**GitHub Username:** ncrespo5
**Issue:** https://github.com/WorldconVotingSystems/nomnom/issues/358
**Pull Request:** https://github.com/WorldconVotingSystems/nomnom/pull/536

---

## Toolkit

**Unit 9: Issue-scout setup and ownership checks**

November 18, 2026. The issue-scout setup carries forward the issue-selection rubric and adds searches for small Python parser and CLI work. An exploratory GitHub scan surfaced issues with no listed assignee, but their threads showed existing claims or a competing pull request. The revised search strategy prioritizes zero-comment results, and the rubric still checks the thread and open pull requests before an issue is selected. When the project shifted to frontend work, CodePath’s saved HTML/UI issue list supplied the candidates. The direct rubric review checked NomNom #358 against the issue timeline and open pull requests.

**Unit 10: Repro-check and voice guide**

November 18, 2026. In the PathReview sandbox, the repro-check and voice guide helped prepare the claim and reproduction comments for #55. The first evaluation matched 17 of 20 cases. The rubric was revised to accept a bounded cannot-reproduce report when it tested the same operation, captured observable output, and named the trigger it did not reach. The revised run matched 20 of 20. [Reproduction and eval notes](../beat-1-sandbox/unit-2/reproduction.md)

**Unit 11: Plan-check and implementation evidence**

November 18, 2026. The PathReview plan-check matched 18 of 20 evaluation cases. One clear plan was rejected because it stated a possible cause too confidently, which showed the value of pairing an explicitly labeled hypothesis with a trace step. The final live plan passed all seven checks after the deviations were documented, and the posted plan and branch both point back to the five failing fixtures. [Plan and branch evidence](../beat-1-sandbox/unit-3/plan-and-implement.md)

**Unit 12: PR precheck and draft revision**

November 18, 2026. The first live precheck of the PathReview #55 PR draft flagged a change to existing database display labels. The patch restored those labels and added a PostgreSQL assertion covering both the exact label and deduplication. The revised draft passed all five required checks and was used for PathReview PR #98. [PR and precheck evidence](../beat-1-sandbox/unit-4/pull-request.md)

---

## Why I Chose This Issue

**Claim:** https://github.com/WorldconVotingSystems/nomnom/issues/358#issuecomment-6997163269

NomNom #358 appeared in CodePath’s saved HTML/UI issue list. It proposes two controls on one existing page. At selection time the issue was open and unassigned, with no prior comments, no linked PR in its timeline, and no matching open PR in the repository. The repository is active and its developer guide describes a pull-request contribution workflow.

I chose NomNom #358 because it was a focused frontend change I could test in the browser. I liked that the improvement was easy to see. If someone wants to browse several categories, they can open them together instead of clicking through each one.

**Toolkit**

- Tool: Issue-selection rubric, CodePath’s issue selector, and GitHub issue and PR searches.
- What it produced: A shortlist and a manual decision to proceed with #358 after checking scope, ownership, and competing PRs.
- Difficulties: Some issues with no assignee already had a claim or competing work in their threads.
- What changed: Opened the issue discussion and checked PRs before treating an issue as available.

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

- Tool: Codex-assisted inspection of the GitHub issue and NomNom’s Django templates.
- What it produced: Traced the existing category button to its Bootstrap collapse target and the events that update its label.
- Difficulties: A top-level section without children looks like a category in the data but renders as a flat section.
- What changed: Used the actual finalist collapse containers to define which sections the bulk controls should affect.

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

- Tool: Django admin, Docker Compose, browser inspection, and Codex-assisted setup troubleshooting.
- What it produced: A working local baseline with two categories, individual toggles, and no bulk controls.
- Difficulties: The checkout path contained a space, the Docker CLI helper was missing from PATH, and the admin lacked a member profile.
- What changed: Ran the environment helper directly, corrected PATH, added the profile, and created two local categories with child sections.

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

- Tool: Codex-assisted review of the packet template and Bootstrap behavior.
- What it produced: A plan to call Bootstrap’s show and hide methods on the existing collapse instances.
- Difficulties: Always-visible packet downloads and unrelated collapsible elements had to retain their behavior.
- What changed: Scoped the bulk actions to finalist containers and kept the existing per-category event listeners.

---

## Testing Strategy

At baseline `22d531f`, source inspection found a collapse button per category and no page-level controls. A local Node and jsdom fixture loaded the changed template’s actual script and Bootstrap 5.3.3. With two categories, it verified **Expand All** from a mixed state, **Collapse All**, individual toggles, and synchronization of button labels and `aria-expanded`. An unrelated collapse stayed open, and the bulk controls stayed hidden when categories or Bootstrap were absent. The fix was also checked on the page rendered by the local Django app, using the Bootstrap bundle served by that app. The browser check confirmed that both finalists appeared with **Expand All** and hid with **Collapse All**. The full repository test suite has not been run.

**Toolkit**

- Tool: Node, jsdom, Bootstrap, and the local Django app in the browser.
- What it produced: Passing checks for mixed category state, both bulk buttons, individual toggles, labels, and aria-expanded.
- Difficulties: The original fixture had no collapsible categories, and a synthetic test alone could not confirm what Django rendered.
- What changed: Added test categories and repeated the checks against Django-rendered HTML and the Bootstrap bundle served by the app.

---

## Implementation Notes

**November 18, 2026**

Claimed NomNom #358 in its GitHub thread. The local branch `fix/358-packet-category-controls` contains the one-template change in commit `507fdd3`. The fixture confirmed that each category’s existing Bootstrap events still update its individual button. The tested template was published to the fork in commit [`b0cb8e6`](https://github.com/ncrespo5/nomnom/commit/b0cb8e68deb582bd3923381265ee4591e0a943c5). The PR targets NomNom’s `main` branch.

Local verification hit three setup blockers. The bootstrap script split the checkout path at a space, Docker Compose could not find the installed credential helper on `PATH`, and the packet view required a member profile for the local admin. Running the environment helper directly, adding Docker’s CLI directory to `PATH`, and creating the local profile let the app render the packet. Two test categories then made it possible to compare the original and updated page.

**Toolkit**

- Tool: Git and Codex-assisted template editing.
- What it produced: A one-template change on a feature branch, with the tested file verified on the fork.
- Difficulties: The checkout used for the local demo was still running the original template.
- What changed: Started a separate local preview for the changed template so the same packet data could be compared before and after.

---

## Pull Request

**PR Link:** https://github.com/WorldconVotingSystems/nomnom/pull/536

**PR Description:** The PR adds **Expand All** and **Collapse All** to the packet page and keeps the individual category buttons in sync. It links issue #358 and records the local Django browser check and automated checks.

**Maintainer Feedback:**

- November 18, 2026: None yet.

**Status:** Awaiting review.

**AI-use disclosure:** I used OpenAI Codex to help evaluate the issue, investigate the local setup errors, implement the packet controls, run automated checks, and draft the PR description. I verified both buttons in the running app and opened the PR on GitHub.

**Toolkit**

- Tool: GitHub’s compare page and a Codex-assisted PR draft.
- What it produced: An open upstream PR linked to #358, with manual and automated test evidence in the description.
- Difficulties: The connected GitHub integration could publish the branch to the fork but lacked permission to open the upstream PR.
- What changed: I opened PR #536 through GitHub’s compare page.

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
