# Create an animal

Creation is a write and requires an explicit request for the target environment.
Inspect `Input_CreateData_Animal` and resolve species, breed, gender and file
IDs there before constructing `createOneAnimal`.

Before creating a customer-owned profile, confirm that the available operation
supports the requested ownership. Do not assume that supplying `ownerUser`
establishes that ownership. If the operation cannot meet the request, report
the limitation rather than creating a profile under another user or silently
reassigning it.

Names (`callName`, `givenName`, `kennelName`) are ordinary scalars.
Reference relations use connect inputs; Animal has no translated-name rows.
Birth, measurements and medications require their own event/attachment data,
not invented fields such as `birthDate` or `weight`.

Read back owner and memberships after an authorized creation. A lost response
requires inspection before retrying to avoid duplicate animals.
See [Animals](../animals.md) and [Events](animal-events.md).
