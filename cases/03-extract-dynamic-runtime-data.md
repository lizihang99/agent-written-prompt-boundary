# Case 03 - Extract Dynamic Runtime Data

## Input Brief

"Generate a support reply. In this conversation we used the sample name Maya, sample order 18273, and a pasted ticket body. The real system will supply customer name, order id, ticket text, and refund eligibility at runtime."

## Expected Handling

- sample name, order id, ticket body -> `runtime-variable`
- refund eligibility supplied by the system -> `runtime-variable`
- politeness and brevity guidance -> `derived-runtime-rule`

## Common Failure

Sample values get baked into the stable prompt text.

Another failure: the prompt says to personalize with the customer name and then forbids using the name in the reply.

## Pass Criteria

The prompt contains placeholders or named inputs, not hard-coded ticket data, and instructions do not contradict variable usage.
