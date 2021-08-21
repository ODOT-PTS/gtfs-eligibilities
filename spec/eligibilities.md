# GTFS-eligibilities


## Goals

Describes the limitations on types and groups of people who may book a trip or board a vehicle.

GTFS-eligibilities is formed around the concept that it should provide a manner for systems operating based on user accounts to understand whether a trip is eligible based on user account information. This means the fields proposed provide:

* Common attributes associated with user accounts such as age, gender, company affiliation, trip purposes, and assistance levels provided.
* Customizable authentications of locally-defined attributes and statuses. Custom eligibilities are provided, as well as a way to understand how the custom eligibility can be authenticated.

## Requirements

Extends **[GTFS-RiderCategories](https://docs.google.com/document/d/19j-f-wZ5C_kYXmkLBye1g42U-kvfSVgYLkkG5oyBauY/edit#heading=h.9gqyl4w7f6x1)**

## Files extended or added

|File Name|State|Defines|
| --- | --- | --- |
|`routes.txt`|Extended|Adds reference to `rider_category_id`|
|`trips.txt`|Extended|Adds reference to `rider_category_id`, which overrides assignment on routes|
|`stop_times.txt`|Extended|Adds reference to `rider_category_id`, which overrides assignment on trips and routes|
|`rider_categories.txt`|Extended|Adds fields to define various eligibility restrictions|
|`urn_sets.txt`|Created|Adds ability for a rider category to reference URNs for purposes of describing allowed trip purposes, rider eligibility, and legal compliance|
|`urns.txt`|Created|Provides additional information related to Uniform Resource Names (URNs)|

## File Definitions

### routes.txt (file extended)

|Field Name|Details|
| --- | --- |
|`rider_category_id`|(ID, **Optional**) Identifies a rider category eligible for the route.|

### trips.txt (file extended)

|Field Name|Details|
| --- | --- |
|`rider_category_id`|(ID, **Optional**) Identifies a rider category eligible for the trip. Value overrides assignment on `routes.rider_category_id`.|

### stop_times.txt (file extended)

|Field Name|Details|
| --- | --- |
|`rider_category_id`|(ID, **Optional**) Identifies a rider category eligible for the stop_time. Value overrides assignment on `trips.rider_category_id` and `routes.rider_category_id`.|

### rider_categories.txt (file extended)

|Field Name|Details|
| --- | --- |
|`rider_category_desc`|(Text, **Optional**) Description of all elements of the rider category, including age, trip purpose, and other factors.|
|`trip_purpose`|(Enum, **Optional**) Indicates a trip purpose eligible for this service, where the purpose describes the primary activity at the destination the rider is going to or returning from.<br><br>`0` or blank - All rider purposes are allowed on this service.<br>`1` - This service is for riders needing transportation for **medical** purposes<br>`2` - This service is for riders needing transportation for **shopping** purposes<br>`3` - This service is for riders needing transportation for **educational** purposes<br>`4` - This service is for riders needing transportation for **work** purposes|
|`trip_purpose_urn_set_id`|(ID referencing `urn_sets.urn_set_id`, **Optional**) URN set referencing one or more URNs describing allowed trip purposes. If more than one trip purpose URN is provided in the set, a qualifying rider trip must match any one or more of the listed trip purposes.|
|`eligibility`|(Enum, **Optional**) Indicates an eligibility constraint that limits access to this service (in addition to the age range, if specified)<br><br>`0` or blank - All riders are allowed on this service.<br>`1` - This service is limited to riders with disabilities<br>`2` - This service is limited to riders based on other criteria|
|`eligibility_urn_set_id`|(ID referencing `urn_sets.urn_set_id`, **Optional**) URN set referencing one or more URNs providing detailed identifiers for eligibility. If more than one URN is provided in the set, the rider must be eligible for all factors described by the entire set of URNs.|
|`eligibility_authentication`|(Enum, **Optional**) Indicates the manner in which qualification for eligibility will be determined.<br><br>`0` or blank - Eligibility is authenticated onboard at no particular time.<br>`1` - Eligibility is authenticated at the time of boarding.<br>`2` - Eligibility is authenticated at the time of booking.|
|`registration_desc`|(Text, **Optional**) Description of how a rider may establish eligibility for the service.|
|`registration_url`|(Text, **Optional**) URL where a rider may register to establish eligibility for the service.|
|`registration_phone`|(Text, **Optional**) Phone number where a rider may register to establish eligibility for the service.|
|`appeal_url`|(Text, **Optional**) URL where a rider may appeal or learn how to appeal a determination regarding this eligibility.|
|`appeal_phone`|(Text, **Optional**) Phone number where a rider may appeal or learn how to appeal a determination regarding this eligibility.|
|`compliance_urn_set_id`|(ID referencing `urn_sets.urn_set_id`, **Optional**) URN set referencing one or more URNs providing detailed identifiers for laws or regulations the eligibility is intended to comply with. If more than one URN is provided in the set, the eligibility must comply with all laws or regulations identified by the URNs.|

### urn_sets.txt (optional file, added)

|Field Name|Details|
| --- | --- |
|`urn_set_id`|(ID, **Required**) Identifies a set of URNs to be used together. Multiple entries in `urn_sets.txt` may share the same `urn_set_id`.|
|`urn`|(URN,  **Required**) A single uniform resource name.|
|`reverse_test`|(Enum, **Optional**) If the URN is being used in a true/false test for equality, indicates that the result of the test should be reversed (the same as using a "not" operator).<br><br>`0` or blank - Result of test is not reversed (true returns true, false returns false)<br>`1` - Result of test is reversed (true returns false, false returns true)|


### urns.txt (optional file, added)

|Field Name|Details|
| --- | --- |
|`urn`|(URN referencing `urn_sets.urn`, **Required**) A uniform resource name.|
|`urn_name`|(Text, **Optional**) A short name corresponding to a URN that may be displayed to the rider.|
|`urn_desc`|(Text, **Optional**) A more detailed description corresponding to a URN.|
|`urn_url`|(URL, **Optional**) URL for more detailed information corresponding to a URN.|
