### Goals

Describes the additional capabilities that a service may be able to provide to serve people with disabilities, those who have mobility devices, or 

GTFS-capabilities leverages and enhances pre-existing specification extensions to provide ways for trip planners and analysts to identify how many people could board a vehicle or book a trip. It is chiefly composed of three themes:



*   Vehicle information, described by the (further extended) [GTFS-VehicleCategories](https://docs.google.com/document/d/156RiBjI6FnWJvO8_XWX11Q9nLdOiBdS_rilA-oamlv8/edit#heading=h.tosuo6e9e0z7) specification. See also the [GTFS-seats](bit.ly/gtfs-seats) draft extension.
*   A focus on describing vehicle amenities related to mobility devices, and how boarding with those devices affects capacity for other riders and devices.
*   Flexible fleet capacity loads, which are related to vehicle capacity but affected by availabilities of drivers and dispatchers, as well as agency operational processes.


### Requirements

**GTFS-VehiclesCategories**. Capabilities also in part reference and extend concepts within **GTFS-RequestTrips** although those components are not required in order to leverage the extensions to **GTFS-vehicles.**


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
   <td>Add additional information about service level.
   </td>
  </tr>
  <tr>
   <td><code>trips.txt</code>
   </td>
   <td>Extended
   </td>
   <td>Add additional information about service level.
   </td>
  </tr>
  <tr>
   <td><code>vehicle_categories.txt</code>
   </td>
   <td>Extended
   </td>
   <td>Adds granularity (modifies current extension) for mobility device capacity.
   </td>
  </tr>
  <tr>
   <td><code>mobility_device_spaces.txt</code>
   </td>
   <td>Added
   </td>
   <td>Allows defining the different spaces available for mobility devices on a vehicle group
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
   <td><code>service_level</code>
   </td>
   <td>(Enum, <strong>Optional</strong>) Defines the level of service provided to riders by the driver or other staff when picking up or discharging riders.
<p>
0 or empty - Unknown
<p>
1 - Curb-to-curb (assistance at the vehicle only)
<p>
2 - Door-to-door (assistance provided to passenger between the vehicle and the door of their origin or destination)
<p>
3 - Door-through-door (assistance provided to passenger out of and into the rider’s origin or destination)
<p>
4 - Hand-to-hand (rider is assured continuous attendance)
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
   <td><code>service_level</code>
   </td>
   <td>(Enum, <strong>Optional</strong>) Defines the level of service provided to riders by the driver or other staff when picking up or discharging riders.
<p>
0 or empty - Unknown
<p>
1 - Curb-to-curb (assistance at the vehicle only)
<p>
2 - Door-to-door (assistance provided to passenger between the vehicle and the door of their origin or destination)
<p>
3 - Door-through-door (assistance provided to passenger out of and into the rider’s origin or destination)
<p>
4 - Hand-to-hand (rider is assured continuous attendance)
   </td>
  </tr>
</table>



#### vehicle_categories.txt (file extended)


<table>
  <tr>
   <td><strong>Field Name</strong>
   </td>
   <td><strong>Details</strong>
   </td>
  </tr>
  <tr>
   <td><code>Mobility_ device_space_ id</code>
   </td>
   <td>(ID, <strong>Optional</strong>) Identifies the mobility device space for the vehicle category.
   </td>
  </tr>
  <tr>
   <td><code>Has_seat_ \
belts</code>
   </td>
   <td>(Enum, <strong>Optional</strong>) Indicates the presence of seat belts on the vehicle.
<p>
0 or blank - There are no seat belts for passengers on the vehicle.
<p>
1 - Seat belts are available for seated passengers.
<p>
2 - Seat belts are present and must be worn if they are available for use.
   </td>
  </tr>
  <tr>
   <td><code>Stretcher_ capacity</code>
   </td>
   <td>(Non-negative integer, <strong>Optional</strong>) This number denotes the maximum number of riders in a stretcher that the vehicle can carry.
   </td>
  </tr>
  <tr>
   <td><code>vehicle_lift</code>
   </td>
   <td>(Enum, <strong>Optional</strong>) Indicates if a lift for wheelchair boarding is available in the vehicle.
<p>
0 or empty - Unknown
<p>
1 - Not available
<p>
2 - Available
   </td>
  </tr>
  <tr>
   <td><code>lift_capacity</code>
   </td>
   <td>(Non-negative integer, <strong>Optional</strong>) Mass that the lift is capable of raising and lowering, in kilograms.
   </td>
  </tr>
  <tr>
   <td><code>lift_width</code>
   </td>
   <td>(Non-negative integer, <strong>Optional</strong>) Width of lift, in centimeters.
   </td>
  </tr>
  <tr>
   <td><code>lift_length</code>
   </td>
   <td>(Non-negative integer, <strong>Optional</strong>) Length of lift, in centimeters.
   </td>
  </tr>
  <tr>
   <td><code>Vehicle_min_ aisles_width</code>
   </td>
   <td>(Non-negative integer, <strong>Optional</strong>) Minimal width of aisles, in centimeters.
   </td>
  </tr>
</table>



#### mobility_device_spaces.txt (file added)


<table>
  <tr>
   <td><strong>Field Name</strong>
   </td>
   <td><strong>Details</strong>
   </td>
  </tr>
  <tr>
   <td><code>Mobility_ device_ space_id</code>
   </td>
   <td>(ID, <strong>Required</strong>) Identifies a mobility device space. A mobility device space describes the space(s) onboard a vehicle where . An <code>mobility_device_id</code> can appear on multiple lines of <code>mobility_device_spaces.txt</code>, indicating that multiple distinct spaces are available, which may have different parameters.
   </td>
  </tr>
  <tr>
   <td><code>Securement_ method</code>
   </td>
   <td>(Enum, <strong>Optional</strong>) Indicates the method by which mobility devices are secured.
<p>
0 or blank - There is no equipment in this space to secure mobility devices.
<p>
1 - There is equipment in this space to secure a mobility device, which can be operated by the passenger.
<p>
2 - There is equipment in this space to secure a mobility device, which must be operated by the driver.
   </td>
  </tr>
  <tr>
   <td><code>Mobility_ device_ position</code>
   </td>
   <td>(Enum, <strong>Optional</strong>) Indicates the position within the vehicle where the mobility_space is located.
<p>
0 or blank - The mobility device space is near the front door.
<p>
1 - The mobility device space is near the rear door.
<p>
2 - The mobility device space is near the rear of the vehicle, accessed by a separate door or lift.
   </td>
  </tr>
  <tr>
   <td><code>width</code>
   </td>
   <td>(Non-negative integer, <strong>Optional</strong>) The number of centimeters of clearance along the width of the vehicle for this mobility device space.
   </td>
  </tr>
  <tr>
   <td><code>length</code>
   </td>
   <td>(Non-negative integer, <strong>Optional</strong>) The number of centimeters of clearance along the length of the vehicle for this mobility device space.
   </td>
  </tr>
  <tr>
   <td><code>capacity_effect</code>
   </td>
   <td>(Non-negative integer, <strong>Optional</strong>) The number of seats which cannot be occupied by a rider while this mobility device space is in use.
   </td>
  </tr>
</table>
