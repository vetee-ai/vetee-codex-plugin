# Facility detail, contacts and schedules

Read `getOneFacility(filter: {id: $id})`. Include base and translated
name/description/address, category/country/region, coordinates, flags,
contacts, schedules and only relevant targeting/labels.

`FacilityTranslation` links object/locale with name, description and address
fields. Base and translated values can differ; compare before a requested edit.

`FacilityContact` links facility with `type`, `name`, `value`,
`isActive`, `isPrimary`, `priority`, and translations of name/value.
Current admin ACL has no root query right for FacilityContact; read through
`Facility.facilityContacts`. Root mutations may be available. Do not invent
`getListFacilityContact` or assume unlisted fields are exposed.

`FacilitySchedule` holds `isActive`, `validFrom`, `validTill`,
`isEmergency`, `isEmergencyByPhone`, `daysOfWeek`, `note`, and
`facilityScheduleRanges`.
`FacilityScheduleRange` contains `openFrom` / `openTill` strings,
`isActive` and note. Inspect live weekday representation and preserve time
format; ranges are not full DateTime values.

For requested schedule/contact edits, target existing child IDs and preserve
unrelated ranges/translations. Follow the
[facility update instructions](create-and-list-a-veterinarian-facility.md),
including explicitly preserving the intended active state.
See [Facilities](../facilities.md).
