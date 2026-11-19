# Contribution: Keyword search raises `ZeroDivisionError` when the index is empty

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** youlinaxu-en
**GitHub Username:** youlinaxu-en
**Issue:** https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68
**Pull Request:** https://github.com/codepath/pathreview-ai301-fa26-s3/pull/261

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.


**Unit 5: Built issue-scout's search strategy and fixed its blind spot to issues that already have a PR**

I wrote a fit profile and a search strategy for issue-scout (three `gh search issues` queries for Python good-first-issues, ranking filters, top 5 graded). My first scan graded 5 issues and accepted only one; three were rejected because another contributor's open PR already said "Closes #N", which my `--no-assignee` queries could not see since PRs never set an assignee. I added `-linked:pr` to every query (checked that a known PR-linked issue dropped out) and a one-issue-per-repo rule, because one repo had taken two of the five graded slots. I left the rubric unchanged because each reject cited a real PR or scope trigger. I also graded one issue I picked by hand, ArduPilot #14438; it was rejected for a two-day-old claim comment and an earlier closed PR, so I did not take it.


**Unit 6: Installed the voice guard with my upstream rules, wrote a repo-memory file, and patched my scout's scope check**

I appended an Upstream section to my voice guide (claims, questions, pings, each with a wrong/right pair), installed the guard as a hook, and wrote `CLAUDE.local.md` for the Path Review clone. The guard did not fire at first for two reasons that are specific to my Windows setup: its script only accepted the Bash tool while Claude Code runs my commands through PowerShell, and my PowerShell-written settings file had a byte-order mark that Python could not parse. I added PowerShell to the script and the hook matcher and rewrote the files without the mark; the wiring test then stopped `gh issue comment --help` as intended and a manual check of a claim draft passed. I also replaced my `scope-bounded` check with the staff `scope-feasible` row and difficulty notes.

**Unit 7: Installed the ship-gate and wrote a manifest of the three checks Path Review asks for**

My ship-manifest lists unit tests, ruff and mypy from CONTRIBUTING.md and the Makefile, written as `.venv\Scripts\...` commands because the gate runs without my virtual environment; Black and the frontend tests are excluded with dated reasons. On my branch `fix/68-empty-bm25-index` the gate passed all three checks and my pr-precheck (files in scope, claims match diff, evidence real, diff reviewable). It also flagged that my PR text states the repo has no integration tests, which I never verified, and that I excused Black on the grounds that CI was green. My first run stopped because I had written the manifest to the wrong folder, and the hook needed the same PowerShell fix as the voice guard; the repo checks and the gate's feedback are real, but the PR was already open, so the gate did not decide whether it opened.

**Unit 8: Installed the PR monitor and wrote a playbook from what this repo actually does**

The monitor read PR #261 (28 days quiet, 0 reviews, 0 comments, 6 checks passing) and drafted a polite nudge because my own 14-day first-review threshold was met. Path Review has no merged PRs to measure (96 of the 100 most recent are open, and only 6 have any response), so my playbook records that and sets thresholds from it instead of from a wait I could not count. The monitor first crashed on Windows because Python read GitHub's output as gbk; setting `PYTHONUTF8=1` fixed it. I have not posted the draft; its notes also caught a stale checkbox in my PR description (CI is green now), which I still need to correct.

---

## Why I Chose This Issue

This issue did not come from a wild search. It is the Path Review issue I selected in Unit 1 from the four candidates my scout graded, and I worked it through Units 1 to 4: I claimed it on 2026-10-01, posted a reproduction on 2026-10-02, posted a plan on 2026-10-06, and opened PR #261 on 2026-10-21. In Unit 1 my sandbox rubric accepted all four candidates and the fit profile put #68 first: it is a Python backend bug in a retriever module, like my own RAG coursework project, with defensive error handling and a test-driven finish (remove the strict `xfail` marker) — the kind of work my profile says I want more of. I am carrying this issue forward as my contribution because the reproduction, plan, fix and PR already exist and I want to see them through review, and I hope to learn how a maintainer actually reviews a small defensive fix.

