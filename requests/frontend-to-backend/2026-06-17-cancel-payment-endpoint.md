# RFC: Cancel Payment Endpoint

Status: Proposed

Author: Frontend Demo Team

Created: 2026-06-17

## Problem

The checkout UI needs a way to let users cancel a payment that is still in `processing`.

Today the shared contract supports:

- `POST /api/payments/intent`
- `GET /api/payments/{id}/status`

There is no contract-approved way to cancel an in-flight payment.

## User impact

- Users cannot stop a payment attempt after submission.
- The UI must wait for the payment to become terminal even when the user changes their mind.

## Proposed change

Add a new endpoint to the shared contract:

`POST /api/payments/{id}/cancel`

## Proposed request

```json
{
  "reason": "user_requested"
}
```

## Proposed success response

```json
{
  "paymentId": "pay_7f5f7df34c6d",
  "status": "cancelled",
  "updatedAt": "2026-06-17T09:00:00.000Z"
}
```

## Proposed error cases

- payment already terminal
- payment not found
- invalid cancellation reason

## Rollout note

This RFC does not modify backend code. The next step is backend review and, if accepted, a contract update in `contracts/api/payments.md` before implementation work begins.
