# Delete an animal

Only delete an identified animal when explicitly requested. First read its
owner, names and deleted state to confirm the target. Use
`deleteOneAnimal(filter: {id: $animalId})` only after checking its live contract.

The generic delete implementation sets `deletedAt`; it does not physically
delete the database row or guarantee soft deletion of its events, files and
memberships. Customer visibility and admin visibility differ, so an admin
query may still return the deleted animal.

Verify `deletedAt` using a query. Do not cascade additional deletions merely
because related records remain. Restoration, where the update input permits
clearing `deletedAt`, is a separate requested change and requires checking
related access/data.

App owner-only rules should not be mistaken for admin ACL scope.
See [Animals](../animals.md) and
[deletion conventions](../reference-data/filters-and-translations.md).