I have not graded #68 with the patched scout this week. I expect it would be rejected on `unclaimed`, because my own PR #261 is open and the Path Review house rule that ignored classmates' claims no longer applies. That reject is the tool working as written, not a reason to doubt the issue, and I am choosing it against that expectation. On the scout itself: it fell short on the wild search because `--no-assignee` could not see claims made through open PRs, so three of five graded issues were rejected as already taken; I added `-linked:pr` and a one-issue-per-repo rule. This week I also replaced my `scope-bounded` check with the staff `scope-feasible` row plus a difficulty note, because open design edges were rejecting honest work. Claim comment: https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68#issuecomment-5925769158

**Toolkit**

- Tool: issue-scout (my search strategy and my rubric): run one scan with three `gh search issues` queries, graded the top five, then graded ArduPilot #14438 directly.
- What it produced: a first scan with 1 accept (SU-OSPO/preprint-bot #175) and 4 rejects; a reject of ArduPilot #14438 for a recent claim comment and a closed-unmerged PR; and a read-out in `scan-output.md`.
- Difficulties: `--no-assignee` missed open PRs that already claimed an issue; two of five graded slots went to one repo; the unit-1 scope check rejected open design edges.
- What changed: added `-linked:pr` to every query, a one-issue-per-repo ranking rule, and the `scope-feasible` check with difficulty notes (dated line in `scan-notes.md`).

---

## Understanding the Issue

**Problem Description**

`KeywordSearcher.index()` passes its tokenized corpus to `BM25Okapi`. When the list of chunks is empty, the corpus is empty too, and the `rank-bm25` library divides by a corpus size of zero and raises `ZeroDivisionError`. `search()` already returns an empty list for an empty index, so `index()` should not crash on one either.

**Expected Behavior**

`KeywordSearcher.index([])` completes without raising, and searching the empty index afterward returns `[]`.

**Current Behavior**

`searcher.index([])` raises `ZeroDivisionError: division by zero` from `rank_bm25.py:52` (`self.avgdl = num_doc / self.corpus_size`), called from `rag/retriever/keyword_search.py:25`.

**Affected Components**

`rag/retriever/keyword_search.py` (`KeywordSearcher.index`) and its covering test `tests/unit/test_keyword_search.py` (`test_empty_index`, marked `xfail` for manifest id H-01).

**Toolkit**

- Tool: repro-check, to grade my claim comment and reproduction report; the `selection.md` verdict from my Unit 1 scout.
- What it produced: an accepted claim and a reproduction report that named the failing line and the root cause.
- Difficulties: none recorded in this phase.
- What changed: nothing.

---

## Reproduction Process

**Environment Setup**

Windows, Python 3.14.5, `rank-bm25` 0.2.2, project virtual environment `.venv`, repository commit `2f4e82f` on a local branch `issue-68-repro`. I confirmed the installed `rank-bm25` version with `python -m pip show rank-bm25`; the package is required by the project itself (`Required-by: pathreview`).

**Steps to Reproduce**

1. From the repository root, activate the environment: `.\.venv\Scripts\Activate.ps1`.
2. Check out `issue-68-repro` and confirm the commit with `git rev-parse --short HEAD` (`2f4e82f`).
3. Run `python -m pytest .\tests\unit\test_keyword_search.py -v --runxfail --tb=long` (`--runxfail` makes pytest run the test instead of treating the `xfail` marker as an expected failure).
4. Observe `test_empty_index` fail with `ZeroDivisionError: division by zero`.

**Reproduction Evidence**

- **Commit showing reproduction:** none of my own; I reproduced on the upstream commit `2f4e82f` without committing to my fork.
- **Screenshots/logs:**

```text
>       searcher.index([])
tests\unit\test_keyword_search.py:140

>       self.bm25 = BM25Okapi(tokenized_corpus)
rag\retriever\keyword_search.py:25

>       self.avgdl = num_doc / self.corpus_size
E       ZeroDivisionError: division by zero
.venv\Lib\site-packages\rank_bm25.py:52: ZeroDivisionError
```

- **My findings:** the issue is real on commit `2f4e82f`. The failure path is `index([])` → `tokenized_corpus = []` → `BM25Okapi([])` → `corpus_size = 0` → `ZeroDivisionError`. My report is posted at https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68#issuecomment-5945984752.

**Toolkit**

- Tool: repro-check, to grade my claim comment and reproduction report before posting.
- What it produced: a reproduction report with environment, steps, expected and actual behavior, a root-cause trace and the traceback.
- Difficulties: the report's suggested fix assumed `search()` needed a new `None` guard; reading the code later showed `search()` already returned `[]` for an empty index.
- What changed: the plan treated that guard as confirmed behavior, not as work to do.

---

## Solution Approach

**Analysis**

`KeywordSearcher.index()` builds `tokenized_corpus` from `chunks` and passes it straight to `BM25Okapi`. With an empty `chunks` list, the corpus size is zero and `rank-bm25` divides by it while computing the average document length. The defect is that `index()` does not handle the empty-corpus case before constructing `BM25Okapi`.

**Proposed Solution**

Detect the empty `chunks` list at the top of `index()`, store it, set `self.bm25 = None`, and return before calling `BM25Okapi([])`. I am deliberately not changing `search()` (its existing guard `if not self.bm25 or not self.chunks: return []` already covers this), the `rank-bm25` dependency, BM25 scoring or ranking, tokenization, or unrelated retriever components.

**Implementation Plan**

1. In `rag/retriever/keyword_search.py`, add the empty-corpus early return in `index()`; leave the non-empty path unchanged.
2. In `tests/unit/test_keyword_search.py`, remove the `xfail` marker from `test_empty_index` and have it check that `index([])` does not raise and a later search returns `[]`.
3. Re-run the reproduction command, then the whole keyword-search test file.

No deviations: the implementation followed the planned scope and approach. My plan comment is at https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68#issuecomment-6009071925.

**Toolkit**

- Tool: plan-check, to grade my plan and plan comment before posting.
- What it produced: a plan with diagnosis, scope, files, approach and test plan. My plan-check run scored 18/20 against the gold labels.
- Difficulties: my rubric's "Honesty about uncertainty" check wrongly rejected a gold-accept package (pkg-05).
- What changed: while checking my own plan, that check pushed me to verify `search()` before planning to change it, so the plan states the existing guard as fact. I kept the stricter check rather than loosening it to win back two packages.

---

## Testing Strategy

Before the fix, `python -m pytest tests/unit/test_keyword_search.py -v --runxfail --tb=long` fails `test_empty_index` with `ZeroDivisionError: division by zero`. After the fix, the same command shows 17 passed, including `test_empty_index` with no `xfail` marker, and searching the empty index returns `[]`. The repo's own checks ran locally with the commands from the Makefile because GNU Make was not available on Windows: unit tests 376 passed and 52 xfailed (the xfails belong to other known issues), `python -m ruff check .` passed, and `python -m mypy api/ core/ ingestion/ rag/ agent/ safety/` reported no issues in 76 source files. On the PR, CI runs eval, frontend, lint, test-integration, test-unit and typecheck, and all six pass.

**Toolkit**

- Tool: pytest with `--runxfail` for the before and after runs, plus ruff and mypy; CI on the PR.
- What it produced: a failing run before the fix, 17 passing after, and green lint, type check and CI.
- Difficulties: no GNU Make on Windows, so I ran the Makefile commands directly.
- What changed: nothing in the fix; the PR records the commands I actually ran.

---

## Implementation Notes

**2026-10-01**

Claimed the issue on GitHub, saying I would reproduce it and report back.

**2026-10-02**

Reproduced on commit `2f4e82f` and posted the reproduction report with the traceback and root cause.

**2026-10-06**

Posted the plan on the issue. While writing it I checked `search()` and found it already handled an empty index, so I removed that from the planned work.

**2026-10-20**

By this date the fix was on branch `fix/68-empty-bm25-index`: early return in `index()` when `chunks` is empty, `self.bm25 = None`, and the `xfail` marker removed from `test_empty_index`. My PR-check run (pr-precheck against its gold-labeled packages) finished at 19/20 on this date.

**2026-10-21**

Opened PR #261 with the before and after evidence, lint, type check and the AI-assistance note.

**2026-11-18**

Ran the ship-gate on the branch (PASS) and the PR monitor on PR #261: 28 quiet days, no reviews, 6 checks passing. The monitor drafted a polite nudge; I have not posted it.

**Toolkit**

- Tool: AI assistance (Claude Code) to understand the issue, interpret test results and organize the PR text, as the PR itself discloses; pytest for verification.
- What it produced: the two-file change, checked against the original reproduction, and the PR description.
- Difficulties: none beyond the missing GNU Make.
- What changed: nothing.

---

## Pull Request

**PR Link:** https://github.com/codepath/pathreview-ai301-fa26-s3/pull/261

**PR Description:** "Fix #68: Handle empty BM25 keyword search indexes." The PR adds an early return in `KeywordSearcher.index()` when no chunks are provided, sets `self.bm25` to `None`, removes the `xfail` marker from `test_empty_index`, and leaves `search()` unchanged. It records the before and after runs, the local lint and type checks, and a note that I used AI assistance and checked its explanations against the code and the tests. It closes #68.

**Maintainer Feedback:**

- 2026-11-18: none yet.

**Status:** Awaiting review

**Toolkit**

- Tool: the ship-gate (my manifest's three checks, then my pr-precheck on branch `fix/68-empty-bm25-index`, plan.md, test_evidence.md and pr_draft.md), run by hand with `check_gate.py --branch`.
- What it produced: `ship-gate: PASS`. Unit tests, ruff and mypy passed, and pr-precheck passed files in scope, claims match diff, test evidence real, diff reviewable (2 files, 4 insertions and 4 deletions) and standards and disclosure.
- Difficulties: it did not run before I opened the PR, because the PR was already open from Unit 4. It flagged that my PR text claims the repo has no integration tests, which I never verified (CONTRIBUTING lists a `test-integration` job), and that my manifest excused Black on the grounds that CI was green. My first run stopped because I had written the manifest to the wrong folder, and the hook needed PowerShell support on my machine.
- What changed: I wrote the manifest correctly and added PowerShell to the hook. I still need to correct the stale checkbox and the integration-test note in the PR description.

---

## Learnings and Reflections

**Technical Skills Gained**

I learned why `rank-bm25` fails on an empty corpus (it divides by the corpus size) and how to fix it with a guard in `index()` that leaves `self.bm25` as `None`. I used pytest's `--runxfail` to see the real traceback behind a strict `xfail` test and learned that removing the marker is part of the fix. On the tooling side I learned `gh search issues` qualifiers such as `-linked:pr` and that a search filter and a rubric check answer different questions.

**Challenges Overcome**

My first scan rejected three of five issues because other contributors' PRs already claimed them; I added `-linked:pr` and checked it on a real case. On Windows, my hooks only worked after I added the PowerShell tool to the guard scripts and rewrote files without a byte-order mark, and the PR monitor needed `PYTHONUTF8=1`. While planning my fix I also found that `search()` already handled an empty index, so I changed the plan instead of editing code that did not need it.

**What I'd Do Differently Next Time**

I would check the issue's linked PRs and every comment before spending time on it, run the scout on the issue I plan to take before I plan, and keep my PR description in step with the CI state. I would also pick the real issue from a wild search at the start of the term, instead of continuing the sandbox issue, so my scout is tested on what I actually work on.

---

## Resources Used

- docs/CONTRIBUTING.md in the Path Review repo: branch and commit conventions, the CI-must-be-green rule, and the instruction to remove the strict `xfail` marker when fixing a seeded bug.
- Issue #68 and my own reproduction and plan comments on it (https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68): the maintainer-written description of the empty-corpus failure and the files involved.
- The `rank-bm25` traceback line `self.avgdl = num_doc / self.corpus_size` (rank_bm25.py:52), which explained the cause.
- The `gh search issues` manual and GitHub's guide to searching issues, for the filters and `-linked:pr`.
