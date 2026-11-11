# Offers, orders and payments

These models describe membership/entitlement offers and billing. Shop purchases
use separate [shop order models](shop.md).

| Model | Administrative meaning |
| --- | --- |
| `Offer` | Visibility, sales availability, partner and strategy. |
| `OfferStripePrice` | Price assignment, optional coupon/tariff and trial configuration. |
| `StripePrice` | Price currency, amount, recurrence and entitlement limits. |
| `StripeCoupon` | Fixed or percentage billing discount. |
| `OfferVoucher` | Redeemable code, validity and optional originating order/contact data. |
| `UserOrder` | User entitlement/order linked to an offer-price assignment. |

- [Vouchers and offers](offers-orders-and-payments/vouchers-and-offers.md)
- [Orders and price assignments](offers-orders-and-payments/orders-and-checkout.md)
- [Payment inspection, cancellation and refunds](offers-orders-and-payments/payment-history-and-billing-portal.md)

Use model queries for a selected user's records, not customer checkout or
billing-portal flows. Never publish voucher values, contacts, payment IDs or
secrets in this repository.

See [shared conventions](reference-data/filters-and-translations.md).
