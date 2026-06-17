# Payments API Contract

Status: Active

Backend owner: Payments Platform Demo

Frontend usage:

- Checkout page submits a payment intent.
- Payment status component polls payment status until it becomes terminal.
- Retry button creates a brand new payment intent with the same checkout payload when the last payment is failed and retryable.

## Endpoint: POST /api/payments/intent

Creates a new payment intent for a checkout session.

### Request

Content-Type: `application/json`

```json
{
  "orderId": "ord_demo_1001",
  "amount": 4999,
  "currency": "USD",
  "paymentMethodToken": "pm_card_visa",
  "customer": {
    "email": "ada@example.com"
  }
}
```

### Request rules

- `orderId`: required string
- `amount`: required positive integer in minor units
- `currency`: required 3-letter uppercase ISO-style currency code
- `paymentMethodToken`: required string
- Demo-supported tokens:
  - `pm_card_visa`
  - `pm_card_chargeDeclined`
- `customer.email`: required string

### Success response

Status: `201 Created`

```json
{
  "paymentId": "pay_7f5f7df34c6d",
  "status": "processing",
  "clientSecret": "demo_secret_7f5f7df34c6d",
  "pollAfterMs": 1500
}
```

### Notes

- The frontend must treat `paymentId` as the handle for later status polling.
- The frontend must not assume success on the create response.
- The frontend must use `pollAfterMs` as the first suggested delay before checking status.

## Endpoint: GET /api/payments/{id}/status

Returns the latest state for an existing payment.

### Success response

Status: `200 OK`

```json
{
  "paymentId": "pay_7f5f7df34c6d",
  "orderId": "ord_demo_1001",
  "status": "succeeded",
  "amount": 4999,
  "currency": "USD",
  "retryable": false,
  "updatedAt": "2026-06-17T08:30:00.000Z",
  "failure": null
}
```

### Status values

- `processing`
- `succeeded`
- `failed`

### Failure shape

When `status` is `failed`, `failure` must be an object:

```json
{
  "code": "card_declined",
  "message": "The card was declined by the issuer."
}
```

When `status` is not `failed`, `failure` must be `null`.

### Retry behavior

- `retryable` is `true` only when `status` is `failed`.
- The frontend retry button must create a new payment by calling `POST /api/payments/intent`.
- No dedicated retry endpoint exists in this contract.

## Error response

All non-2xx responses use this shape:

```json
{
  "error": {
    "code": "validation_error",
    "message": "Validation failed.",
    "details": [
      {
        "field": "amount",
        "message": "Must be a positive integer in minor units."
      }
    ]
  }
}
```

### Error codes

- `validation_error`
- `invalid_json`
- `payment_not_found`
- `method_not_allowed`
- `not_found`

## Frontend usage summary

1. Call `POST /api/payments/intent`.
2. Show the returned `paymentId` and `status`.
3. Poll `GET /api/payments/{id}/status` until status is `succeeded` or `failed`.
4. If `failed` and `retryable` is `true`, show a retry button that creates a new payment intent with the same checkout payload.

## Live demo goal

Show that:

- frontend and backend can work from the same contract file
- AI can implement each side without cross-editing the other repo
- new backend needs can be proposed as RFCs before code changes happen
