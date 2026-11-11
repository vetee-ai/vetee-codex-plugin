# Shop

Shop catalog, carts and purchases are separate models from membership UserOrder.

| Model | Meaning |
| --- | --- |
| `ShopItemCategory` | Translated category tree and targeting. |
| `ShopItem` | Product or subproduct, fulfillment flags, text/media and targeting. |
| `ShopItemCurrency`, `ShopItemDiscount` | Currency prices and optional tariff discounts. |
| `UserShopItem` | User cart row, optional animal and parent row. |
| `UserShopOrder` | Purchase with currency, status, delivery/contact/billing snapshots. |
| `UserShopOrderShopItem` | Purchased row with saved unit price, quantity and fulfillment state. |
| `ShopPlaceCategory`, `ShopPlace` | Pickup/submission location catalog. |
| `ShopDelivery`, `ShopDeliveryCurrency` | Delivery methods and per-currency delivery prices. |

- [Catalog and filters](shop/shop-catalog-and-filters.md)
- [Prices and discounts](shop/shop-prices-and-discounts.md)
- [Cart records and subproducts](shop/shop-cart-and-subproducts.md)
- [Order/payment and delivery records](shop/shop-checkout-and-mobile-payments.md)
- [Order fulfillment and consultations](shop/shop-orders-and-consultation-workflow.md)

These references cover administrative data, delivery/place configuration,
tracking and available invoice/receipt fields. Mobile checkout instructions
and internal processing details are omitted. See [shared conventions](reference-data/filters-and-translations.md).
