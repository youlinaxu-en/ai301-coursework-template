# Diagnosis

Issue #68 occurs because `KeywordSearcher.index([])` passes an empty tokenized corpus directly to `BM25Okapi`.

The Unit 2 reproduction confirmed the failure on commit `2f4e82f`.

Relevant evidence:

> `searcher.index([])`

raises:

> `ZeroDivisionError: division by zero`

The traceback shows the failure path:

> `rag\retriever\keyword_search.py:25`  
> `self.bm25 = BM25Okapi(tokenized_corpus)`

followed by:

> `.venv\Lib\site-packages\rank_bm25.py:52`  
> `self.avgdl = num_doc / self.corpus_size`

When `chunks` is empty, `tokenized_corpus` is also empty. `BM25Okapi([])` initializes with a corpus size of zero and attempts to compute the average document length by dividing by that corpus size.

Therefore, the failure is caused by `KeywordSearcher.index()` not handling the empty-corpus case before constructing `BM25Okapi`.

# Scope

The change will make `KeywordSearcher` handle an empty index safely.

The implementation will:

- Prevent an empty corpus from being passed to `BM25Okapi`.
- Preserve the empty chunk list as the current index state.
- Rely on the existing `search()` guard for empty-index queries.
- Update the existing empty-index test so it represents expected behavior instead of an expected failure.
- Verify that non-empty keyword-search behavior remains unchanged.

The change will not:

- Modify the `rank-bm25` dependency.
- Change BM25 scoring or ranking behavior for non-empty corpora.
- Change tokenization behavior.
- Refactor unrelated retrieval components.

# Files to Change

Expected files:

- `rag/retriever/keyword_search.py`
- `tests/unit/test_keyword_search.py`

No other files are expected to require changes unless implementation reveals an existing related contract that must be updated.

# Approach

1. Update `KeywordSearcher.index()` to detect an empty `chunks` list before constructing `BM25Okapi`.

2. When the corpus is empty:
   - store the empty chunk list in `self.chunks`;
   - keep the BM25 index in an empty/uninitialized state, such as `self.bm25 = None`;
   - return without calling `BM25Okapi([])`.

3. Leave the existing `search()` empty-index guard unchanged. The current
   implementation already returns `[]` when `self.bm25` or `self.chunks`
   is empty, so no additional search-path change is required.

4. Preserve the existing behavior for non-empty corpora:
   - tokenize each chunk;
   - initialize `BM25Okapi`;
   - execute normal ranking and result selection.

5. Remove the `xfail` marker from `test_empty_index` once the behavior is fixed, and ensure the test checks the intended empty-index behavior.

# Test Plan

First, re-run the Unit 2 reproduction command:

```powershell
python -m pytest .\tests\unit\test_keyword_search.py -v --runxfail --tb=long
```

Before the fix, the reproduction produced:

> `ZeroDivisionError: division by zero`

After the fix, `test_empty_index` should complete without raising an exception.

The expected behavior is:

- `KeywordSearcher.index([])` completes successfully.
- Searching the empty index returns `[]`.
- The empty-index test passes without relying on `xfail`.
- Existing non-empty keyword-search tests continue to pass.

Then run the complete keyword-search unit test file:

```powershell
python -m pytest .\tests\unit\test_keyword_search.py -v
```

The expected result is that all keyword-search unit tests pass.

# Risks and Unknowns

# Risks and Unknowns

The existing `search()` implementation already handles an empty or
uninitialized BM25 index by returning `[]`, so setting `self.bm25` to
`None` for an empty corpus is consistent with the current search path.

The main regression risk is accidentally changing behavior for non-empty
corpora. The implementation should therefore keep the existing
tokenization and `BM25Okapi` initialization path unchanged whenever
`chunks` is non-empty.

Another consideration is test coverage: the empty-index test should
verify both that `index([])` does not raise and that searching afterward
returns an empty result, while the remaining keyword-search tests verify
that normal ranking behavior is preserved.

## Deviations

The implementation followed the planned scope and approach. No material deviations were required.