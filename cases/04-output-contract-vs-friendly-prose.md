# Case 04 - Output Contract Beats Friendly Prose

## Input Brief

"The frontend wants a friendly explanation, but the parser needs strict JSON with `summary`, `action_items`, and `confidence`. The product manager keeps asking for 'natural language output.'"

## Expected Handling

- strict JSON shape -> `output-contract`
- friendly wording inside field values -> `derived-runtime-rule`
- no prose outside the JSON envelope unless the caller explicitly accepts mixed output

## Common Failure

The prompt asks for both free-form prose and strict machine parsing in the same output channel.

## Pass Criteria

The output contract stays machine-safe while the content inside fields can still sound human.
