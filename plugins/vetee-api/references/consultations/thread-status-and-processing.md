# Thread status and processing

Read `status`, `type`, `veterinarian`, `veterinarianAcceptedAt`,
`summary`, messages and optional `userShopOrderShopItem`. Thread and message
status use different enums.

| Thread status | Diagnostic meaning |
| --- | --- |
| `pending` | Initial queue. |
| `rejectedCategory` | Intake failed category rules. |
| `llmProcessing` | Automated preparation running. |
| `pendingInformation` | Waiting for questionnaire data. |
| `pendingLlmQuickAdvice`, `llmQuickAdviceProcessing` | Quick-advice queue / generation. |
| `pendingPayment` | Waiting for payment. |
| `pendingShop` | Waiting for shop fulfillment/result. |
| `pendingVeterinarian` | Waiting for veterinary processing. |
| `veterinarianProcessing` | Accepted by a veterinarian. |
| `answered`, `rejected` | Answered / rejected. |

These are branches, not one universal sequence. For shop threads inspect the
linked order/item too. Compare assigned veterinarian and acceptance time;
changing only one can leave contradictory data.

Use `updateOneAnimalThread` only for explicitly requested record corrections.
For a business action, use its documented dedicated operation when available;
do not simulate it by changing status fields.
See [Consultations](../consultations.md) and
[shop fulfillment](../shop/shop-orders-and-consultation-workflow.md).
