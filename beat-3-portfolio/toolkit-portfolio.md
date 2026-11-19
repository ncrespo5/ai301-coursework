# Toolkit Portfolio

**Student:** Nyla Crespo

## Featured Tools

I chose issue-scout, repro-check, and PR precheck because each one helped at a different point in the contribution. Issue-scout helped narrow down what was worth working on. Repro-check helped me show what was actually happening, and PR precheck caught a change I wanted to fix before someone reviewed the PR. Together, they show how I went from choosing an issue to giving a reviewer evidence they could check.

**issue-scout**

**What it is, and the judgment hole I wrote:** Issue-scout evaluates whether an issue is a reasonable first contribution. The rubric checks whether the repo is open to contributions, whether the change is small enough to verify, and whether someone else is already working on it. An empty assignee field is only one clue. I also check the thread and pull requests for signs that someone has claimed the work.

**How it evolved, dated:** On November 17, 2026, the first evaluation matched 14 of 20 cases. The rubric treated recent activity as a preference, so it accepted a bounded issue in a repo with old activity and no maintainer response in the sampled threads. The revision made prolonged inactivity a reason to reject only when the available dates and the thread evidence both pointed to it. On November 18, I used CodePath’s issue list to find NomNom #358 and checked the issue thread and open PRs before claiming it.

**Evidence:** The evaluation improved from `14/20` to `18/20`. In `issue-02`, the verdict changed from `accept` to `reject`, matching the expected result. The scout also returned `accept` for PathReview #55 after finding a bounded change and no visible competing PR. The NomNom ownership check was manual. [Issue selection and evaluation](../beat-1-sandbox/unit-1/selection.md) · [NomNom claim](https://github.com/WorldconVotingSystems/nomnom/issues/358#issuecomment-6997163269)

**repro-check**

**What it is, and the judgment hole I wrote:** Repro-check evaluates whether a reproduction comment gives someone enough evidence to understand and repeat the attempt. The rubric asks for the environment, the operation, and observable output. If an attempt cannot reproduce the issue, it can still be useful when it tests the same operation and names the condition it did not reach.

**How it evolved, dated:** On November 18, 2026, the first run matched 17 of 20 cases. One report was rejected because it could not establish which command reached the size limit first. The report did have output from the relevant batch operation and named the missing trigger. The revised rule let that narrower, evidence-backed result pass while still requiring a positive reproduction to show the reported failure.

**Evidence:** The revised evaluation matched `20/20`. In the live PathReview #55 reproduction, the original suite reported `13 passed, 5 xfailed`. Running the same cases with `--runxfail` exposed the assertions and reported `5 failed, 13 passed`. I posted the command, environment, and failing case names so someone else could repeat the run. [Reproduction and evaluation](../beat-1-sandbox/unit-2/reproduction.md) · [Posted evidence](https://github.com/codepath/pathreview-ai301-fa26-howard/issues/55#issuecomment-6975445963)

**pr-precheck**

**What it is, and the judgment hole I wrote:** PR precheck evaluates whether the diff follows the plan, whether the tests exercise the original problem, and whether the PR is ready for review under the repo’s standards. The reproduction-proof rule asks for a before result and a concrete after result for the same trigger. A passing test for a different case cannot establish that the reported bug was fixed.

**How it evolved, dated:** On November 18, 2026, the recorded evaluation matched 20 of 20 cases. The live check of PathReview #55 exposed a problem the score alone could not show. It rejected the first draft because the patch changed existing database display labels. I kept the existing labels and strengthened the PostgreSQL fixture to check the exact label and confirm that a direct reference plus an alias produces one result. The live feedback changed the patch and its tests.

**Evidence:** The live verdict changed from `reject` to `accept`, with all five required checks passing in the revised draft. Its reproduction check compared `5 failed, 13 passed` before with `18 passed` after using the same `--runxfail` run. [Precheck output and evaluation](../beat-1-sandbox/unit-4/pull-request.md) · [PathReview PR #98](https://github.com/codepath/pathreview-ai301-fa26-howard/pull/98)

## Inventory

- **plan-check** checks whether a proposed fix follows the reproduction, stays in scope, identifies unknowns, and has a test plan. It matched 18 of 20 evaluation cases. The final live plan for PathReview #55 passed all seven required checks. [Plan and evaluation](../beat-1-sandbox/unit-3/plan-and-implement.md)

## The Arc

**Beat 1**\
Date: November 17, 2026\
Friction: Issue-scout accepted a small issue in a repo whose activity and maintainer responses were both stale.\
Change: Made prolonged inactivity a required check when both the repo history and the thread evidence support it.\
Result: Agreement rose from 14/20 to 18/20, and the inactive-repo case changed to the expected rejection.

**Beat 2**\
Date: November 18, 2026\
Friction: Repro-check rejected a report with useful output because the reporter could not confirm the exact trigger.\
Change: Allowed a bounded cannot-reproduce report when it shows the same operation, records the result, and names the untested condition.\
Result: The revised rubric accepted that report and agreement rose from 17/20 to 20/20.

**Beat 3**\
Date: November 18, 2026\
Friction: Plan-check rejected a viable sample plan because it treated a hypothesis about the cause as an established fact.\
Change: For the live PathReview plan, kept the suspected cause explicit and included a step to trace each failing fixture before changing the detector.\
Result: The posted live plan passed all seven required checks, and the focused parser suite passed all 18 tests after the patch.

**Beat 4**\
Date: November 18, 2026\
Friction: PR precheck caught a display-label regression outside the intended parser fix.\
Change: Preserved the existing labels and added a test for the exact PostgreSQL label and deduplication.\
Result: The revised draft passed all five checks and became PathReview PR #98.

## Limitations and What's Next

These tools depend on the evidence they receive. A clear reproduction comment can still miss the original environment, and a passing precheck only covers the code and output it reviewed. I would add a final check that ties each before-and-after result to the commit and command that produced it. I would also test the issue-scout rubric on a few quiet repos that still accept contributions to see how often the inactivity rule rules them out.

**Tool limits.**\
issue-scout: An inactive-looking repo may still welcome a patch. A teammate may also have claimed an issue in a thread or PR that the initial search missed.\
repro-check: A well-documented cannot-reproduce attempt leaves the original trigger unresolved until someone can recreate it.\
pr-precheck: A passing local review cannot tell me how hosted CI or maintainers will respond once the PR is opened.
