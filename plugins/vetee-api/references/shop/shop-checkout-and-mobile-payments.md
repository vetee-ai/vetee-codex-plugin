# Shop order, payment and delivery records

Read `getListUserShopOrder` / `getOneUserShopOrder`, filtering by selected
user/order/code. Inspect `currency`, `status`, `stripe_id`,
`deliveryValue`, `shopDelivery` and purchased rows. Do not expose payment
secrets. Order states are `pendingPayment`, `processing`, `shipped`,
`completed`; there is no `paid` or `isActive` order state.

Saved billing/contact/address, fulfillment flags, delivery/submission place
selection and `note` describe the order snapshot. They are read-only in current
admin ACL even though generic order CRUD exists. Do not edit a user's current
address expecting an old order snapshot to change.

`invoiceUrl` and `receiptUrl` are computed fields; they may be absent.
Treat returned document links as sensitive and retrieve only when requested.
Total is saved item `value × quantity` for every row plus `deliveryValue`.
Catalog price changes do not rewrite the order.

For delivery configuration:
- `ShopItem` flags: `isDeliveryRequired`, `isSubmissionRequired`,
  `isContactRequired`, `isHomeDeliveryAllowed`; `shopPlaceFilters`
  constrain places.
- `ShopPlace` links its category/country/partner and holds location details.
- `ShopDelivery.type` is `home` or `place`; home cannot connect a pickup place.
- `ShopDeliveryCurrency` has active currency and nonnegative major-unit price
  validated against currency precision.

For payment questions use the order's returned payment information and the
available documented operations. A manually edited status is not proof of
payment; do not simulate a payment or invoice action by changing record fields.
Mobile checkout/payment instructions are omitted.
See [Shop](../shop.md) and [fulfillment](shop-orders-and-consultation-workflow.md).
