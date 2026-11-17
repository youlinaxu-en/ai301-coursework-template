# From issue scout to open PR: fixing an empty-index crash with four rubric-driven checkers

## Overview

Path Review is a course project with a RAG pipeline that uses BM25 keyword search. Issue [#68](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68) reported that `KeywordSearcher.index([])` crashes with a `ZeroDivisionError` on an empty index. I picked the issue with a scout skill, claimed it, reproduced the crash, planned the fix, and opened [PR #261](https://github.com/codepath/pathreview-ai301-fa26-s3/pull/261) with a four-line fix and a regression test. All six CI jobs pass. As of 2026-11-17 the PR is still open and unreviewed. At each stage I used a Claude Code skill I built: `issue-select`, `repro-check`, `plan-check` and `pr-precheck`. The part I wrote myself is each skill's judgment: its rubric, its fit profile and a voice guide for how I write upstream. I tested each rubric against 20 labelled packages.

## What happened

**Unit 1: choosing the issue (2026-09-22).** My `issue-select` rubric graded four candidates and ranked #68 first, because it is Python backend code in a retriever, like my coursework project. The `scope-bounded` evidence described the fix before I wrote it, and the same output flagged a risk I chose to discount:

```text
"scope-bounded", "grade": "pass", "evidence": "maintainer-filed single fix: guard empty corpus in KeywordSearcher.index() ... drop xfail H-01, est. 2-4h"
"maintainer-responsive", "grade": "fail", "evidence": "0 of 5 recently commented issues ... have any maintainer first response"
```

I judged that a seeded classroom tracker, where staff review PRs instead of replying in threads. The tool's eval run was `agreement: 18/20 (bar: 18/20: PASS)`. It missed issue-15 and issue-19. I kept the `scope-bounded` wording, because rephrasing it to flip exactly those two cases would have been tuning to the test set.

**Unit 2: claiming and reproducing.** I claimed the issue, then reproduced the crash on commit `2f4e82f` (Windows, Python 3.14.5, rank-bm25 0.2.2). The repo marks the failing test `xfail`, so I ran it with `--runxfail`:

```text
>       self.bm25 = BM25Okapi(tokenized_corpus)
rag\retriever\keyword_search.py:25
>       self.avgdl = num_doc / self.corpus_size
E       ZeroDivisionError: division by zero
```

An empty `chunks` list gives an empty corpus, and `BM25Okapi([])` divides by a corpus size of zero. I posted this as the [reproduction report](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68#issuecomment-5945984752).

**A change I made because of a miss.** My `repro-check` rubric did badly at first: a 3-package smoke run scored 2/3, and a run on pkg-19 and pkg-20 scored 0/2. Both should have been rejected, and my rubric accepted them. pkg-19's comment broke the repository's contribution rules, and my rubric only looked at technical evidence. I added a required check. It reads now:

```text
| Repository conventions followed | ... | Pass unless the candidate comment violates an explicit repository rule or makes a substantive unsupported coordination claim such as assignment, reservation, contribution ownership, or a concrete promise to fix. Minor stylistic or formatting differences do not fail this check. | required |
```

The "minor differences do not fail" clause is deliberate, because a stricter version would reject good packages over formatting. The final run was `agreement: 19/20 (bar: 18/20: PASS)`, and pkg-19 now matches its gold label.

**Units 3 and 4: the plan and the pull request.** My plan was to guard the empty case in `index()`, leave `search()` alone because it already returns `[]`, and touch two files. `plan-check` scored 18/20 on 2026-10-05, and `pr-precheck` scored 19/20 on 2026-10-20. On 10-20 I also added three PR rules to my voice guide, including "Disclose shortfalls and test results plainly". My PR draft follows it. Make was not installed on my machine, and the draft says so. It says I ran the equivalent commands directly, and it leaves the "CI is green" and integration-test boxes unchecked until they were true.

**The fix.** Commit `2fc808c` (2026-10-05) matches the plan and touches only the two planned files:

```diff
         self.chunks = chunks
+        if not chunks:
+            self.bm25 = None
+            logger.info("keyword_index_built", chunk_count=0)
+            return
...
-    @pytest.mark.xfail(strict=True, reason="issue #68 ...")
     def test_empty_index(self, searcher):
```

Removing the strict `xfail` marker turns the existing test into the regression test. Re-running the reproduction command now gives `test_empty_index PASSED` and 17 of 17 keyword-search tests passing. The full unit run was 376 passed and 52 xfailed (other known issues), with `ruff` and `mypy` clean.

**What landed.** I opened PR #261 on 2026-10-21, and all six CI jobs pass. The scout's Unit 1 description of the fix (one small guard plus dropping `xfail`) matched what I shipped. The PR has no review comments and is not merged, so I have no maintainer feedback to quote.

## Limitations and what's next

The PR is unreviewed. That is the risk my scout flagged on 2026-09-22 and I discounted: the PR I opened on 2026-10-21 has had no response in the 27 days since. My "classroom quirk" judgment may be right, but I have no evidence for it yet. Next I will check the PR for review activity and respond to any within a day. If maintainers stay silent, I will give the `maintainer-responsive` check more weight in my scout.

The fix covers one failure, an empty index. I did not test other degenerate inputs, such as chunks with empty text. My "before" trace comes from my earlier reproduction report, not a re-run on the pre-fix commit.

The checkers are accurate on 20-package test sets, not on every repo. Each one still misses valid packages, such as pkg-09 for `repro-check`, because I kept the strict required checks on purpose. Loosening them risks accepting wrong-target reproductions, but it means my tools lean toward "hold." Next I would add pkg-09's pattern as a labelled case, loosen that check just enough to accept it, and re-run the full set to confirm wrong-target packages are still rejected. Finally, my first `repro-check` rubric was not saved, so I can show the check as it is now but not an exact before-and-after diff.
