# Use of URNs

Uniform Resource Names (URNs) are identifiers that are globally unique, human-readable, and follow a consistent syntax so as to be easily human-generated. URNs are described in [RFC 8141](https://www.ietf.org/rfc/rfc8141.html).

Global uniqueness is achieved through a series of nested namespaces joined by the colon character (“:”) beginning with `urn` and followed by a namespace identifier (NID). The proposed NID for URNs within the GTFS is `gtfs`, resulting in the first portion of a URN being `urn:gtfs:`. This formatting, with the use of colons to separate terms, is required by the URN standard. Formatting after these terms, including use of colons and other term separators, is at the discretion of the GTFS standards development process. What follows are two recommended formats based on research into other URN schemes.

`urn:gtfs:{entity type}:{jurisdiction names}:{organization name}:{entity name}`

`urn:gtfs:compliance:{jurisdiction names}:{organization name}:{type of law}:{name of law}`

The entity type corresponds with the type of field being described. In the GTFS-eligibilities extension, URNs are used to identify trip purposes, eligibility constraints, and regulatory compliance. Accordingly the proposed entity types are “trip.purpose”, “eligibility”, and “compliance”.

Jurisdiction names identify the governing entities in which the urn is being used. They serve to narrow the scope of the URN’s meaning and application both geographically and administratively. The recommended approach for identifying jurisdictions is described in _[A Uniform Resource Name (URN) Namespace for Sources of Law (LEX)](https://datatracker.ietf.org/doc/html/draft-spinosa-urn-lex-14)_. Names should ideally identify the smallest jurisdictional unit that contains the entire scope of the URN geographically and administratively. For example, if a URN applies exclusively to Multnomah County, Oregon in the United States, the jurisdiction names would be `us;oregon;multnomah.county` rather than `us;oregon` or `us`.

The organization name identifies the entity that applies or determines the entity name. For example, it may be the name of a transit agency that administers a reduced fare strictly within its service area. It may also be a regional planning body that coordinates a common eligibility criteria across multiple transportation providers.

The entity name is the human-readable term the URN is identifying. The term should be durably unambiguous for the organization using it. If appropriate, years or dates (e.g. `2021-05-21`) may be integrated into the name to distinguish it from future versions of a term that may change over time.

For compliance URNs, this specification recommends adhering to format laid out in the [draft LEX URN standard](https://datatracker.ietf.org/doc/html/draft-spinosa-urn-lex-13#section-1.4), replacing `urn:lex` with `urn:gtfs:compliance` as the first portion of the URN. 

Examples of LEX URNs for US laws are available from the [Legal Information Institute](https://www.law.cornell.edu/wiki/lexcraft/urn_lex_illustrative_examples) at the Cornell Law School.


## Example URNs



* Trip purposes
    * `urn:gtfs:trip.purpose:us;oregon;org:ride.connection:recreation;non-specific`
    * `urn:gtfs:trip.purpose:us;oregon;org:ride.connection:medical;cancer.treatment`
    * `urn:gtfs:trip.purpose:us;oregon;org:ride.connection:medical;non-specific`
    * `urn:gtfs:trip.purpose:us;oregon;org:ride.connection:medical;dialysis`
* Eligibilities
    * `urn:gtfs:eligibility:us:va:veteran`
    * `urn:gtfs:eligibility:us;oregon:odva:veteran`
    * `urn:gtfs:eligibility:us;oregon:ride.connection:2021.veteran`
    * `urn:gtfs:eligibility:us;oregon;multnomah.county:ads:case.managed`
    * `urn:gtfs:eligibility:us;oregon;lane.transit.district:low.income`
    * `urn:gtfs:eligibility:us;oregon;lane.transit.district:lane.county.resident`
* Compliance
    * `urn:gtfs:compliance:us:federal:session.law:1990-07-26;pl.101-336,104.stat.327` (Americans with Disabilities Act)


## Namespace Identifier Registration

[Section 5 of RFC 8141](https://www.ietf.org/rfc/rfc8141.html#section-5) calls for the `gtfs` namespace identifier (NID) to be formally registered with the Internet Assigned Numbers Authority (IANA). Currently registered NIDs can be found [here](https://www.iana.org/assignments/urn-namespaces/urn-namespaces.xhtml). A fast-track registration process for standards bodies can be found in [Section 6.3](https://www.ietf.org/rfc/rfc8141.html#section-6.3). It appears that some organizations, such as [Microsoft](https://docs.microsoft.com/en-us/linkedin/shared/api-guide/concepts/urns) and [HBO](https://play.hbomax.com/page/urn:hbo:page:GWPUe_AuML52-hAEAAAAJ:type:feature), use URN formatting without having finalized a registration process.
