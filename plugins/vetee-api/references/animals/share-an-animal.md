# Animal membership and sharing data

`Animal.ownerUser` is the profile owner relation. `AnimalUser` separately
links `animal`, optional `user` and a `role`: `owner`, `editor`,
`viewer`. Inspect both when diagnosing access; a membership row can have no
connected user and does not prove a completed user association.

Read `Animal.animalUsers {id role user {id}}` or query AnimalUser with a narrow
animal/user filter. Include deleted-state checks when determining live access.
Use only fields exposed by the authenticated schema; do not assume sharing
codes are available through administrative reads.

For explicitly requested membership edits, identify the exact row and user,
then use the available generic mutation. Changing `ownerUser` alone does
not maintain all membership roles; ownership and joins must remain consistent.
Do not silently transfer ownership when fixing a display name.

Invitation/code acceptance and customer sharing workflows are omitted.
See [Animals](../animals.md).
