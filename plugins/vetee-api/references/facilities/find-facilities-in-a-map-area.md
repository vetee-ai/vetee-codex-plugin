# Geographic and opening filters

`getListFacility` exposes additional arguments alongside its model filter:

| Argument | Fields / units |
| --- | --- |
| `filterGpsRectangle` | `centerLatitude`, `centerLongitude`, `cornerLatitude`, `cornerLongitude`. |
| `filterGpsDistance` | Center latitude/longitude and `distance` in **meters**. |
| `sortByDistance` | Center latitude/longitude for nearest-first sorting. |
| `filterIsOpen` | Boolean opening-state filter evaluated by the server. |

These are root list arguments, not fields inside `Input_Filter_Facility`.
Use a geographic predicate to bound the search; distance sorting alone is not
a radius filter. Return coordinates and the computed `distance` when
supported. Missing coordinates should not be interpreted as zero.

For an opening-state discrepancy, inspect base nonstop/emergency flags and
active schedules, validity, weekdays and time ranges. `filterIsOpen` uses
server-side schedule logic; don't derive it from a translated text description.

Combine geographic arguments with explicit admin active/deleted/category
filters as required. Inspect pagination/meta rather than assuming all matching
locations fit one page.
See [Facilities](../facilities.md) and [schedules](get-a-facility.md).
