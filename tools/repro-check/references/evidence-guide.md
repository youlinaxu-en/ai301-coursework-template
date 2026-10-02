# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

Where it lives:
In an eval bundle, look in the issue context and the reproduction report's environment section. In live mode, check the issue thread for the affected version and platform, then compare it with the environment information stated in the student's draft reproduction comment.

What good looks like:
The report identifies the relevant software or package version, operating system, runtime or language version, and important dependencies when they may affect the result. The environment should match the issue's stated target, or any difference should be explicitly called out.

## Steps

Where it lives:
In an eval bundle, look in the reproduction report for setup instructions, commands, inputs, and the sequence of actions used to trigger the reported behavior. In live mode, compare the student's draft steps with any reproduction instructions already present in the issue thread or repository documentation.

What good looks like:
The steps describe a clear path from the starting state to the point where the issue is triggered. Another person should be able to attempt the reproduction without needing important unstated setup, commands, inputs, or assumptions.

## Behavior shown

Where it lives:
In an eval bundle, look at the issue description and compare it with the reproduction report's output excerpts, error messages, logs, screenshots, or other artifacts. In live mode, compare the issue's reported behavior with the artifacts included or quoted in the student's draft comment.

What good looks like:
The evidence shows the same behavior described in the issue, including the relevant error, incorrect output, or observable failure. Evidence of a different or only loosely related problem is not sufficient.

## Honesty
Where it lives:
In an eval bundle, compare the reproduction report's conclusion with the logs, outputs, screenshots, and other artifacts it provides. In live mode, compare the student's claims in the draft comment with the actual evidence shown.

What good looks like:
The conclusion does not claim more than the evidence supports. A report may honestly state that the issue could not be reproduced if the environment, steps, and observed result are documented; an unsupported claim of successful reproduction is not acceptable.

## Comms

Where it lives:
In an eval bundle, review the claim comment, repro report, repo-facts block, and any stated repository contribution rules. In live mode, check the issue thread, repository contribution documentation, issue templates, and the student's draft comments.

What good looks like:
The comment is specific about what was tested, the affected version, expected behavior, actual behavior, and observed evidence. It follows repository-specific contribution requirements and avoids vague statements, unsupported root-cause claims, boilerplate confirmations, or claims that are stronger than the available evidence.