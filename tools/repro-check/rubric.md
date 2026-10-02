# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Repository activity | Repository activity history, including recent commits, maintainer responses, issues, and pull requests | Recent repository activity may be noted as context, but repository inactivity alone does not make an otherwise complete reproduction package unready to post. | preferred |
| Affected version identified | Issue description and reproduction report | The affected software, package, or repository version is clearly identified and specific enough for another person to reproduce or compare the behavior. | required |
| Reproduction environment recorded | Repro report environment record | The report records the relevant environment information, such as operating system, runtime or language version, package versions, and dependencies that could affect the result. | required |
| Expected behavior recorded | Issue description and repro report | The expected result is clearly stated so that a reader can determine what should have happened. | required |
| Actual behavior recorded | Error message, console output, logs, screenshots, or other reproduction artifacts | The actual observed behavior is recorded with enough detail to distinguish it from the expected behavior. | required |
| Expected and actual behavior differ | Expected behavior compared directly with the reproduced output or artifact | The evidence demonstrates a meaningful difference between the expected behavior and the actual behavior reported in the issue. | required |
| Reproduction steps complete | Reproduction steps together with concrete setup, commands, inputs, or linked reproduction details available in the package | Pass if the package provides enough concrete information for another reader to reproduce the reported behavior from setup to trigger. Information may appear outside the steps section if it is explicitly present elsewhere in the package. Fail only when an essential setup, input, command, or trigger condition is missing. | required |
| Behavior matches the issue | Reproduction artifacts read against the original issue description | The reproduced behavior corresponds to the problem described in the issue rather than a different, adjacent, or unrelated failure. | required |
| Outcome supported by evidence | Reproduction conclusion together with logs, outputs, screenshots, or other artifacts | The stated conclusion accurately reflects the evidence. A well-supported cannot-reproduce result may pass, while an unsupported claim of successful reproduction fails. | required |
| Repository conventions followed | Repo-facts contribution policy, issue template requirements, and candidate comments | Pass unless the candidate comment violates an explicit repository rule or makes a substantive unsupported coordination claim such as assignment, reservation, contribution ownership, or a concrete promise to fix. Minor stylistic or formatting differences do not fail this check. | required |
| Required disclosure present | Repo-facts AI-use or disclosure policy read against the claim comment and repro report | Any disclosure explicitly required by the repository is present in the required form. If no disclosure is required, this check passes. | required |
## Verdict rule
Accept only if every required check passes.

Reject if any required check receives fail or unclear.

Preferred checks do not change the verdict.

An evidenced cannot-reproduce result may still pass if the environment, steps, and observed outcome are documented and the conclusion accurately reflects the evidence.