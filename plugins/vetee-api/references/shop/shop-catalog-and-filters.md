# Shop catalog and filters

Use `getListShopItemCategory` / `getOneShopItemCategory` and
`getListShopItem` / `getOneShopItem`.

Categories form a tree: `shopItemCategory` is the parent and
`shopItemCategories` direct children. Products use singular `shopItem`
for a parent and plural `shopItems` for subproducts. Filter a null parent
for roots. Primary category is `ShopItem.shopItemCategory`; additional
membership is `ShopItemCategoryShopItem` / `shopItemCategoryShopItems`.

```graphql
query InspectProducts($filter: Input_Filter_ShopItem, $pagination: Input_Pagination) {
  getListShopItem(filter: $filter, order: {order: asc, code: asc}, pagination: $pagination) {
    status { success errorCode errorMessage }
    meta { limit offset total }
    nodes {
      id code isActive deletedAt isStackable isForAnimal isAnimalThread
      shopItem { id }
      shopItemCategory { id code }
      translations { id name description content locale { id code } }
      shopItemCurrencies { id isActive value currency { id code } }
    }
  }
}
```

Both categories and products have locale/country/gender/species targeting
joins with `isActive`. To match a configured species use
`animalSpeciesFilters: {some: {isActive: {equals: true},
animalSpecies: {code: {in: ["dog"]}}}}`.
An empty collection does not match `some`. Admin does not automatically
infer a customer's targeting or exclude inactive/deleted products.

Search `code` or `translations.some.nameUnaccent` using normalized text
and insensitive mode. Restrict translation locale inside `some` if needed.
For category membership combine primary-category and active additional join
predicates with `OR`.

Translations hold name/description and product body; targeting is separate.
`ShopItemFile` adds file, order, active/premium settings; ShopItemLabel links
labels. `orderPrice` and `soldCount` are read-only catalog fields, not writable
currency prices. See [Shop](../shop.md) and
[shared conventions](../reference-data/filters-and-translations.md).
