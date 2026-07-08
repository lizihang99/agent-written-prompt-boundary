# Priority Rules

Use this file when a fact plausibly fits multiple roles.

## Decision Order

Ask these questions in order. Stop at the first clear match.

1. **Irrelevant to this call?**  
   Use `exclude`.

2. **Only useful to the coding agent?**  
   Use `agent-only`.

3. **Only affects implementation or wiring?**  
   Use `implementation-detail`.

4. **Only needed for testing or review?**  
   Use `eval-case`.

5. **Dynamic at runtime?**  
   Use `runtime-variable`.

6. **Useful but not evidenced yet?**  
   Use `proposed-assumption`.

7. **Required structurally by downstream code or tooling?**  
   Use `output-contract`.

8. **Stable behavioral or safety policy?**  
   Use `derived-runtime-rule`.

9. **Example materially improves runtime output?**  
   Use `few-shot-example`.

10. **Still useful for design, but not runtime?**  
   Use `design-context`.

## Tie-Break Notes

- Safety, refusal, escalation, and uncertainty rules beat brevity concerns.
- Safety preservation is not a license to invent domain policy. Mark new guardrails as assumptions unless supported by evidence.
- Examples are not neutral. If an example adds a new trigger, category, threshold, or exception, it expands policy.
- A dynamic fact does not become a rule just because it appears in the conversation more than once.
- A parser requirement belongs in `output-contract` even when the prompt also mentions it in prose.
- An output shape belongs in `output-contract` only when the user, code, schema, tool, or downstream consumer requires it.
- Exact downstream fields and enum values are closed by default. Additions must be labeled as proposed assumptions outside the contract.
- Proposed assumptions do not belong in the formal runtime output format until accepted by the user or evidenced by code.
- Do not infer enum values, ranges, wrappers, or parser behavior from common naming conventions alone.
- Do not keep the same fact in both `few-shot-example` and `eval-case` unless the duplication is deliberate and documented.
- If a fact is both useful background and a stable runtime behavior rule, keep the distilled behavior as `derived-runtime-rule` and keep the backstory as `design-context`.

## Quick Examples

| Fact | Primary role | Why |
| --- | --- | --- |
| "Do not give legal reassurance when evidence is incomplete." | `derived-runtime-rule` | Stable safety behavior. |
| "Return JSON with `summary` and `risk_level`." | `output-contract` | Downstream parser depends on it. |
| "Maybe return JSON if the UI later needs it." | `proposed-assumption` | Useful suggestion, not an evidenced contract. |
| A field named `risk_level` with no enum listed | `output-contract` | Field is required, but enum values are not. |
| Suggested enum values for `risk_level` with no schema evidence | `proposed-assumption` | Common convention is not downstream evidence. |
| The user's draft email | `runtime-variable` | Dynamic input to process. |
| "We store results in Postgres." | `implementation-detail` | Runtime model does not need storage design. |
| A tricky edge case used for regression review | `eval-case` | Review artifact, not prompt text. |
| "This product is for first-time creators." | `design-context` | Distill into tone or audience rules if needed. |
