# Facilities

`Facility` represents a clinic/service location. It links `facilityCategory`,
`country`, optional `region` and `ownerUser`, media, translations,
contacts, schedules, labels and targeting joins.

Base name/address fields coexist with translations. Latitude/longitude,
`isActive`, `isEmergency`, `isEmergencyByPhone`, `isNonstop` and
`order` are separate from localized text. A translated address does not
automatically update coordinates.

- [Create/configure a facility](facilities/create-and-list-a-veterinarian-facility.md)
- [List and filter facilities](facilities/list-facilities.md)
- [Geographic and opening filters](facilities/find-facilities-in-a-map-area.md)
- [Detail, contacts and schedules](facilities/get-a-facility.md)

Current opening data uses `facilitySchedules` and their ranges, not old
`openingHours` / `emergencyOpeningHours` fields. Admin reads do not apply
customer visibility automatically.

See [shared conventions](reference-data/filters-and-translations.md).
