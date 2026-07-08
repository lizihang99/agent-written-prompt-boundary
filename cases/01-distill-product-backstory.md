# Case 01 - Distill Product Backstory

## Input Brief

"This feature is for beginner creators who feel intimidated by professional critique. The model should summarize their draft and suggest next steps. Do not paste our internal product pitch into the prompt. Use the user's draft text at runtime."

## Expected Handling

- "beginner creators who feel intimidated" -> `design-context`
- "warm, concrete, non-jargony tone" -> `derived-runtime-rule`
- user's draft text -> `runtime-variable`
- the internal product pitch -> `exclude` or remain outside runtime artifacts
- output shape -> `not specified`; do not invent JSON or parser requirements unless explicitly marked as an assumption

## Common Failure

The runtime prompt repeats the product backstory almost verbatim.

Another failure: the result fabricates a downstream JSON contract when the brief only asks for summary and next steps.

## Pass Criteria

The final prompt contains distilled behavior rules, not company narrative, and does not invent an output schema as if it were required.
