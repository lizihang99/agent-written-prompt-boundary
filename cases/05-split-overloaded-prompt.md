# Case 05 - Split Overloaded Prompt

## Input Brief

"One prompt should classify the complaint, summarize the account history, decide whether a refund is allowed, and draft the final customer email."

## Expected Handling

- the boundary summary flags multiple incompatible jobs
- the result recommends split or staged calls instead of stuffing all behaviors into one prompt
- refund-policy inputs and account history remain structured inputs, not narrative instructions

## Common Failure

The workflow keeps adding rules to one giant prompt rather than separating judgment, transformation, and generation steps.

## Pass Criteria

The result proposes a cleaner boundary, such as classify -> decide -> draft, with each step owning one job.
