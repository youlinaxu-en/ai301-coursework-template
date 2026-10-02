# Rubric: is this a good first issue?

All recency thresholds are measured against the bundle's capture date in
eval mode, and against today in live mode.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| repo-alive | Repo facts: the `archived:` flag on the repo line and `last push to any branch` (live: the archived banner on the repo front page, and the newest commit date above the file list plus the Branches page) | `archived: no` AND the last push to any branch is within 90 days | required |
| maintainer-active | Repo facts: `last 5 default-branch commits`, with author names (live: the front-page commit list; open a bot commit to see whose PR it merged) | At least one default-branch commit within 90 days that was authored by a human, or by a bot merging a human's pull request | required |
| scope-bounded | The issue title, body, and full comment thread | The issue asks for exactly one bounded change with a settled spec: what to change is stated by the opener or confirmed by a maintainer in the thread. A terse body, a checklist of acceptance criteria, or a bug report without repro steps still passes when the work asked for is one bounded change. Fails on any scope trigger listed below the table | required |
| unclaimed | Repo facts: the `this issue: assignees; linked PRs` line, plus any PRs mentioned and any claim comments in the thread (live: the Assignees and Development sidebar boxes plus the thread; when sidebar and thread disagree, believe the thread) | No assignee is set, AND no linked or thread-mentioned PR is currently open, AND no claim comment ("I'll take this", "working on this") from the last 90 days stands unreleased — a claim older than 90 days with no open PR is stale and does not block, and a claim a maintainer has since re-opened to takers does not block. Closed-unmerged PRs are not claims (they are graded under no-abandoned-attempts). Apply any house rule from scope.md about whose claims count | required |
| policy-allows-ai | Repo facts: the `contribution policy` line (live: CONTRIBUTING.md in the repo root or `.github/` and the contributor docs it links to, dedicated files like AI_POLICY.md or AI_USAGE_POLICY.md, and PR/issue templates) | The policy does not ban the AI-assisted workflow: an outright ban ("we do not accept AI-generated code/documentation") fails; conditions (disclose AI use, personally understand and test every change, human-review AI output, no fully AI-generated submissions) pass; silence — no policy found after looking in the places named — passes | required |
| release-recent | Repo facts: `latest release` (live: the Releases box in the repo front page's right sidebar) | A release was published within the last 12 months | preferred |
| maintainer-responsive | Repo facts: `maintainer first-response sample` (live: time to first Owner/Member/Collaborator reply on 5 recently updated issues) | At least 2 of the 5 sampled issues got a maintainer first response within 30 days | preferred |
| maintainer-endorsed | The issue header: labels, opener, and opener's association, plus maintainer comments in the thread | The issue carries a `good first issue` or `help wanted` label, or was opened or confirmed in-thread by someone with Owner/Member/Collaborator association | preferred |
| no-abandoned-attempts | The `linked PRs` line (states per PR) and PRs mentioned in the thread | No closed-unmerged PR is linked to or mentioned for this issue | preferred |

### Scope triggers (any one fails scope-bounded)

- The issue is an umbrella or tracking issue: a list of sub-items meant
  to be split into separate pieces of work.
- The design is still being debated in the thread and no maintainer has
  settled what the change should be.
- A maintainer says the fix touches core internals (parser, architecture,
  a rewrite).
- The issue is a pure usage or support question ("how do I get this to
  work?"), not a change to the software.
- The issue is a feature wish whose spec would require a product decision
  no maintainer has made (the thread contains no settled "what", only a
  want).

## Verdict rule

- **Accept** if and only if every `required` check grades `pass`. Any
  `required` fail is a **reject**.
- `unclear` on a `required` check counts as **fail**: a first issue whose
  evidence cannot be verified is not a first issue to take. Note the one
  built-in exception: for policy-allows-ai, finding no stated policy after
  looking is silence, which the check itself grades `pass` — grade
  `unclear` only when the evidence source is genuinely absent (no
  contribution-policy line in the bundle, or the live repo's policy pages
  are unreachable).
- `preferred` checks never change the verdict. Among accepted issues they
  are ranking support: more `preferred` passes is a reason to rank one
  accepted issue above another (alongside the fit profile in scope.md,
  which orders the accepted list in live mode). `unclear` on a
  `preferred` check simply earns no ranking credit.
