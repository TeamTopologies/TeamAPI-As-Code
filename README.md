# TeamAPI documents

A TeamAPI document is a file that defines and annotates the different details of a team and their interactions with other teams within an organziation.

The format of the file must be JSON or YAML; however, only the subset of YAML that matches the JSON capabilities is allowed:

``` YAML
teamapi: 0.0.1
info: 
  name: Example stream A
  focus: Core focus of the team
  type: stream-aligned
channels:
  - type: slack
    name: example-stream-a
searchTerms:
  - term: Example team search term
platform: 
  $ref: https://github.com/example.com/example-platform-team/teamapi.yml
services: 
  - name: Example Service A
    url: https://anexampleservice.com
    versioning: 
      type: semantic
    repository: https://github.com/example.com/example-service-a
work:
  services: 
    - name: Improve the example service a
      $ref: https://github.com/example.com/example-service-a
  waysOfWorking: 
    - name: Lean
      $ref: https://example.internal-wiki.com/ways-of-working/lean 
meetings:
  - purpose: daily sync
    dayOfWeek: Wednesday
    timeOfDay: 09:00
    durationMinutes: 15
interactions:
  - teamName: Example Platform Team
    mode: X-as-a-service
    purpose: Consume the example platform services to reduce cognitive load
    startDate: 01/01/2022
    expectedDuration: 3
    expectedDurationUnit: months
    $ref: https://github.com/example.com/example-platform-team/teamapi.yml
  - teamName: Automation Test Enabling Team
    mode: Facilitating
    purpose: Introduce automation tests into the example service
    $ref: https://github.com/example.com/automation-test-team/teamapi.yml
dependencies:
  - teamName: Example stream b
    description: We currently rely on example stream b to make changes to component X.
    type: Blocking
    $ref: https://github.com/example.com/example-stream-b-team/teamapi.yml 
  - teamName: Example Platform Team
    description: We use the platform team to provide CI/CD services
    type: OK
    $ref: https://github.com/example.com/example-platform-team/teamapi.yml 
```

The TeamAPI document is a machine-readable definition of your team's API. This document can then be used to generate documentation and visualizations of how the teams within your organization are interacting and how that changes over time.

Using a TeamAPI document schema provides a machine-readable and easily parseable by code file that will provide a myriad of useful applications including things like automatic diagram creation or automatic team discovery i.e. something could scan each of your repositories, find the teamapi.yml file, parse it and collate all of the teams in your organization into a diagram that highlights the interactions and dependencies between them.

For more details on the specification please see the [TeamAPI Specification](/spec/teamapi.md)
