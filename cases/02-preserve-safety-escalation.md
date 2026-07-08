# Case 02 - Preserve Safety And Escalation

## Input Brief

"Build a legal-risk triage prompt. The assistant must not tell users they are legally safe. If facts are incomplete, it should say so. If the message suggests immediate harm or a filing deadline, escalate. Downstream code expects a JSON object with `risk_level`, `reasoning`, and `escalate`."

## Expected Handling

- no legal reassurance -> `derived-runtime-rule`
- explicit uncertainty when facts are incomplete -> `derived-runtime-rule`
- escalation trigger -> `derived-runtime-rule`
- `risk_level`, `reasoning`, `escalate` -> `output-contract`
- any extra legal policy trigger not in the brief -> proposed assumption, not silent runtime contract
- extra output fields or risk enum values -> proposed assumption, not part of required contract

## Common Failure

Safety rules get shortened into vague tone language or dropped because they are rare edge conditions.

Another failure: the result invents extra legal escalation policy and presents it as required.

Another failure: the result adds fields such as `missing_facts` or enum values such as `critical` even though downstream code only expects `risk_level`, `reasoning`, and `escalate`.

Another failure: the result labels a risk enum as "proposed" but still puts it in the formal runtime output contract.

Another failure: examples or trigger lists broaden "immediate harm or filing deadline" into extra escalation policy such as active proceedings, enforcement actions, or generic urgency.

Another failure: the result treats `risk_level` as evidence for a `low | medium | high` enum. A common convention is not downstream evidence.

## Pass Criteria

Safety and escalation behavior remain explicit after prompt slimming, without silently expanding domain policy or output schema beyond the brief, and proposed schema assumptions stay outside the formal contract.
