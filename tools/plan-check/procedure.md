# Procedure: how this skill grades a plan package

## Read order

1. Read the issue context first and note the problem statement, expected behavior, observed failure, and any maintainer instructions or thread highlights. Record the concrete bug the plan is supposed to fix.
2. Read the reproduction evidence before the candidate plan and extract the exact behavior it proves: the trigger, the observed output or error, the expected behavior, and any artifacts or commands that matter. This matters because every required check compares the plan against what the evidence actually pins down; a plan that contradicts the evidence is rejected even if it looks polished.
3. Read the candidate plan next and record its diagnosis, scope statement, implementation steps, and test plan. Make a short list of claims it makes about cause, files, and verification before you judge them.
4. Read the plan comment after the plan so you can judge thread-awareness and repo conventions separately from the technical content. Note whether the comment says the same thing the plan says and whether it matches the issue's maintainers or repo policy.
5. Read the repo-facts block last if present, so you can check whether the plan and comment match the repo's stated workflow, templates, or disclosure expectations.

The reason for this order is that the issue and reproduction evidence provide the objective facts, while the plan is judged against those facts. The comment and repo facts are then checked for alignment, not for discovery of the root cause.

## Evidence gathering

For each rubric check, gather the specific fact from the package before grading it.

- Diagnosis follows evidence: pull the plan's root-cause description or fix claim from the candidate plan, and compare it to the issue context and reproduction evidence. Record the specific reproduced behavior the plan is claiming to explain.
- Scope is bounded: pull the plan's scope statement, affected files/areas, and any exclusions or not-in-scope lines. Record the exact files or subsystems named and whether the change remains narrow.
- Executable plan for a stranger: pull the implementation steps, files, order of work, and any approach notes from the plan. Record whether a stranger could start the work without asking the author to clarify the next step.
- Test plan observes the right behavior: pull the plan's validation steps, commands, or user-visible checks. Record which behavior is supposed to be observed and whether it matches the reproduced failure or the intended fix.
- Honesty about uncertainty: pull the plan's assumptions, risks, unknowns, or record of deviation. Record whether the plan states uncertainty honestly or presents speculation as fact.
- Comment is thread-aware and repo-aware: pull the plan comment and compare it with issue highlights or maintainer signals and the repo-facts block. Record any required repo conventions or AI-use/disclosure expectations the comment must satisfy.
- Comment quality is useful, not boilerplate: pull the plan comment and the plan together and note whether the comment is specific to this issue, explains the approach, and helps a maintainer understand the change.

If a check's evidence is not present in the package, grade the check as fail unless the rubric allows it to be marked unclear because the evidence exists but cannot be verified.

## Check execution

Run the checks in this order:

1. Diagnosis follows evidence
2. Scope is bounded
3. Executable plan for a stranger
4. Test plan observes the right behavior
5. Honesty about uncertainty
6. Comment is thread-aware and repo-aware
7. Comment quality is useful, not boilerplate

For each check:

- State the exact fact or quote that decided the grade.
- Compare the proposed claim to the evidence.
- If the evidence clearly supports the claim, mark pass.
- If the evidence directly contradicts the claim, ignores the evidence, or omits a required condition, mark fail.
- If the evidence is present but not enough to decide, mark unclear.
- Apply the rubric's comment about unclear and default to fail when the package does not give enough proof.

Do not re-read the entire package for every check. After the first pass through the relevant sections, use the notes you recorded during evidence gathering to evaluate each remaining check. The one exception is when a check depends on a later part of the package that you have not yet read, such as the repo-facts block or the plan comment; in that case, read only that specific section before grading that check.

## Verdict assembly

1. Assign a grade of pass, fail, or unclear to each check using the exact evidence recorded in the previous step.
2. Apply the verdict rule from the rubric: accept only if every required check passes; preferred checks never change the verdict; if any required check is fail or unclear, the verdict is reject.
3. Quote the most decisive fact for the failing or passing required check in the output. The deciding fact must be something the package actually says or shows, not a restatement of the rubric.
4. If the plan is rejected, the output should identify the specific required check that failed and the evidence that drove it. If the plan is accepted, the output should still include the evidence that established the required checks all passed.

This procedure is intentionally explicit so two graders who read the same package will produce the same verdict: the issue and reproduction evidence establish the truth conditions, the plan is judged against those facts, and the comment is judged only after the technical core has been checked.
