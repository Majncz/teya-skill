# Cancel a payment request

There are two main ways for a payment request to be cancelled. Either via the ePOS or the terminal depending on the point within the transaction.

Given a payment request has been posted to POSLink and a card has not yet been presented to the terminal for payment, it is possible to cancel via ePOS. However, if the user has started the payment process by presenting their card to the terminal, an attempt to cancel this payment can only be made from the terminal.

## Cancelling via ePOS

To cancel a payment request from ePOS:

1. ePOS calls POSLink's **Update a Payment Request API** submitting a status of `CANCELLING`.
2. Once the ePOS receives a successful response from POSLink, ePOS should continue to poll the Retrieve a payment request API to confirm the outcome of the request to cancel and final state of the transaction. These final states can either be `CANCELLED`, `SUCCESSFUL` or `FAILED`. Should the state be `CANCELLED`, the payment request can be considered cancelled.

### Example request

```http
PATCH /poslink/v2/payment-requests/{payment-request-id} HTTP/1.1
Content-Type: application/json
Authorization: Bearer <token>
Host: api.teya.com

{
  "status": "CANCELLING"
}
```

### Example response

```json
{
  "payment_request_id": "368dc71b-e9d4-4f30-a94c-0432e30043b6",
  "status": "CANCELLING",
  "updated_at": "2023-03-02T14:39:29.151Z"
}
```

## Cancelling via the terminal

Terminal will post a cancel request to the terminal Integration API which will be passed to ePOS.

1. The terminal will call the terminal Integration API to send cancel request.
2. If the terminal receives a successful response to the API call, it is considered that the transaction request has been cancelled.
3. The ePOS should reflect the cancelled state upon calling POSLink.

## Status flow diagrams

### Payment request status flow

The payment request can transition through the following states:

- **NEW** → Initial state when payment request is created
- **IN_PROGRESS** → Terminal has received and is processing the request
- **CANCELLING** → Cancellation has been requested
- **CANCELLED** → Payment was successfully cancelled
- **SUCCESSFUL** → Payment completed successfully
- **FAILED** → Payment failed
