# GTFS-eligibilities

### Goals

Describes the limitations on types and groups of people who may book a trip or board a vehicle.

GTFS-eligibilities is formed around the concept that it should provide a manner for systems operating based on user accounts to understand whether a trip is eligible based on user account information. This means the fields proposed provide:



*   Common attributes associated with user accounts such as age, gender, company affiliation, trip purposes, and assistance levels provided.
*   Customizable authentications of locally-defined attributes and statuses. Custom eligibilities are provided, as well as a way to understand how the custom eligibility can be authenticated.


### Requirements

[None. Extends the core CSV GTFS.] 


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
   <td>Adds reference to <code>eligibility_id</code>
   </td>
  </tr>
  <tr>
   <td><code>trips.txt</code>
   </td>
   <td>Extended
   </td>
   <td>Adds reference to <code>eligibility_id</code>, which overrides assignment on routes
   </td>
  </tr>
  <tr>
   <td><code>stop_times.txt</code>
   </td>
   <td>Extended
   </td>
   <td>Adds reference to <code>eligibility_id</code>, which overrides assignment on trips and routes
   </td>
  </tr>
  <tr>
   <td><code>eligibilities.txt</code>
   </td>
   <td>Added
   </td>
   <td>Provides fields to define various eligibility restrictions.
   </td>
  </tr>
</table>



### 


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
   <td><code>eligibility_id</code>
   </td>
   <td>(ID, <strong>Optional</strong>) Identifies an eligibility restriction in effect for the route.
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
   <td><code>eligibility_id</code>
   </td>
   <td>(ID, <strong>Optional</strong>) Identifies an eligibility restriction in effect for the trip.
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
   <td><code>eligibility_id</code>
   </td>
   <td>(ID, <strong>Optional</strong>) Identifies an eligibility restriction in effect for the stop_time.
   </td>
  </tr>
</table>



#### eligibilities.txt (file added)


<table>
  <tr>
   <td><strong>Field Name</strong>
   </td>
   <td><strong>Details</strong>
   </td>
  </tr>
  <tr>
   <td><code>eligibility_id</code>
   </td>
   <td>(ID, <strong>Required</strong>) Identifies an eligibility restriction. An eligibility restriction describes a group of people who can ride a service. An <code>eligibility_id</code> can appear on multiple lines of <code>eligibilities.txt</code>, indicating that multiple groups of people are eligible for the service.
   </td>
  </tr>
  <tr>
   <td><code>eligibility_name</code>
   </td>
   <td>(Text, <strong>Optional</strong>) if an eligibility does not fit into one of the other eligibility.txt field descriptions, then the <code>custom_eligibility_name </code>field should provide a short (up to 25 characters) name describing the eligibility, for use in customer facing apps.
<p>
For example, if a service is for those registered in Medicaid, the <code>custom_eligibility_name</code> could be “Medicaid recipients”. A custom eligibility could also be a company affiliation, like “OSU community members” or “OSU employees”.
   </td>
  </tr>
  <tr>
   <td><code>eligibility_desc</code>
   </td>
   <td>(Text, <strong>Optional</strong>) Description of all elements of the eligibility restriction, including age, trip purpose, and other factors.
   </td>
  </tr>
  <tr>
   <td><code>min_age</code>
   </td>
   <td>(Non-negative integer, <strong>Optional</strong>) Indicates all riders this age or older are eligible.
   </td>
  </tr>
  <tr>
   <td><code>max_age</code>
   </td>
   <td>(Non-negative integer, <strong>Optional</strong>) Indicates all riders this age or younger are eligible.
   </td>
  </tr>
  <tr>
   <td><code>trip_purpose</code>
   </td>
   <td>(Enum, <strong>Optional</strong>) Indicates a rider purpose eligible for this service.
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
   <td><code>trip_purpose_urns</code>
   </td>
   <td>(Text, <strong>Optional</strong>) Uniform Resource Names (URNs) providing detailed identifiers for trip purposes. URNs must be separated by one or more spaces or newline characters. If more than one URN is provided, any is allowed for a given trip.
<p>
Examples: 
<p>
urn:gtfs:trip-purpose:us:federal:va:vts:medical
<p>
urn:gtfs:trip-purpose:us:federal:medicaid:state:oregon:medical
<p>
urn:gtfs:trip-purpose:us:state:oregon:org:ride.connection:recreation
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
   <td><code>eligibility_urns</code>
   </td>
   <td>(Text, <strong>Optional</strong>) One or more uniform resource names (URNs) providing detailed identifiers for eligibility. URNs must be separated by one or more spaces or newline characters. If more than one URN is provided, the rider must be eligible for each and every factor described by the URNs.
<p>
Examples:
<p>
urn:gtfs:eligibility:us:va:veteran
<p>
urn:gtfs:eligibility:us;oregon:odva:veteran
<p>
urn:gtfs:eligibility:us;oregon;org:ride.connection:veteran
<p>
urn:gtfs:eligibility:us;oregon;multnomah.county:ads:case-managed
<p>
urn:gtfs:eligibility:us;oregon;lane.transit.district:low-income
   </td>
  </tr>
  <tr>
   <td><code>eligibility_authentication</code>
   </td>
   <td>(Enum, <strong>Optional</strong>) Indicates the manner in which qualification for eligibility will be determined.
<p>
0 - Eligibility is authenticated onboard at no particular time.
<p>
1 or blank - Eligibility is authenticated at time of boarding.
<p>
2 - Eligibility is authenticated online via an <code>authentication_url</code>
<p>
3 - Eligibility is authenticated at time of booking, without an <code>authentication_url</code>
   </td>
  </tr>
  <tr>
   <td><code>registration_url</code>
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
   <td><code>authentication_param_name</code>
   </td>
   <td>(Text, <strong>Conditionally required</strong>) The name of the parameter that a value can be passed to through the <code>authentication_url</code> in order to authenticate a particular user during the online booking process.  
<ul>

<li><strong>Required</strong>, if the eligibility has an <code>authentication_url</code>

<li><strong>Forbidden</strong> otherwise
</li>
</ul>
   </td>
  </tr>
  <tr>
   <td><code>authentication_url</code>
   </td>
   <td>(Text, <strong>Conditionally required</strong>) The url that can be utilized in order to authenticate a particular user during the online booking process, along with an <code>authentication_param_name</code>.  
<ul>

<li><strong>Required</strong>, if the eligibility has an <code>authentication_param_name</code>

<li><strong>Forbidden</strong> otherwise
</li>
</ul>
   </td>
  </tr>
  <tr>
   <td><code>compliance_urns</code>
   </td>
   <td>(Text, <strong>Optional</strong>) One or more uniform resource names (URNs) providing detailed identifiers for laws the eligibility is intended to fulfill. URNs must be separated by one or more spaces or newline characters. If more than one URN is provided, the eligibility fulfill must be eligible for each and every URNs. 
<p>
Examples:
<p>
urn:gtfs:compliance:us:1990-07-26;ada
<p>
urn:gtfs:compliance:us;oregon;oregon.city:ordinance:2020-06-15;13.30.070
   </td>
  </tr>
</table>


