# ai-contracts-demo

This repository is the shared contract layer for the demo.

It exists to answer one question in a live demo:

How can frontend and backend teams coordinate through AI without editing each other's codebases directly?

## Structure

- `contracts/`: source-of-truth API contracts
- `requests/frontend-to-backend/`: RFCs written by frontend for new backend needs

## Demo flow

1. Frontend reads `contracts/api/payments.md` and implements a checkout UI without inventing endpoints.
2. Backend reads the same contract and implements the API without changing the response shape.
3. Frontend later needs a new capability and writes an RFC instead of touching backend code.

## Suggested prompts

Frontend prompt:

```text
Read ai-contracts/contracts/api/payments.md.
Create the frontend payment client and checkout UI based only on this contract.
Do not invent endpoints.
```

Backend prompt:

```text
Read ai-contracts/contracts/api/payments.md.
Implement the backend endpoint exactly according to this contract.
Do not change the response shape unless you update the contract first.
```
