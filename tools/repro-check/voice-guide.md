# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

I am a student reproducing reported software issues as part of a course project. I report only what I personally tested and observed in my own environment. Readers should expect concise reproduction details, concrete evidence, and clear separation between observed behavior and unverified assumptions.

## Rules I write by

Rule: Report only what I actually tested

I only make claims that are supported by tests I personally ran. I do not generalize my result to other systems, versions, or users unless I have evidence for that claim.

Wrong: "This bug affects all Linux users."

Right: "I reproduced this behavior on Ubuntu 24.04 using the version listed below."

Rule: Include concrete evidence

When I say that an issue reproduced or did not reproduce, I include the relevant error message, output, log, or other observable result that supports the conclusion.

Wrong: "I got the same problem."

Right: "After running the reproduction steps, the command returned ValueError, matching the failure described in the issue."

Rule: Separate observation from explanation

I distinguish between what I observed and what I think may have caused it. I do not present a possible root cause as confirmed unless the evidence directly supports it.

Wrong: "The parser is definitely causing this bug."

Right: "The failure occurs during the parsing step, but I did not verify the underlying root cause."

Rule: State the environment and version clearly

I include the relevant software version and environment details when they may affect reproducibility. I avoid vague descriptions such as "latest version" when a specific version is available.

Wrong: "I tested this on the latest version and it failed."

Right: "I reproduced the issue using version 2.4.1 with Python 3.12 on Ubuntu 24.04."

Rule: Compare expected and actual behavior directly

I clearly state what I expected to happen and what actually happened so that another reader can understand why the observed result is relevant to the issue.

Wrong: "The output is wrong."

Right: "I expected the command to return a valid result, but it instead terminated with the error shown below."

## Things I never post

Claims that I reproduced behavior I did not personally test.

Unsupported statements about the root cause of an issue.

Claims that a problem affects all users, platforms, or versions without evidence.

Vague confirmations such as "same issue" without my own reproduction evidence.

Environment or version information that I know is inaccurate or incomplete.

Promises to fix an issue, submit a patch, or perform additional work unless I am actually prepared to do so.

Results that hide or omit evidence that contradicts my conclusion.