# Orders and price assignments

Read `UserOrder` through `getListUserOrder` / `getOneUserOrder`.
Filter `user: {id: {equals: $userId}}`. Inspect `isActive`, `isCanceled`,
`validFrom`, `validTill`, `messageLimit` and `offerStripePrice` before
diagnosing access. Cancellation and remaining validity are separate facts.

`OfferStripePrice` links `offer`, `stripePrice`, optional `stripeCoupon`
and `offerTariff`, with `isActive`, `category`
(`default` / `onboardingPromo`), `isTrial`, `trialUnit`, `trialValue`.
Current admin ACL has no root query right for it. Read
`Offer.offerStripePrices` or `UserOrder.offerStripePrice`;
do not invent `getListOfferStripePrice`.

`StripePrice` has `currency`, `value`, `isRecurring`,
`recurrenceUnit/Value`, `validityUnit/Value`, `messageLimit`,
`isPerAnimalThreadMessage`, `offerTariff` and translations. Amount, currency
and recurrence are creation-only in the current admin contract; introspect
before proposing updates. StripePrice has no delete operation.

`StripeCoupon` represents fixed/percentage and recurring discounts; fixed
amounts require currency. Billing configuration writes can affect external
billing, so perform only the concrete requested change and inspect current
records before retrying a write.

UserOrder has read/update/delete rights but no generic create right in current
admin ACL. Editing `isCanceled` or validity directly does not cancel Stripe
billing or refund a payment. Use the
[dedicated operation](payment-history-and-billing-portal.md) on explicit request.
See [overview](../offers-orders-and-payments.md).
