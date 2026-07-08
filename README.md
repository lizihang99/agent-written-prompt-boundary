# Runtime Prompt Boundary Skill

A Codex skill for designing product runtime prompts without leaking development conversation, project backstory, implementation details, or unsupported assumptions into the model call.

The core idea is simple: prompt work is information routing. Every fact should land in the cheapest artifact that preserves its value:

- runtime instruction
- runtime variable
- output contract
- few-shot example
- eval case
- implementation note
- proposed assumption
- exclusion

## When To Use

Use this skill when building or editing an LLM-powered feature and the conversation mixes product requirements, UX intent, architecture, examples, schemas, or implementation details.

Typical cases:

- turning product discussion into a runtime system/developer prompt
- shrinking an overgrown prompt that absorbed project backstory
- separating stable instructions from dynamic user input
- protecting JSON/schema/tool contracts from accidental drift
- keeping safety, privacy, refusal, uncertainty, and escalation rules explicit

## What It Prevents

This skill is especially tuned against "helpful invention":

- inventing JSON schemas when no downstream contract exists
- adding fields or enum values to an exact parser contract
- treating common naming conventions as evidence
- expanding safety policy through examples or broad trigger lists
- hard-coding sample user data into stable prompt text
- pasting product history instead of distilling behavior rules

## Repository Layout

```text
.
├── SKILL.md
├── agents/
│   └── openai.yaml
├── cases/
│   ├── 01-distill-product-backstory.md
│   ├── 02-preserve-safety-escalation.md
│   ├── 03-extract-dynamic-runtime-data.md
│   ├── 04-output-contract-vs-friendly-prose.md
│   ├── 05-split-overloaded-prompt.md
│   └── README.md
└── references/
    ├── output-template.md
    └── priority-rules.md
```

## Main Concepts

### Non-Negotiable Safety Gate

Safety, compliance, privacy, abuse-prevention, uncertainty, escalation, identity, and authorization constraints must survive prompt slimming. Brevity never wins over safety behavior.

### Proposed Assumptions

Useful defaults that are not evidenced by the user brief, code, schema, or downstream consumer belong in `proposed-assumption`. They should stay outside the runtime contract until accepted or proven.

Example:

```text
risk_level -> string
```

is supported if the brief names only the field.

```text
risk_level -> low | medium | high
```

is only a proposed assumption unless the downstream contract says so.

### Closed Output Contracts

If downstream code expects exact fields, enum values, or output type, preserve that contract exactly. Do not add wrappers, metadata, required fields, enum values, or parser obligations unless the code or user request supports them.

## Pressure Cases

The `cases/` directory contains regression scenarios used to test whether the skill holds its boundary under realistic pressure:

1. Distill product backstory into runtime behavior.
2. Preserve safety and escalation constraints without expanding policy.
3. Extract dynamic runtime data instead of hard-coding samples.
4. Keep strict machine-readable output compatible with friendly prose.
5. Split overloaded prompts into staged calls.

Run at least three pressure cases after materially changing the skill. Include one safety case, one dynamic-data case, and one overloaded-prompt case.

## Expected Output Shape

Unless the user asks for raw prompt text only, the skill expects these artifacts:

- Boundary Summary
- Boundary Ledger
- Runtime Prompt
- Runtime Variables
- Output Contract
- Change Note for existing prompts

See `references/output-template.md` for the exact headings.

## Status

This version has been pressure-tested with local advisor runs against the included cases. The hardest observed failure pattern was agents treating helpful guesses as contracts; the current skill explicitly routes those guesses to `proposed-assumption`.
