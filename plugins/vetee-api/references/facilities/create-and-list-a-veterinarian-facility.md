# Create and configure a facility

For a requested creation inspect `Input_CreateData_Facility`, resolve
`facilityCategory` and `country`, and optional region/owner/media.
The category code `user-veterinarian` identifies a user veterinarian facility;
resolve its actual ID in the selected environment. Confirm any requested
owner relationship through the available API input.

For every facility update, read the current `isActive` value and explicitly
send the intended value along with the requested changes. Preserve the current
state unless activation/deactivation was requested, then verify it by query.

Names and addresses can exist on Facility and FacilityTranslation. Create or
update the intended language row; do not overwrite all languages. Manage
contacts, schedules, labels and locale/species/specialization targeting as
separate related data.

Use the generic create/update mutations only for requested changes. Saving a
facility does not geocode its address or establish the full schedule.
For inspection use [list](list-facilities.md) and [detail](get-a-facility.md).
See [Facilities](../facilities.md).
