# Pressure Cases

Use these scenarios to regression-test the skill after edits or major workflow changes.

## Minimum Run Set

Run at least three cases:

- one safety-preservation case
- one dynamic-data extraction case
- one overloaded-prompt split or stage case

## Pass Criteria

A case passes when the result:

- keeps development-only context out of the runtime prompt
- preserves safety, refusal, escalation, and uncertainty behavior
- extracts dynamic data into `runtime-variable`
- uses `output-contract` for parser or schema requirements
- avoids duplicating the same fact across instructions, examples, and evals without reason

If a case fails, tighten the main skill or the reference files before considering the edit complete.
