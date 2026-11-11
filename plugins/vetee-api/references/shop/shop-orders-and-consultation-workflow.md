# Shop order fulfillment and consultations

`UserShopOrderShopItem` stores purchased product, order, animal, optional
parent row/thread, `quantity`, saved unit `value` and nullable fulfillment
`status`. Read-only integration identifiers, when exposed, should be returned
only when relevant to the requested lookup.
Read parent/child rows without double counting quantities.

Item statuses are `pending`, `processing`, `examinationKitPreparing`,
`examinationKitShipped`, `examinationAwaitingCollection`,
`examinationAwaitingDropoff`, `examinationInLab`, `examinationTested`,
`done`. Item and overall order status are separate; null item status is not
the same as pending.

Inspect the row's `animalThread` relation when diagnosing an associated
consultation. Read the actual thread type/status instead of inferring it from
quantity or item status.

For explicitly requested record corrections, use `updateOneUserShopOrder`
for supported order fields and `updateOneUserShopOrderShopItem` for supported
item fields. Do not simulate payment or fulfillment actions through generic
status edits; use a documented dedicated operation when available. Verify the
item and linked thread after a requested correction.

Tracking code is limited to 255 characters; URL to 2048 with HTTP(S) and no URL
credentials.

See [Shop](../shop.md), [payment records](shop-checkout-and-mobile-payments.md)
and [thread status](../consultations/thread-status-and-processing.md).
