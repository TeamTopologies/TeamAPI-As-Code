# TeamAPI Specification

[Team Topologies](http://teamtopologies.com/) Team Topologies is the leading approach to organizing business and technology teams for fast flow, providing a practical, step-by‑step, adaptive model for organizational design and team interaction. .

One of the concepts from Team Topologies is the introducation of a [Team API](https://github.com/TeamTopologies/Team-API-template) which helps teams to capture and improve their clarity of purpose.

The TeamAPI Specification is an attempt at codifying the Team API template into a machine readable definition that can be can then be used to generate documentation and visualizations of how the teams within your organization are interacting and how that changes over time.

## Table of Contents<!-- omit in toc -->

- [<a name="definitions"></a>Definitions](#definitions)
  - [<a name="definitionsStreamAlignedTeam"></a>Stream Aligned Team](#stream-aligned-team)
  - [<a name="definitionsPlatformTeam"></a>Platform Team](#platform-team)
  - [<a name="definitionsEnablingTeam"></a>Enabling Team](#enabling-team)
  - [<a name="definitionsComplicatedSubsystemTeam"></a>Complicated Subsystem Team](#complicated-subsystem-team)
  - [<a name="definitionsFacilitation"></a>Facilitation](#facilitation)
  - [<a name="definitionsCollaboration"></a>Collaboration](#collaboration)
  - [<a name="definitionsXAsAService"></a>X-as-a-service](#x-as-a-service)
- [<a name="specification"></a>Specification](#specification)
  - [<a name="format"></a>Format](#format)
  - [<a name="file-structure"></a>File Structure](#file-structure)
  - [<a name="schema"></a>Schema](#schema)
    - [<a name="TASObject"></a>TeamAPI Object](#teamapi-object)
      - [Fixed Fields](#fixed-fields)
    - [<a name="TASVersionString"></a>TeamAPI Version String](#teamapi-version-string)
    - [<a name="infoObject"></a>Info Object](#info-object)
      - [Fixed Fields](#fixed-fields-1)
      - [Info Object Example](#info-object-example)
    - [<a name="channelObject"></a>Channel Object](#channel-object)
      - [Fixed Fields](#fixed-fields-2)
      - [Channel Object Example](#channel-object-example)
    - [<a name="searchTermObject"></a>Search Term Object](#search-term-object)
      - [Fixed Fields](#fixed-fields-3)
      - [Search Term Object Example](#search-term-object-example)
    - [<a name="platformObject"></a>Platform Object](#platform-object)
      - [Fixed Fields](#fixed-fields-4)
      - [Platform Object Example](#platform-object-example)
    - [<a name="serviceObject"></a>Service Object](#service-object)
      - [Fixed Fields](#fixed-fields-5)
      - [Service Object Example](#service-object-example)
    - [<a name="versioningObject"></a>Versioning Object](#versioning-object)
      - [Fixed Fields](#fixed-fields-6)
      - [Versioning Object Example](#versioning-object-example)
    - [<a name="workObject"></a>Work Object](#work-object)
      - [Fixed Fields](#fixed-fields-7)
      - [Work Object Example](#work-object-example)
    - [<a name="workServiceObject"></a>Work Service Object](#work-service-object)
      - [Fixed Fields](#fixed-fields-8)
      - [Work Service Object Example](#work-service-object-example)
    - [<a name="waysOfWorkingObject"></a>Ways Of Working Object](#ways-of-working-object)
      - [Fixed Fields](#fixed-fields-9)
      - [Ways Of Working Object Example](#ways-of-working-object-example)
    - [<a name="meetingsObject"></a>Meetings Object](#meetings-object)
      - [Fixed Fields](#fixed-fields-10)
      - [Meeting Object Example](#meeting-object-example)
    - [<a name="interactionObject"></a>Interaction Object](#interaction-object)
      - [Fixed Fields](#fixed-fields-11)
      - [Interaction Object Example](#interaction-object-example)
    - [<a name="dependencyObject"></a>Dependency Object](#dependency-object)
      - [Fixed Fields](#fixed-fields-12)
      - [Dependency Object Example](#dependency-object-example)

## <a name="definitions"></a>Definitions

### <a name="definitionsStreamAlignedTeam"></a>Stream Aligned Team
Stream-aligned teams should aim to produce a steady flow of feature delivery, with end-to-end responsibility for a service or application.

### <a name="definitionsPlatformTeam"></a>Platform Team
Platform teams provide the underlying internal services required by stream-aligned teams to deliver higher level services or functionalities, thus reducing extraneous cognitive load.

### <a name="definitionsEnablingTeam"></a>Enabling Team
Enabling teams help stream-aligned teams detect and acquire missing capabilities but do not own services themselves.

### <a name="definitionsComplicatedSubsystemTeam"></a>Complicated Subsystem Team
Complicated subsystem teams off-load work from stream-aligned teams on particularly complicated subsystems.

### <a name="definitionsFacilitation"></a>Facilitation
Facilitating is where one team helps another and is the main operating model for enabling teams. This mode is used to help clear impediments and help discover gaps or inconsistencies in existing components and services used by other teams. There should be a focus on the quality of interaction between other teams. Like the Collaboration mode, Facilitating is a temporary interaction mode - the interaction should generally last for no more than a few weeks.

### <a name="definitionsCollaboration"></a>Collaboration
Collaboration is where teams work closely with other teams with different skill sets for a defined period of time (usually a few weeks). This is typically used when a high degree of adaptability or discovery is needed.

### <a name="definitionsXAsAService"></a>X-as-a-service
X-as-a-service (XaaS) is a natural interaction model after collaboration has discovered suitable boundaries. XaaS provides clear ownership of a service with a smaller cognitive load for teams consuming the service. It is important that this interaction mode provides a good developer experience and the service being consumed should generally be managed as [part of] a product.

## <a name="specification"></a>Specification

### <a name="format"></a>Format

The files describing team interactions in accordance with the TeamAPI Specification are represented as JSON objects and conform to the JSON standards.
YAML, being a superset of JSON, can be used as well to represent a TAS (TeamAPI Specification) file.

For example, if a field is said to have an array value, the JSON array representation will be used:

```yaml
{
   "field" : [...]
}
```

While the API is described using JSON it does not impose a JSON input/output to the API itself.

All field names in the specification are **case sensitive**.

In order to preserve the ability to round-trip between YAML and JSON formats, YAML version [1.2](https://www.yaml.org/spec/1.2/spec.html) is recommended along with some additional constraints:

- Tags MUST be limited to those allowed by the [JSON Schema ruleset](https://www.yaml.org/spec/1.2/spec.html#id2803231)
- Keys used in YAML maps MUST be limited to a scalar string, as defined by the YAML Failsafe schema ruleset

### <a name="file-structure"></a>File Structure

An TeamAPI document MAY be made up of a single document or be divided into multiple,
connected parts at the discretion of the author. In the latter case, [Reference Objects](#referenceObject) are used.

By convention, the TeamAPI Specification (TAS) file is named `TeamAPI.json` or `TeamAPI.yaml`.

### <a name="schema"></a>Schema

#### <a name="TASObject"></a>TeamAPI Object

This is the root document object for the API specification.
It combines resource listing and API declaration together into one document.

##### Fixed Fields

Field Name | Type | Description
---|:---:|---
<a name="TASTeamAPI"></a>teamapi | [TeamAPI Version String](#TASVersionString) | **Required.** Specifies the TeamAPI Specification version being used. It can be used by tooling Specifications and clients to interpret the version. The structure shall be `major`.`minor`.`patch`, where `patch` versions _must_ be compatible with the existing `major`.`minor` tooling. Typically patch versions will be introduced to address errors in the documentation, and tooling should typically be compatible with the corresponding `major`.`minor` (1.0.*). Patch versions will correspond to patches of this document.
<a name="TASInfo"></a>info | [Info Object](#infoObject) | **Required.** Core information about the team including their focus and fundamental team type.
<a name="TASChannels"></a>channels | [[Channels Object]](#channelObject) | A list of any channels that can be used to contact the team.
<a name="TASSearchTerms"></a>searchTerms | [[Search Terms]](#searchTermObject) | Any terms specific to this team that people might use to search for.
<a name="TASPlatform"></a>platform | [Platform Object](#platformObject) | If this is present, indicates that this team is part of a wider platform.
<a name="TASServices"></a>services | [[Services Object]](#serviceObject) | A list of any software, services or products that is currently owned by the team.
<a name="TASWork"></a>work | [Work Object](#workObject) | Details of the type of work the team takes part in.
<a name="TASMeetings"></a>meetings | [[Meetings Object]](#meetingObject) | A list of meetings that the team currently takes part in.
<a name="TASInteractions"></a>interactions | [[Interaction Object]](#interactionObject) | Team interactions that the team currently take part in.
<a name="TASDependencies"></a>dependencies | [[Dependency Object]](#dependencyObject) | A list of other teams that the team have a dpendency on.

This object can be extended with [Specification Extensions](#specificationExtensions).

#### <a name="TASVersionString"></a>TeamAPI Version String

The version string signifies the version of the TeamAPI Specification that the document complies to.
The format for this string _must_ be `major`.`minor`.`patch`.  The `patch` _may_ be suffixed by a hyphen and extra alphanumeric characters.

A `major`.`minor` shall be used to designate the TeamAPI Specification version, and will be considered compatible with the TeamAPI Specification specified by that `major`.`minor` version.
The patch version will not be considered by tooling, making no distinction between `1.0.0` and `1.0.1`.

In subsequent versions of the TeamAPI Specification, care will be given such that increments of the `minor` version should not interfere with operations of tooling developed to a lower minor version. Thus a hypothetical `1.1.0` specification should be usable with tooling designed for `1.0.0`.

#### <a name="infoObject"></a>Info Object

Core information about the team including their focus and fundamental team type

##### Fixed Fields

Field Name | Type | Description
---|:---:|---
<a name="infoObjectName"></a>name | `string` | **Required.** The name of the team.
<a name="infoObjectFocus"></a>focus | `string` | The core focus/goal of the team
<a name="infoObjectTyoe"></a>type | `string` | stream-aligned, platform, complicated-subsystem, enabling.

##### Info Object Example

```yaml
info:
  name: Example stream A
  focus: Core focus of the team
  type: stream-aligned
```

#### <a name="channelObject"></a>Channel Object

 A channel that can be used to contact the team

##### Fixed Fields

Field Name | Type | Description
---|:---:|---
<a name="channelObjectType"></a>type | `string` | **Required.** The type of the communication channel.
<a name="channelObjectName"></a>name | `string` | **Required.** The name of the communication channel.

##### Channel Object Example

```yaml
channels:
  - type: slack
    name: example-stream-a
```

#### <a name="searchTermObject"></a>Search Term Object

 A term that can be used to find information about the team and it's products on an internal wiki or similar.

##### Fixed Fields

Field Name | Type | Description
---|:---:|---
<a name="searchTermObjectTerm"></a>term | `string` | **Required.** The searchable term.

##### Search Term Object Example

```yaml
searchTerms:
  - term: Example team search term
```

#### <a name="platformObject"></a>Platform Object

If this is present, indicates that this team is part of a wider platform.

##### Fixed Fields

Field Name | Type | Description
---|:---:|---
<a name="platformObjectRef"></a>$ref | `string` | **Required.** A reference to the team api for the platform team that this team is part of

##### Platform Object Example

```yaml
platform:
  - $ref: https://github.com/example.com/example-platform-team/teamapi.yml 
```

#### <a name="serviceObject"></a>Service Object

Describes any software, services or products that is currently owned by the team.

##### Fixed Fields

Field Name | Type | Description
---|:---:|---
<a name="serviceObjectName"></a>name | `string` | **Required.** The name of the software owned by this team
<a name="serviceObjectUrl"></a>url | `string` |  A url to documentation describing the software
<a name="serviceObjectVersioning"></a>versioning | [Versioning Object](#versioningObject) |  Details of the way in which this product is versioned
<a name="serviceObjectRepository"></a>repository | `string` |  A url to the repository containing source code for this service

##### Service Object Example

```yaml
services:
  - name: Example Service A
    url: https://anexampleservice.com
    versioning:
      type: semantic
    repository: https://github.com/example.com/example-service-a
```

#### <a name="versioningObject"></a>Versioning Object

Details of the way in which a service, subsystem or product is versioned.

##### Fixed Fields

Field Name | Type | Description
---|:---:|---
<a name="versioningObjectType"></a>type | `string` | **Required.** The versioning strategy employed i.e. semantic etc

##### Versioning Object Example

```yaml
versioning:
  type: semantic
```

#### <a name="workObject"></a>Work Object

Details of the type of work the team takes part in.

##### Fixed Fields

Field Name | Type | Description
---|:---:|---
<a name="workObjectServices"></a>services | [Work Service Object](#workServiceObject) | A list of services, software, products that the team is currently working on
<a name="workObjectWaysOfWorking"></a>waysOfWorking | [Ways Of Working Object](#waysOfWorkingObject) | A list of the ways in which the team currently works
<a name="workObjectCrossTeam"></a>crossTeam | [CrossTeamWorkObject](#crossTeamWorkObject) | A list of the cross-team work or improvements that the team currently takes part in

##### Work Object Example

```yaml
versioning:
  type: semantic
```

#### <a name="workServiceObject"></a>Work Service Object

Details of a service that the team is currently working on.

##### Fixed Fields

Field Name | Type | Description
---|:---:|---
<a name="workServiceObjectName"></a>name | `string` | The name of the service being worked on
<a name="workServiceObjectRef"></a>$ref | `string` | A reference to the service being worked on

##### Work Service Object Example

```yaml
work:
  services:
  - name: Improve the example service a
    $ref: https://github.com/example.com/example-service-a
```

#### <a name="waysOfWorkingObject"></a>Ways Of Working Object

Details of how a team is working.

##### Fixed Fields

Field Name | Type | Description
---|:---:|---
<a name="waysOfWorkingObjectName"></a>name | `string` | The name of the way of working
<a name="waysOfWorkingObjectRef"></a>$ref | `string` | A reference to details about the way of working

##### Ways Of Working Object Example

```yaml
work:

  waysOfWorking:
    - name: Lean
      $ref: https://example.internal-wiki.com/ways-of-working/lean
```

#### <a name="meetingsObject"></a>Meetings Object

Details of meetings that the team attends.

##### Fixed Fields

Field Name | Type | Description
---|:---:|---
<a name="meetingsObjectPurpose"></a>purpose | `string` | The purpose of the meeting
<a name="meetingsObjectDayOfWeek"></a>dayOfWeek | `string` | The day of the week that the meeting takes place
<a name="meetingsObjectTimeOfDay"></a>timeOfDay | `string` | The time of day that the week the meeting takes place
<a name="meetingsObjectDurationMinutes"></a>durationMinutes | `integer` | The duration of the meeting in minutes

##### Meeting Object Example

```yaml
meetings:
  - purpose: daily sync
    dayOfWeek: Wednesday
    timeOfDay: 09:00
    durationMinutes: 15
```

#### <a name="interactionObject"></a>Interaction Object

Details of team interactions that the team currently take part in

##### Fixed Fields

Field Name | Type | Description
---|:---:|---
<a name="interactionObjectTeamName"></a>teamName | `string` | The name of the team being interacted with
<a name="interactionObjectPurpose"></a>purpose | `string` | The purpose of the interaction
<a name="interactionObjectStartDate"></a>startDate | `Date` | The date the interaction began
<a name="interactionObjectExpectedDuration"></a>expectedDuration | `string` | The date the interaction began
<a name="interactionObjectExpectedDurationUnit"></a>expectedDurationUnit | `string` | One of Days, Weeks, Months
<a name="interactionObjectRef"></a>$ref | `string` | A reference to the team api of the interacting team

##### Interaction Object Example

```yaml
interactions:
  - team-name: Example Platform Team
    mode: X-as-a-service
    purpose: The purpose of the interaction
    startDate: 01/01/2022
    expectedDuration: 3
    expectedDurationUnit: months
    $ref: https://github.com/example.com/example-platform-team/teamapi.yml
  - team-name: Automation Test Enabling Team
    mode: Facilitating
    purpose: Introduce automation tests into the example service
    startDate: unknown
    $ref: https://github.com/example.com/automation-test-team/teamapi.yml
```

#### <a name="dependencyObject"></a>Dependency Object

Details of dependencies on other teams that the team has

##### Fixed Fields

Field Name | Type | Description
---|:---:|---
<a name="dependencyObjectTeamName"></a>teamName | `string` | The name of the dependent team
<a name="dependencyObjectDescription"></a>description | `string` | A description of the dependency
<a name="dependencyObjectType"></a>type | `string` | The type of the dependency. One of OK, Slowing or Blocking
<a name="dependencyObjectRef"></a>$ref | `string` | A reference to the team api of the dependent team

##### Dependency Object Example

```yaml
dependencies:
  - team-name: Example stream b
    description: We currently rely on example stream b to make changes to component X.
    type: Blocking
    $ref: https://github.com/example.com/example-stream-b-team/teamapi.yml
  - teamName: Example Platform Team
    description: We use the platform team to provide CI/CD services
    type: OK
    $ref: https://github.com/example.com/example-platform-team/teamapi.yml
```
