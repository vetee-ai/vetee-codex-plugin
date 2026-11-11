# Shop prices and discounts

`ShopItemCurrency` links product/currency with `isActive` and `value`;
the product/currency pair is unique. Prices are **major currency units**.
Zero is free; a missing currency row is unavailable, not free.

`ShopItemDiscount` links product and optional `offerTariff`, with
`isActive`, `publicFrom/Till`, `isFixedAmount`, `value`.
A fixed value subtracts that number of selected-currency major units; the
discount has no separate currency. A percentage value is 0–100.
Read through the product or `getListShopItemCurrency` /
`getListShopItemDiscount`, narrowed by product/currency/tariff.

For a price audit, inspect the product's currency rows and discount records,
including active/deleted state, validity and optional tariff relation. A list
of configured discounts is not a computed customer price. Use values returned
by the appropriate API operation; do not reconstruct pricing rules from the
configuration or assume that discounts combine.

Historical `UserShopOrderShopItem.value` is the saved discounted unit price.
Interpret it with that row's quantity and order currency. Keep parent and child
quantities separate, and include `deliveryValue` when inspecting order totals.
Do not recalculate historical orders using today's catalog.

Requested price/discount edits use their own row IDs and direct scalar update
values. They affect future calculation, not proof of payment or old snapshots.
See [Shop](../shop.md).
