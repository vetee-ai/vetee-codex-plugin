# Payment inspection, cancellation and refunds

Start with query-only UserOrder reads filtered to the selected user/order.
App payment-history and billing-portal operations are current-user operations,
not an arbitrary-user admin ledger.

`getUserOrderStripeInfo(data: {orderId: ...})` is a **GraphQL mutation**
despite its read-like name. The default query-only rule forbids it until the
user explicitly requests that mutation. It returns `status`, order ID,
subscription/cancellation state, validity, `currentPeriodEnd`, currency,
total/refunded/refundable amounts and refund capability flags. Stripe amounts
are minor units; do not confuse them with shop major-unit prices.

For an explicitly requested cancellation/refund, introspect
`cancelUserOrderStripe` / `Input_Custom_CancelUserOrderStripeData`:

- `orderId`: resolved UserOrder ID.
- `cancellationType`: `END_OF_PERIOD` (subscription only), `NOW`, `AT_DATE`.
- `cancelAt`: required for `AT_DATE`.
- `refundType`: `NONE`, `FULL`, `PRORATED`.
  End-of-period cancellation requires `NONE`.

This operation cancels/schedules cancellation and may issue the requested
refund. It has financial effects; keep parameters within the user's request.
Check `status`, `validTill`, `isCanceled`, `refundedAmount`, `currency`
and verify the order. A lost response may follow external side effects:
inspect before retrying.

See [overview](../offers-orders-and-payments.md).
