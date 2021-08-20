## GTFS-eligibilities


### Goals

Describes the limitations on types and groups of people who may book a trip or board a vehicle.

GTFS-eligibilities is formed around the concept that it should provide a manner for systems operating based on user accounts to understand whether a trip is eligible based on user account information. This means the fields proposed provide:

* Common attributes associated with user accounts such as age, gender, company affiliation, trip purposes, and assistance levels provided.
* Customizable authentications of locally-defined attributes and statuses. Custom eligibilities are provided, as well as a way to understand how the custom eligibility can be authenticated.

### Requirements

Extends **[GTFS-RiderCategories](https://docs.google.com/document/d/19j-f-wZ5C_kYXmkLBye1g42U-kvfSVgYLkkG5oyBauY/edit#heading=h.9gqyl4w7f6x1)**

### Files extended or added

<table>
  <tr>
   <td><strong>File Name</strong>
   </td>
   <td><strong>State</strong>
   </td>
   <td><strong>Defines</strong>
   </td>
  </tr>
  <tr>
   <td><code>routes.txt</code>
   </td>
   <td>Extended
   </td>
   <td>Adds reference to <code>rider_category_id</code>
   </td>
  </tr>
  <tr>
   <td><code>trips.txt</code>
   </td>
   <td>Extended
   </td>
   <td>Adds reference to <code>rider_category_id</code>, which overrides assignment on routes
   </td>
  </tr>
  <tr>
   <td><code>stop_times.txt</code>
   </td>
   <td>Extended
   </td>
   <td>Adds reference to <code>rider_category_id</code>, which overrides assignment on trips and routes
   </td>
  </tr>
  <tr>
   <td><code>rider_categories.txt</code>
   </td>
   <td>Extended
   </td>
   <td>Adds fields to define various eligibility restrictions
   </td>
  </tr>
  <tr>
   <td><code>urn_sets.txt</code>
   </td>
   <td>Created
   </td>
   <td>Adds ability for a rider category to reference URNs for purposes of describing allowed trip purposes, rider eligibility, and legal compliance
   </td>
  </tr>
  <tr>
   <td><code>urns.txt</code>
   </td>
   <td>Created
   </td>
   <td>Provides additional information related to Uniform Resource Names (URNs)
   </td>
  </tr>
</table>

### File Definitions

#### routes.txt (file extended)

<table>
  <tr>
   <td><strong>Field Name</strong>
   </td>
   <td><strong>Details</strong>
   </td>
  </tr>
  <tr>
   <td><code>rider_category_id</code>
   </td>
   <td>(ID, <strong>Optional</strong>) Identifies a rider category eligible for the route.
   </td>
  </tr>
</table>

#### trips.txt (file extended)

<table>
  <tr>
   <td><strong>Field Name</strong>
   </td>
   <td><strong>Details</strong>
   </td>
  </tr>
  <tr>
   <td><code>rider_category_id</code>
   </td>
   <td>(ID, <strong>Optional</strong>) Identifies a rider category eligible for the trip. Value overrides assignment on <code>routes.rider_category_id</code>.
   </td>
  </tr>
</table>

#### stop_times.txt (file extended)

<table>
  <tr>
   <td><strong>Field Name</strong>
   </td>
   <td><strong>Details</strong>
   </td>
  </tr>
  <tr>
   <td><code>rider_category_id</code>
   </td>
   <td>(ID, <strong>Optional</strong>) Identifies a rider category eligible for the stop_time. Value overrides assignment on <code>trips.rider_category_id</code> and <code>routes.rider_category_id</code>.
   </td>
  </tr>
</table>

#### rider_categories.txt (file extended)

<table>
  <tr>
   <td><strong>Field Name</strong>
   </td>
   <td><strong>Details</strong>
   </td>
  </tr>
  <tr>
   <td><code>rider_category \
_desc</code>
   </td>
   <td>(Text, <strong>Optional</strong>) Description of all elements of the rider category, including age, trip purpose, and other factors.
   </td>
  </tr>
  <tr>
   <td><code>trip_purpose</code>
   </td>
   <td>(Enum, <strong>Optional</strong>) Indicates a trip purpose eligible for this service, where the purpose describes the primary activity at the destination the rider is going to or returning from.
<p>
0 or blank - All rider purposes are allowed on this service.
<p>
1 - This service is for riders needing transportation for medical purposes
<p>
2 - This service is for riders needing transportation for shopping purposes
<p>
3 - This service is for riders needing transportation for educational purposes
<p>
4 - This service is for riders needing transportation for work purposes
   </td>
  </tr>
  <tr>
   <td><code>trip_purpose_ urn_set_id</code>
   </td>
   <td>(ID referencing <code>urn_sets.urn_set_id</code>, <strong>Optional</strong>) URN set referencing one or more URNs describing allowed trip purposes. If more than one trip purpose URN is provided in the set, a qualifying rider trip must match any one or more of the listed trip purposes.
   </td>
  </tr>
  <tr>
   <td><code>eligibility</code>
   </td>
   <td>(Enum, <strong>Optional</strong>) Indicates an eligibility constraint that limits access to this service (in addition to the age range, if specified) 
<p>
0 or blank - All riders are allowed on this service.
<p>
1 - This service is limited to riders with disabilities
<p>
2 - This service is limited to riders based on other criteria
   </td>
  </tr>
  <tr>
   <td><code>eligibility_ urn_set_id</code>
   </td>
   <td>(ID referencing <code>urn_sets.urn_set_id</code>, <strong>Optional</strong>) URN set referencing one or more URNs providing detailed identifiers for eligibility. If more than one URN is provided in the set, the rider must be eligible for all factors described by the entire set of URNs.
   </td>
  </tr>
  <tr>
   <td><code>eligibility_ authentication</code>
   </td>
   <td>(Enum, <strong>Optional</strong>) Indicates the manner in which qualification for eligibility will be determined.
<p>
0 or blank - Eligibility is authenticated onboard at no particular time.
<p>
1 - Eligibility is authenticated at time of boarding.
<p>
2 - Eligibility is authenticated at time of booking.
   </td>
  </tr>
  <tr>
   <td><code>registration_ desc</code>
   </td>
   <td>(Text, <strong>Optional</strong>) Description of how a rider may establish eligibility for the service.
   </td>
  </tr>
  <tr>
   <td><code>registration_ url</code>
   </td>
   <td>(Text, <strong>Optional</strong>) URL where a rider may register to establish eligibility for the service.
   </td>
  </tr>
  <tr>
   <td><code>registration_ phone</code>
   </td>
   <td>(Text, <strong>Optional</strong>) Phone number where a rider may register to establish eligibility for the service.
   </td>
  </tr>
  <tr>
   <td><code>appeal_url</code>
   </td>
   <td>(Text, <strong>Optional</strong>) URL where a rider may appeal a determination regarding this eligibility.
   </td>
  </tr>
  <tr>
   <td><code>appeal_phone</code>
   </td>
   <td>(Text, <strong>Optional</strong>) Phone number where a rider may appeal a determination regarding this eligibility.
   </td>
  </tr>
  <tr>
   <td><code>compliance_urn _set_id</code>
   </td>
   <td>(ID referencing <code>urn_sets.urn_set_id</code>, <strong>Optional</strong>) URN set referencing one or more URNs providing detailed identifiers for laws or regulations the eligibility is intended to comply with. If more than one URN is provided in the set, the eligibility must comply with all laws or regulations identified by the URNs.
   </td>
  </tr>
</table>

#### urn_sets.txt (optional file, added)

<table>
  <tr>
   <td><strong>Field Name</strong>
   </td>
   <td><strong>Details</strong>
   </td>
  </tr>
  <tr>
   <td><code>urn_set_id</code>
   </td>
   <td>(ID, <strong>Required</strong>) Identifies a set of URNs to be used together. Multiple entries in <code>urn_sets.txt</code> may share the same <code>urn_set_id</code>.
   </td>
  </tr>
  <tr>
   <td><code>urn</code>
   </td>
   <td>(URN,  <strong>Required</strong>) A single uniform resource name.
   </td>
  </tr>
  <tr>
   <td><code>reverse_test</code>
   </td>
   <td>(Enum, <strong>Optional</strong>) If the URN is being used in a true/false test for equality, indicates that the result of the test should be reversed (the same as using a “not” operator).
<p>
0 or blank - Result of test is not reversed (true returns true, false returns false)
<p>
1 - Result of test is reversed (true returns false, false returns true)
   </td>
  </tr>
</table>

#### urns.txt (optional file, added)

<table>
  <tr>
   <td><strong>Field Name</strong>
   </td>
   <td><strong>Details</strong>
   </td>
  </tr>
  <tr>
   <td><code>urn</code>
   </td>
   <td>(URN referencing <code>urn_sets.urn</code>, <strong>Required</strong>) A single uniform resource name.
   </td>
  </tr>
  <tr>
   <td><code>urn_name</code>
   </td>
   <td>(Text, <strong>Optional</strong>) A short name corresponding to a URN that may be displayed to the rider. 
   </td>
  </tr>
  <tr>
   <td><code>urn_desc</code>
   </td>
   <td>(Text, <strong>Optional</strong>) A more detailed description corresponding to a URN.
   </td>
  </tr>
  <tr>
   <td><code>urn_url</code>
   </td>
   <td>(URL, <strong>Optional</strong>) URL for more detailed information corresponding to a URN.
   </td>
  </tr>
</table>
