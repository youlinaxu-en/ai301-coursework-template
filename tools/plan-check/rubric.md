# Rubric: is this plan ready to post and build from?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diagnosis follows evidence | The plan's stated cause, root-cause hypothesis, or proposed fix read against the issue context and the reproduction evidence block (the reproduced steps, observed behavior, and any error/output). | Pass if the plan names a cause that is actually supported by the reproduced behavior, does not contradict the evidence, and does not target a symptom while ignoring the observed root cause. A plan that explains the bug in a way the evidence does not support is a fail. | required |
| Scope is bounded | The plan's in-scope statement, files/areas, and any not-in-scope line or exclusions, read against the issue and repo-facts block. | Pass if the change is clearly bounded to the affected behavior and minimal files/areas, with obvious exclusions for unrelated cleanup, broad refactors, or speculative work. A drive-by rewrite or unbounded change is a fail. | required |
| Executable plan for a stranger | The plan's implementation steps, file targets, order of work, and approach, read against the issue and repo-facts block. | Pass if a reasonable stranger could start the fix without asking the author what to do next: the affected files/areas, the plan of attack, and the order of work are concrete and actionable. Missing decision points or vague hand-waving are a fail. | required |
| Test plan observes the right behavior | The plan's test plan or verification steps read against the reproduced evidence and the project's expected validation workflow. | Pass if the plan names a concrete observable check that matches the bug's trigger and confirms the fixed behavior, rather than a vague “should work” claim or a test that proves nothing. | required |
| Honesty about uncertainty | The plan's stated assumptions, risks, unknowns, or mid-build deviations, read against the issue context and the repo-facts block. | Pass if the plan distinguishes what is known from what is assumed, surfaces genuine unknowns or risks, and records a deviation honestly when the build changes course. False certainty, hidden assumptions, or silent drift is a fail. | required |
| Comment is thread-aware and repo-aware | The plan comment read against the issue thread highlights or maintainer signals and the repo-facts block's contribution policy, templates, and AI-use disclosure requirements. | Pass if the comment explains the approach in the issue's terms, respects repo conventions, and is specific to the case instead of generic boilerplate. The comment should not ignore maintainer signals or required disclosure rules. | required |
| Comment quality is useful, not boilerplate | The plan comment and the plan itself read against the issue and reproduction evidence. | Pass if the comment is helpful to a maintainer: it states the diagnosis, the scope, the intended fix, and the verification method in a readable, non-generic form. Boilerplate or copy-paste language is a fail. | preferred |

## Verdict rule

Accept only if every required check passes. Preferred checks never change the verdict. If any required check is fail or unclear, the verdict is reject. An unclear grade counts as fail unless the rubric explicitly says otherwise; a plan that cannot be verified from the package is not ready to build from.
