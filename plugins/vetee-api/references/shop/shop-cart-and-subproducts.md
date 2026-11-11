# Shop cart records and subproducts

`UserShopItem` is a cart row linking `user`, `shopItem`, optional
`animal`, parent `userShopItem`, independent `quantity`, active state
and child `userShopItems`. Inspect with `getListUserShopItem` filtered to
the selected user and deleted/active state.

Product hierarchy and cart hierarchy differ:
`ShopItem.shopItem` says which product is a subproduct;
`UserShopItem.userShopItem` identifies the specific parent cart row.
A child must belong to the correct parent product/row. Do not infer its
quantity by multiplying parent quantity.

Product flags describe quantity support (`isStackable`), animal association
(`isForAnimal`) and consultation association (`isAnimalThread`). Inspect the
actual cart/order relations to determine which records are connected.

For a requested administrative correction, inspect the row, parent, product,
animal and live input first; do not use broad cart replacement. Generic record
edits are not a substitute for dedicated cart or purchase actions. Consumer
add/remove/checkout procedures are omitted.

See [Shop](../shop.md) and [order records](shop-checkout-and-mobile-payments.md).
