# Vouchers and offers

Use `getListOffer` / `getOneOffer` and
`getListOfferVoucher` / `getOneOfferVoucher`.

`Offer` has `isActive`, `isPublic`, `isEnabledInApp`, `isEnabledInStart`,
`strategy` (`open`, `code`, `contact`), partner relations, translations,
`countryFilters`, `stripeCoupon` and `offerStripePrices`. These flags
answer different questions: an active offer need not be public or available
in every channel. Administrative listing alone does not establish customer
eligibility.

`OfferVoucher` holds `code`, `isActive`, `validFrom`, `validTill`,
`userOrder`, `contactEmail` and `contactPhone`. `userOrder` can identify
its originating purchase; it is not a generic proof of current redemption.
Filter by code using variables, active state and validity. Select contacts
only when necessary.

For requested edits target the model, translation or filter row. Inspect the
live OfferVoucher input before constructing relationships; do not invent an
`offer` field or assume generic creation supports it. Report an unavailable
capability.

Never copy offer secrets or actual voucher codes into examples.
See [overview](../offers-orders-and-payments.md) and
[shared conventions](../reference-data/filters-and-translations.md).
