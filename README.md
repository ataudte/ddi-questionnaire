# DDI Solution Evaluation Framework

## Purpose

This repository provides a vendor neutral collection of questions and requirements for evaluating DNS, DHCP and IP address management solutions.

It is intended as an enterprise reference, not as a universal procurement form. Organizations can select, adapt and expand the topics that matter to their architecture, operating model and risk profile. The value of the framework is the content it prompts an enterprise to examine, not a particular worksheet or total score.

The framework should help an enterprise:

* Translate workshop outcomes into testable solution requirements
* Compare product behavior rather than marketing terminology
* Distinguish native capability from configuration, customization and roadmap claims
* Evaluate source of truth, automation, resilience, security and operational fit
* Test critical workflows with representative data
* Identify migration and coexistence implications before selection
* Create the minimum handover required for migration planning

A suitable solution is not simply the product with the longest feature list. It is the solution that fits the enterprise target state, proves the critical behaviors and has acceptable gaps, dependencies, cost and delivery risk.

## Position In The DDI Lifecycle

This repository is the second part of a three document lifecycle:

1. [`ddi-workshop`](https://github.com/ataudte/ddi-workshop) defines the current state, target operating model, authority, architecture principles and critical workflows.
2. **`ddi-questionnaire`** evaluates candidate solutions against that approved context.
3. [`ddi-migration-plan`](https://github.com/ataudte/ddi-migration-plan) uses the selected solution, proven behavior and known conditions to plan implementation and migration.

### Minimum Input From [`ddi-workshop`](https://github.com/ataudte/ddi-workshop)

The following artifact names are identical in both repositories. They are the minimum information needed to evaluate solutions without allowing product capabilities to define the enterprise target state.

| Workshop input | How it is used in the evaluation |
|---|---|
| Scope and boundaries | Determines which services, platforms, regions, environments and exclusions the evaluation must cover |
| Current state summary | Provides the source systems, dependencies, retained services, custom tooling and technical debt that a solution must accommodate |
| Business and operational outcomes | Connects requirements to the problems and behaviors the enterprise wants to improve |
| Scale and growth assumptions | Tests product limits, placement, performance, retention and expansion against a realistic horizon |
| Target operating model | Tests ownership, delegation, administration, support and governance fit |
| Service disposition | Clarifies which services are expected to be replaced, retained, overlaid or retired |
| Data authority model | Defines which source should win, which services execute changes and how conflicts should be reconciled |
| Target architecture principles | Guides evaluation of deployment, resilience, cloud, security, recovery and lifecycle behavior |
| Required integrations | Identifies systems, data flows and actions that must be supported |
| Security and compliance requirements | Establishes mandatory controls, audit, retention and security operations needs |
| Critical workflows | Defines the end to end behaviors that should be demonstrated or proven |
| Mandatory requirements | Identifies conditions that cannot be traded away by a high score elsewhere |
| Risks and constraints | Exposes migration, contract, data quality, support and organizational issues that affect solution fit |
| Decision log | Prevents the evaluation from reopening approved design decisions without governance |

If one of these inputs is incomplete, the evaluation should record the impact and responsible owner. It should not replace the missing decision with a vendor assumption.

### Minimum Output To [`ddi-migration-plan`](https://github.com/ataudte/ddi-migration-plan)

The following artifact names are used unchanged in [`ddi-migration-plan`](https://github.com/ataudte/ddi-migration-plan). They form the minimum handover contract from evaluation to migration planning.

| Questionnaire output | Minimum content required by the migration plan |
|---|---|
| Selection decision | Selected solution, scope of selection, decision authority and principal rationale |
| Architecture mapping | How the selected components implement the approved target architecture and which services remain external |
| Requirement baseline | Mandatory and material requirements, demonstrated behavior, dependencies and accepted exceptions |
| Gaps and conditions | Workarounds, roadmap dependencies, custom components, compensating controls, owners and review points |
| Proof of concept package | Scenarios, representative data, observations, evidence, failures and conclusions |
| Data migration findings | Supported imports, transformations, limitations, reconciliation behavior and data quality implications |
| Coexistence findings | Proven behavior with retained Microsoft, cloud native, open source, external or legacy services |
| Integration dependencies | APIs, connectors, identities, network flows, certificates, service accounts and external teams needed |
| Operational requirements | Monitoring, backup, recovery, patching, support, skills, audit and administrative model |
| Capacity and placement assumptions | Sizing, service locations, failure domains, traffic, object counts, retention and expansion model |
| Delivery assumptions | Product versions, licensing, professional services, implementation responsibilities and schedule constraints |
| Decision record | Final decisions, rejected alternatives, open conditions and accountable owners |

### Additional Inputs

Useful supporting material may include:

* Current configuration and data exports
* Architecture diagrams
* Incident and operational evidence
* Security policies
* Vendor documentation
* Product lifecycle and release information
* Reference architectures
* Commercial proposals
* Customer reference interviews

### Not Covered

This framework does not replace:

* The enterprise target state workshop
* Legal and commercial due diligence
* A formal request for proposal process
* A complete proof of concept plan
* Detailed low level design
* Migration runbooks

## Evaluation Principles

* Start from enterprise outcomes and architecture, not vendor categories.
* Treat every claim as version and license specific.
* Separate product behavior from professional services, custom code and roadmap.
* Require evidence proportionate to the importance and risk of the requirement.
* Prefer representative data and workflows over isolated feature demonstrations.
* Evaluate retained services and coexistence, not only replacement.
* Treat source of truth as a governance and reconciliation capability, not a database label.
* Evaluate management plane failure separately from DNS and DHCP service failure.
* Evaluate security as architecture, operations, telemetry and governance.
* Keep mandatory requirements visible even if the enterprise later applies scoring.
* Record material gaps, conditions and migration implications in plain language.

# Table Of Contents

* [How To Use This framework](#how-to-use-this-framework)
* [Decision Context](#decision-context)
* [Strategic Screening Questions](#strategic-screening-questions)
* [Proof Of Concept](#proof-of-concept)
* [Overall Requirements](#overall-requirements)
* [Component Requirements](#component-requirements)
* [Requirements For DNS Platform](#requirements-for-dns-platform)
* [Requirements For DHCP Platform](#requirements-for-dhcp-platform)
* [Requirements For Address Space Management](#requirements-for-address-space-management)
* [Commercial, Deployment And Vendor Requirements](#commercial-deployment-and-vendor-requirements)
* [Final Decision](#final-decision)
* [Minimum Handover To The Migration Plan](#minimum-handover-to-the-migration-plan)
* [Optional Scoring Approach](#optional-scoring-approach)
* [Appendix](#appendix)

# How To Use This Framework

## Requirement Classification

Classify requirements by business and architectural importance, not by how easy they are to demonstrate.

* **Must have**: failure makes the solution unsuitable unless an explicit exception is approved
* **Should have**: materially improves fit, risk or operating efficiency
* **Could have**: useful but not a selection driver
* **Not applicable**: outside the approved scope

This classification is a prioritization mechanism. It is not a score.

## Delivery Model

For each important capability, understand how it is delivered:

* Native product behavior
* Standard configuration
* Supported integration
* Optional licensed component
* Professional services
* Customer developed automation
* Third party product
* Product roadmap
* Unsupported

The delivery model affects cost, supportability, upgrade risk and migration planning. A feature that exists only through a custom integration is not equivalent to a supported native workflow.

## Evidence

Evidence can include:

* Product documentation for the evaluated version
* Live demonstration
* Proof of concept result
* API specification
* Architecture or security design
* Support statement
* Release and lifecycle documentation
* Customer reference
* Contractual commitment

The strongest evidence depends on the requirement. Documentation may be sufficient for a standard configuration option, while service failure, migration behavior and end to end automation should normally be observed.

## Evaluation Result

Useful result descriptions include:

* **Supported**: the required behavior is demonstrated with acceptable dependencies
* **Partially supported**: part of the behavior works, or important conditions remain
* **Not supported**: the evaluated solution cannot provide the required behavior
* **Not demonstrated**: the claim was not supported by sufficient evidence
* **Not applicable**: the requirement is outside scope

Avoid hiding important conditions inside a positive result. For example, a capability that requires a separate product, custom code and an unproven upgrade path should not be summarized simply as supported.

## Decision Rules

A sound evaluation should make the following distinctions:

* A failed mandatory requirement is a decision issue, not a scoring issue.
* A roadmap item is not current capability.
* A demonstration with sample objects is not proof of scale or migration behavior.
* An API endpoint is not an end to end supported workflow.
* Discovery does not automatically create authority.
* High availability is not proven until failure and recovery behavior are understood.
* A lower license price does not imply lower total cost.
* A familiar interface does not compensate for weak data or operational fit.

## How To Express An Enterprise Requirement

Each applicable requirement should be understandable without a separate spreadsheet. A useful requirement explains:

* The expected behavior
* Why the behavior matters
* The scope and scale to which it applies
* Observable acceptance criteria
* Required evidence
* Allowed delivery models
* Dependencies and exclusions
* Operational and migration implications

This structure makes the evaluation useful even when the enterprise chooses its own procurement or scoring format.

# Decision Context

## Business And Operational Outcomes

The evaluation should remain connected to the outcomes established by the workshop. Common outcomes include:

* Reduce DNS, DHCP and subnet fulfilment time
* Eliminate duplicate entry across DDI, cloud, ITSM and automation
* Improve visibility across on premises and cloud environments
* Establish trusted ownership and lifecycle data
* Reduce service interruptions and improve recovery
* Enable controlled delegation and self service
* Improve DNS security telemetry and policy response
* Reduce dependence on unsupported platforms and custom scripts
* Simplify upgrades, backup, reporting and support
* Preserve appropriate cloud native and Microsoft operating models

For each relevant outcome, ask whether the solution changes the underlying behavior or merely provides another console.

## Nonnegotiable Technical Requirements

Nonnegotiable requirements often arise from:

* Service availability and recovery objectives
* Regulatory or data residency boundaries
* Required DNS or DHCP protocols and deployment roles
* Active Directory integration
* Retained cloud native or third party services
* Scale limits
* IPv6 requirements
* Security controls
* Audit and retention
* API and automation strategy
* Migration constraints
* Support lifecycle

Keep this list short enough to be meaningful. A requirement should be nonnegotiable because failure creates unacceptable business, security or architecture risk.

## Greatest Migration Risks

Instead of leaving migration risk as an empty result field, examine concrete risk themes during evaluation:

* **Inconsistent data authority**: IPAM, DNS, DHCP, cloud, CMDB and spreadsheets contain different values with no agreed winner.
* **Poor source data quality**: duplicate networks, stale DNS records, invalid names, missing metadata or unsupported field values complicate import.
* **Hidden dependencies**: applications, relays, domain controllers, registrars, scripts or security systems depend on undocumented behavior.
* **DNS timing**: TTLs, negative caching, delegation, forwarding and DNSSEC can outlive the cutover window.
* **DHCP timing and state**: lease duration, relay changes, failover state and client behavior affect coexistence and rollback.
* **Unsupported migration path**: the product imports objects but not policy, history, credentials, keys, leases or custom behavior.
* **Coexistence ambiguity**: source and target systems may both appear authoritative during a transition.
* **Custom integration dependency**: critical workflows rely on customer code without ownership, tests or lifecycle support.
* **Operational readiness**: the target can be built, but monitoring, backup, skills, support and incident procedures are not ready.
* **Capacity or placement mismatch**: the selected architecture cannot meet site, latency, isolation, scale or recovery requirements.
* **Security regression**: the migration removes controls, changes logging or exposes management paths.
* **Contract and licensing constraints**: test, recovery, temporary coexistence or retained capacity requires unplanned licenses or services.

A strong evaluation shows how the candidate solution reduces, transfers or increases these risks.

## Critical Workflows To Prove

Select workflows that expose several capabilities at once. Representative examples include:

* Request, approve, allocate and validate a subnet
* Create DNS records through an application deployment pipeline
* Provision a DHCP scope, options and relay changes
* Discover and reconcile a cloud network
* Delegate administration to a regional or application team
* Recover from management plane failure while DNS and DHCP continue
* Restore or roll back an administrative change
* Send DNS security events to the SOC and apply an approved response
* Retire an application and reclaim its DNS and address data
* Export authoritative data for audit or platform exit

The best workflow is not necessarily the most impressive demonstration. It is the workflow that represents enterprise risk and operating complexity.

## Expected Environment

Scale should be described across several dimensions:

* IPv4 networks, addresses and overlapping spaces
* IPv6 prefixes, addresses and delegated prefixes
* DNS zones, records, views, queries and updates
* DHCP scopes, reservations, leases and relay paths
* Sites, regions and isolated locations
* Cloud accounts, subscriptions, projects and regions
* Administrators, delegated teams and tenants
* API transactions and automation concurrency
* Discovery sources and observed objects
* Audit, query and reporting retention
* Growth, acquisition and divestiture expectations

Published maximums should not be treated as operational design targets. Ask what was tested, under which architecture, with which features enabled and with what recovery behavior.

# Strategic screening questions

The following 25 questions provide an initial screening layer. A positive answer should lead to evidence and deeper examination, not automatic acceptance.

## Visibility and source of truth

### 1. Can the platform provide a unified view of IP addresses, DNS and DHCP through a consistent data model?

Look for:

* Direct relationships between address spaces, networks, addresses, DNS zones, DNS records, DHCP scopes, ranges, reservations and leases
* Consistent ownership, lifecycle state, tags and business metadata across DNS, DHCP and IPAM objects
* Cross service search, reporting and impact analysis without exporting data from separate product databases
* Clear handling of overlapping address spaces, VRFs, tenants, DNS views and duplicate names or addresses
* Visibility into whether data is authoritative, discovered, imported, synchronized or calculated
* APIs that expose the same objects, relationships and validation rules as the user interface
* Predictable synchronization behavior when individual services or external systems change independently

### 2. Can it discover network resources automatically?

Look for:

* Discovery of networks, addresses, VLANs, VRFs, devices, interfaces, DNS services, DHCP services and relevant cloud resources
* Appropriate discovery methods such as ICMP, SNMP, routing tables, ARP or neighbor tables, LLDP, CDP, DNS, DHCP, hypervisor and cloud APIs
* Configurable scope, frequency, scheduling, incremental refresh and on demand discovery
* Distributed discovery options that fit remote sites, segmented networks, cloud environments and restricted security zones
* Provenance, discovery method, confidence, first observed time and last observed time for each discovered object
* Safe handling of unknown, duplicate, stale and conflicting objects without silently overwriting authoritative data
* Clear separation between observed state and approved authoritative state, including review and reconciliation workflows
* Rate limiting, credential protection and network impact controls for discovery activity

### 3. Can it discover and reconcile resources across the cloud platforms in scope?

Look for:

* Coverage of the specific AWS accounts, Azure subscriptions, Google Cloud projects, regions and organizational structures used by the enterprise
* Discovery of cloud networks, subnets, interfaces, addresses, load balancers, private endpoints, DNS zones and other resources relevant to DDI
* Support for multiple tenants and overlapping address spaces without losing cloud ownership and context
* Least privilege identities, cross account access, credential rotation and clear permission requirements
* Event driven or suitably frequent polling behavior, including documented freshness and cloud API rate limit handling
* Reliable treatment of deleted, moved, orphaned and temporarily unavailable cloud resources
* Mapping of native tags, labels, resource identifiers and ownership information into the enterprise data model
* Explicit reconciliation rules between cloud native state, infrastructure as code and the enterprise source of authority

### 4. Can it manage or provide governed visibility into third party DNS and DHCP services that will remain?

Look for:

* Supported Microsoft, open source, cloud native, external provider and network appliance DNS and DHCP services relevant to the enterprise
* A clear distinction between inventory, read only visibility, configuration management and full lifecycle control
* Documented support for the required versions, service roles, object types and vendor specific features
* Collection of operational state such as server health, zones, scopes, leases, configuration status and synchronization state where required
* Preservation of vendor specific settings that cannot be represented safely in a common model
* Drift detection and reconciliation behavior when changes are made outside the DDI platform
* Defined authority and conflict handling when both the platform and the native service can make changes
* Clear support boundaries for connectors, agents, APIs, upgrades, failures and retained native administration

### 5. Can it model broader network context?

Look for:

* Devices, interfaces, VLANs, VRFs, routes, applications, cloud resources, owners, locations and service dependencies relevant to DDI operations
* Relationships that support troubleshooting, impact analysis, automation and security investigations rather than a disconnected asset list
* Extensible object types and metadata that can reflect enterprise terminology without uncontrolled customization
* Data provenance, confidence, lifecycle state and last observed information for imported and discovered context
* Clear distinction between authoritative business data, operational data and observations from external systems
* APIs, events and exports that allow trusted network context to be consumed by ITSM, CMDB, security and automation platforms
* Defined scope so the platform complements rather than ambiguously duplicates an enterprise CMDB or asset inventory
* Query and reporting performance that remains usable as relationships and historical data grow

## Automation and integration

### 6. Can routine DNS, DHCP and IPAM workflows be automated from request to validated completion?

Look for:

* End to end workflows that cover request, validation, policy, approval, execution, verification, notification and closure
* Support for common activities such as subnet allocation, IP assignment, DNS record creation, DHCP scope creation, reservation management and address reclamation
* Validation of naming standards, address policy, available capacity, conflicts, dependencies and required metadata before execution
* Consistent behavior through the user interface, APIs, service portals and infrastructure as code workflows
* Idempotent operations that can be repeated safely without creating duplicate or conflicting objects
* Transaction, rollback or compensating action behavior when only part of a multi step workflow succeeds
* Controlled retry, timeout, exception and manual intervention handling for external system failures
* A correlated audit trail that connects the request and approval to the resulting changes at every execution point

### 7. Does the platform support policy driven approvals and delegation?

Look for:

* Delegation by service, object type, tenant, region, zone, network, address space, environment and permitted action
* Least privilege roles that allow teams to perform approved tasks without broad platform administration
* Single stage, multi stage and conditional approval based on risk, scope, object type, environment or requested capacity
* Separation between requesting, approving, executing, auditing and administering a workflow
* Inherited policies and guardrails that remain effective when administration is delegated to local or application teams
* Temporary access, emergency access and break glass procedures with explicit expiry and retrospective review
* Substitution, escalation and absence handling that prevents workflows from becoming dependent on one approver
* Complete audit of policy evaluation, approval decisions, rejected requests, exceptions and role changes

### 8. Are the APIs comprehensive and well documented?

Look for:

* API coverage for the functions and object types that the enterprise intends to automate, not only basic record creation
* Documentation tied to the evaluated product version, including schemas, examples, authentication and error behavior
* Secure authentication options such as scoped tokens, service accounts, OAuth, mutual TLS or equivalent enterprise controls
* Search, filtering, pagination, bulk operations and asynchronous jobs for large environments
* Idempotency, concurrency control, object versioning or equivalent protection against conflicting automation
* Clear validation errors, stable error codes, correlation identifiers and enough detail for automated recovery and support
* Documented rate limits, performance expectations, event or webhook options and long running operation behavior
* Versioning, backward compatibility, deprecation policy, lifecycle support and test environments for integrations
* Audit attribution that identifies the service account, workflow or integration responsible for each change

### 9. Does the platform integrate with the existing IT ecosystem?

Look for:

* Proven integration with the specific ITSM, CMDB, cloud, orchestration, configuration management, observability, SIEM, SOAR, identity, certificate and secrets platforms in scope
* Clarity on whether each integration is native, partner supplied, community maintained or custom developed
* Defined data direction, trigger, authority and expected outcome rather than a marketing list of product logos
* Supported versions, required licenses, connector deployment, service accounts, network flows and certificate requirements
* Reliable transformation and mapping of objects, metadata, statuses and identifiers between systems
* Error, retry, queue, duplicate and partial failure handling that can be monitored by operations teams
* Least privilege access, credential rotation, encryption and audit for every integration path
* Upgrade compatibility, connector lifecycle, support ownership and a documented path for integration changes
* Extensibility through APIs, events or supported frameworks when a required packaged integration does not exist

### 10. Can approved services be exposed safely to application, cloud and DevOps teams?

Look for:

* A service catalog or equivalent set of clearly defined DNS, DHCP and IPAM operations that teams are allowed to request
* Templates and guardrails for naming, address selection, metadata, environment, ownership, lifecycle and security policy
* Delegated scopes, quotas and capacity limits that prevent one team from consuming or changing unrelated resources
* Access through the tools teams already use, such as portals, APIs, pipelines, infrastructure as code and cloud automation
* Automated validation and conditional approval without granting broad administrator access
* Clear ownership, expiry, renewal and reclamation behavior for resources created through self service
* Immediate confirmation and post change validation at the actual DNS, DHCP or cloud execution point
* Complete attribution and audit regardless of whether the request originated from a person, pipeline or application
* Controlled exception and support paths when a request cannot be completed automatically

## Architecture, scalability and resilience

### 11. Can the architecture grow without disruptive redesign?

Look for:

* Scale limits and tested references for addresses, networks, zones, records, leases, queries, sites, administrators, API calls, integrations and retained history
* A clear path to add sites, regions, cloud environments and service capacity without replacing the management architecture
* Horizontal and vertical scaling options with documented operational and licensing implications
* Performance behavior as object relationships, audit data, telemetry and reporting history increase
* Distributed architecture options that account for latency, bandwidth, data sovereignty and network partitions
* Capacity planning guidance based on real workload dimensions rather than only a maximum object count
* Supported expansion and rebalancing procedures that avoid large service outages or data reimport
* Predictable commercial impact when additional capacity, service nodes or environments are added

### 12. Can major functions scale and be placed independently?

Look for:

* Separation of management, DNS, DHCP, discovery, reporting, telemetry processing and security functions where their requirements differ
* Independent sizing and horizontal scale for service components that experience different traffic or data growth
* Placement of DNS and DHCP services close to users and workloads while retaining governed central management
* Support for data center, branch, edge, private cloud and public cloud placement models required by the architecture
* Failure domain and availability zone choices that do not force every component into the same location
* Resource isolation so reporting, discovery or analytics load cannot degrade authoritative DNS, recursive DNS or DHCP service
* Addition, removal, maintenance and replacement of service nodes without redesigning unrelated functions
* Operational clarity on which components are mandatory, optional, licensed separately or dependent on central connectivity

### 13. What high availability and disaster recovery options exist, and how do they behave during real failures?

Look for:

* Documented behavior for management server, database, service node, network, site, region and cloud control plane failures
* Defined recovery point and recovery time expectations for management data and each DNS or DHCP service role
* Replication, quorum, election and split brain prevention mechanisms that match the proposed architecture
* Continued DNS and DHCP operation when central management, reporting or cloud connectivity is unavailable
* DHCP lease state, DNS data and pending change behavior during failover and isolated operation
* Detection, failover, restoration, rejoin and failback procedures, including the operator decisions required
* Backup and restore coverage for configuration, data, certificates, keys, audit information and integrations
* Recovery to an alternate site or environment without assuming the original platform remains available
* Evidence from failure tests rather than only an architecture diagram or availability percentage

### 14. Can policy and audit remain consistent across distributed, hybrid and multi cloud environments?

Look for:

* Centrally governed policy with controlled local or tenant specific exceptions
* Defined synchronization timing, ordering and consistency behavior for policy and object changes
* Clear operation during site isolation, cloud API interruption and temporary loss of central management
* Queueing, conflict detection and reconciliation when changes occur in more than one location
* Unified attribution and audit across user interface, API, workflow, cloud and third party execution points
* Reliable timestamps, time synchronization and correlation identifiers across distributed components
* Data retention and residency controls that support regional, legal and security requirements
* Policy versioning, inheritance, rollback and evidence of which policy was applied to a specific change
* Strong tenant and administrative boundaries when the same platform serves multiple organizations or environments

### 15. How are upgrades, patches, schema changes and rollbacks performed?

Look for:

* Supported upgrade paths, prerequisites and compatibility matrices for every component in the proposed deployment
* Rolling or staged upgrade options and the actual service impact for management, DNS, DHCP and integrations
* Prechecks, backups, health validation and dry run capabilities before an upgrade changes production state
* Cluster sequencing and the supported duration and limitations of mixed version operation
* Treatment of database and schema migrations, including recovery when a migration fails
* Compatibility of APIs, automation, custom workflows, connectors and exported data formats after an upgrade
* A credible rollback method, including the point after which rollback is no longer possible
* Security patch cadence, emergency patch process and dependency on underlying operating system or appliance releases
* A practical staging and validation approach that reflects production scale and critical integrations

## Security and governance

### 16. Does the platform provide granular role based access and separation of duties?

Look for:

* Permissions by service, object type, tenant, zone, network, address space, region, environment and action
* Separate rights to view, create, modify, delete, approve, deploy, export, administer and audit
* Separation of request, approval, execution, security administration, key management and audit responsibilities
* Integration with enterprise identity providers through SAML, OIDC, LDAP or equivalent methods, including MFA enforcement
* Scoped service accounts and API identities that do not reuse human administrator permissions
* Inheritance and delegation behavior that is understandable and does not create hidden privilege escalation
* Temporary, just in time and emergency access with expiry, approval and retrospective review
* Reporting of effective permissions, dormant privileges, role changes and periodic access review evidence
* Isolation between tenants, business units or managed customers where shared infrastructure is used

### 17. Are changes attributable to a user, workflow or system?

Look for:

* Audit records that identify who or what requested, approved, executed and validated a change
* Previous and resulting values, affected objects, timestamps, source interface and execution status
* Correlation across user interface, API, workflow, integration and underlying DNS or DHCP service changes
* Attribution of automated activity to a specific service account, pipeline, connector or scheduled task
* Records of failed, rejected, retried, partially completed, rolled back and manually corrected changes
* Request identifiers, business context, comments or ticket references that explain why the change occurred
* Search, reporting and export that support operations, compliance and incident investigation
* Protected retention, time synchronization and tamper resistance appropriate to the enterprise audit policy
* Visibility into role, policy and approval changes as well as changes to DDI data

### 18. Does the platform support secure DNS controls and protected administration?

Look for:

* Separation and hardening of authoritative, recursive, forwarding and management roles where required
* Query, recursion, update and zone transfer access controls that can be applied consistently at the correct scope
* TSIG, GSS TSIG, SIG(0) or other supported mechanisms for authenticated transfer and dynamic update workflows
* DNSSEC signing and validation with controlled key generation, storage, rollover, algorithm lifecycle and recovery
* Protection for DNS keys, API credentials, certificates and other secrets, including HSM or external secret store integration where required
* Encrypted management, MFA, least privilege administration, secure session handling and certificate lifecycle management
* Rate limiting, response rate limiting, DNS Cookies and other controls appropriate to the DNS role and threat model
* DNS logging and monitoring that supports security investigation without creating unacceptable performance or privacy impact
* Documented hardening, patching, backup, restore and secure configuration guidance for every deployment model

### 19. Can it detect, block or provide evidence for malicious DNS activity?

Look for:

* Visibility into query and response patterns that can reveal tunneling, data exfiltration, domain generation algorithms, fast flux, suspicious newly observed domains and abnormal client behavior
* Detection methods that combine DNS behavior, client context and threat intelligence rather than relying on a static block list alone
* Clear distinction between native detection, integrated third party detection and data merely exported for later analysis
* Policy actions such as block, refuse, redirect, sinkhole, allow, alert and observe, with controlled scope and precedence
* Tuning, exception, allow list and false positive management suitable for enterprise applications
* Threat intelligence provenance, freshness, confidence and update failure behavior
* Client, device, user, domain, response and timeline context that supports investigation and containment
* Integration with SIEM, SOAR, EDR, firewall and incident response processes
* Capacity and availability behavior when inspection, logging or blocking features are enabled at production scale

### 20. Can DDI telemetry support security monitoring and incident response?

Look for:

* DNS query and response data, DHCP lease and option data, IPAM ownership, change history and service health relevant to security use cases
* Correlation of an address with device, user, lease, relay, location, network and time without assuming an address has one permanent owner
* Accurate timestamps, retention, indexing and search across the time period needed for investigation
* Real time streaming, syslog, API, event and export options with documented schemas
* Stable identifiers and correlation fields that allow DDI events to be joined with endpoint, identity, network and cloud telemetry
* Volume, sampling, aggregation and storage behavior, including the effect of high query rates and long retention
* Privacy, access control, regional retention and data minimization options for DNS and client information
* Monitoring of export failures, dropped events, queue backlog and schema changes
* Forensic preservation and audit evidence that remains available after a service or management failure

## Cost, deployment and vendor fit

### 21. Is total cost transparent?

Look for:

* The exact licensing metric, such as managed addresses, service nodes, users, queries, features, tenants, cloud resources or subscription tier
* Cost behavior as the environment grows, including additional sites, clouds, addresses, traffic, history and nonproduction systems
* Mandatory modules, security subscriptions, connectors, API access, reporting, discovery and support tiers
* Infrastructure costs for appliances, virtual machines, cloud compute, storage, backup, network traffic and log retention
* Design, implementation, migration, data cleansing, customization, integration and training services
* Ongoing administration, support, upgrade, certificate, key, monitoring and operational skill requirements
* High availability, disaster recovery, lab, test, development and standby licensing
* Contract terms for price changes, renewal, portability, expansion, reduction and divestiture
* Exit costs, including data export, custom integration replacement and legacy decommissioning

### 22. What is a realistic deployment time for an environment of comparable size and complexity?

Look for:

* A timeline based on comparable scale, architecture, data quality, cloud footprint, retained services and integration complexity
* Separation between software installation, production readiness, migration, operational acceptance and legacy retirement
* Explicit phases for design, prerequisites, build, data preparation, integration, testing, training, migration waves and early life support
* Customer, vendor and partner responsibilities with realistic staffing and decision availability
* Dependencies on procurement, firewall rules, identity, certificates, cloud permissions, service accounts, facilities and change windows
* The effect of data cleansing, custom workflows, application dependencies and coexistence on the critical path
* Assumptions about outage windows, change freezes, approvals and business calendar constraints
* Contingency for failed tests, delayed dependencies, remediation and repeated migration waves
* Evidence from completed projects rather than an ideal installation schedule

### 23. Which professional services are mandatory and which are optional?

Look for:

* Clear separation of required design, installation, configuration, migration, customization, integration, training and managed service activities
* The reason a service is mandatory and whether the enterprise or a qualified partner can perform it instead
* Defined deliverables, acceptance criteria, documentation and knowledge transfer for each service engagement
* Data migration scope, supported source formats, transformation limits, exception handling and reconciliation responsibility
* Ownership, intellectual property, source code, testing and support model for custom workflows and integrations
* Vendor versus partner responsibilities and the escalation path when multiple organizations deliver the solution
* Fixed price and time and materials assumptions, exclusions, travel, remote work and change control
* Ongoing dependence on services after go live and whether normal administration can be performed by enterprise staff
* Post migration support, defect correction and handover obligations

### 24. Does the vendor have a credible product roadmap and investment strategy?

Look for:

* Clear distinction between available capability, committed delivery and longer term direction
* Alignment with the enterprise needs for automation, cloud, APIs, security, data governance, deployment flexibility and operational scale
* A track record of delivering roadmap items and maintaining them after introduction
* Release cadence, security response, quality, support lifecycle and end of life notification practices
* Backward compatibility, API stability, migration support and treatment of deprecated deployment models or integrations
* Evidence of sustained product engineering, documentation, support and ecosystem investment
* Customer feedback mechanisms and the vendor's ability to prioritize enterprise requirements
* Participation in relevant standards and support for interoperable data and automation models
* Product consolidation, acquisition or platform transition risks that could change the selected architecture
* Confirmation that mandatory current requirements do not depend on an uncommitted roadmap promise

### 25. Can the vendor provide comparable customer references?

Look for:

* References with similar scale, industry, regulatory obligations, geographic distribution, cloud use and operational model
* Environments that retained comparable Microsoft, cloud native, open source, external or legacy services
* A migration profile similar in source platforms, data complexity, coexistence and cutover risk
* Experience with the same product generation, deployment model and major features being evaluated
* Actual implementation duration, customer effort, professional services dependence and operational staffing
* Honest discussion of limitations, failed assumptions, workarounds, upgrades and support escalations
* Proven high availability, disaster recovery, security, automation and integration behavior in production
* The ability to speak directly with technical and operational stakeholders rather than receiving only a prepared success story
* References that have operated the platform long enough to evaluate lifecycle, support and upgrade experience

# Proof Of Concept

A proof of concept should test decision risk, not reproduce a polished product demonstration.

## Required Proof Of Concept Tests

### 1. Import And Reconcile Representative Data

Use a meaningful subset of real DNS, DHCP and IPAM data.

Examine:

* Import coverage
* Invalid and duplicate data handling
* Object and metadata mapping
* Authority and conflict rules
* Dry run and exception reporting
* Repeated import behavior
* Rollback or cleanup
* Reconciliation counts and evidence

### 2. Automate An End To End Workflow

Choose a workflow with request, policy, approval, execution and validation.

Examine:

* Identity and authorization
* Required input validation
* Idempotency
* Error and retry behavior
* Audit trail
* Result at the execution point
* Rollback or compensation
* Supportability by the intended operations team

### 3. Simulate A Service Failure

Test a failure relevant to the target architecture.

Examine:

* Client impact
* Detection time
* State consistency
* Automatic and manual recovery
* Management visibility
* Failback
* Audit and alerting
* Behavior while central management is unavailable

### 4. Execute An Integrated Workflow Through APIs

Use at least one real integration pattern.

Examine:

* Authentication and authorization
* API coverage
* Versioning
* Pagination and bulk behavior
* Rate limits
* Error details
* Event or polling model
* Idempotency
* Logging and support boundaries

### 5. Demonstrate Multi Environment Visibility

Include on premises and at least the cloud or third party environments that matter to the enterprise.

Examine:

* Account and tenant separation
* Discovery completeness
* Provenance and freshness
* Overlapping data
* Authority and reconciliation
* Search, reporting and API access
* Deletion behavior

## What A Useful Proof Of Concept Report Contains

The report should explain:

* Why each scenario was selected
* Which enterprise requirement or risk it tests
* The data and environment used
* The exact product version and license
* What was observed
* Which dependencies or manual steps were required
* What failed or remained unproven
* What evidence was retained
* The operational and migration significance
* Whether the result is acceptable, conditional or unsuitable

## Warning Signs

Treat the following as reasons for deeper investigation:

* The vendor changes the scenario to avoid representative data.
* A feature works only in a different product version or edition.
* The demonstration uses broad administrator rights that would not be accepted in production.
* Manual cleanup is hidden between test steps.
* A failure test stops before restoration or failback.
* API behavior differs materially from the user interface.
* Errors are visible only in internal logs that customers cannot access.
* Reconciliation overwrites data without a dry run or clear authority rule.
* A roadmap item is presented as current capability.
* Custom code has no clear owner, test strategy or upgrade commitment.

# Overall Requirements

## Requirements For Accessibility

* Management provides a web based user interface without a required fat client.
* The management UI supports custom TLS certificates and documented certificate renewal.
* The management UI supports current standard browsers.
* The UI validates IP addresses, prefixes, MAC addresses, FQDNs and other structured input.
* The UI conforms to at least [WCAG 2.1 Level AA](https://www.w3.org/WAI/WCAG2AA-Conformance) or the organization's required accessibility standard.
* The UI supports screen readers, keyboard navigation, scalable fonts and sufficient color contrast.
* Hierarchical objects such as domain structures and address space can be displayed as a tree or equivalent navigable structure.
* The hierarchy has no product limitation that conflicts with the target data model.
* Global and user scoped data restore is available where required.
* Deletion behavior for linked objects is explicit, previewable and protected against unintended cascading changes.
* A global search is available across relevant object types.
* Search criteria can be combined and saved.
* Search respects authorization and tenancy boundaries.
* Lists, searches and filtered results can be exported subject to authorization.
* Large data sets remain usable through pagination, filtering or asynchronous export.

## Requirements For Reliability

* Communication between all components is encrypted where technically applicable.
* Passwords, tokens and private keys are not stored in clear text.
* Credentials can be integrated with an approved secret management process.
* Required password characters and lengths are supported.
* System level access is available under an approved support and break glass model.
* System level access is not required for routine operations.
* Failure of central management does not stop already deployed DNS and DHCP services.
* DNS updates, DHCP lease events and other state changes are queued or handled safely while management is unavailable.
* Queue limits, persistence, replay behavior and conflict handling are documented and testable.
* All components integrate with external logging and monitoring.
* DNS and DHCP services provide high availability appropriate to their role.
* Failed services can restart automatically where safe.
* Split brain, stale configuration and inconsistent state are detected.
* Backup and restore cover configuration, data, keys, metadata, workflow and audit information as required.
* Recovery time and recovery point objectives can be demonstrated.
* Health, capacity and dependency status are available through UI and API.

## Requirements For Architecture

* DNS and DHCP service roles can be separated.
* Authoritative DNS and recursive DNS can be separated.
* The solution supports the required physical, virtual, cloud, appliance or container deployment models.
* Third party DNS and DHCP services can be managed or governed where required.
* DNS, DHCP and IPAM data can be managed centrally without forcing all execution points onto one implementation.
* The platform uses a consistent data model across managed services.
* The platform supports multi tenancy and overlapping address or name spaces where required.
* Conflicts between tenants or data sources can be detected and reviewed.
* Selected duplicate objects can be represented only where the data model and authority rules permit them.
* Objects can be disabled, retired or placed in a nondeploying state without deleting historical context.
* Concurrency control prevents unsafe parallel administration.
* Management, DNS, DHCP, discovery, reporting and security components can scale according to their respective needs.
* Placement supports the required sites, regions, failure domains and cloud environments.
* Service operation during WAN or management plane isolation is documented.
* Architecture avoids a hidden single point of failure in management, database, deployment, licensing or telemetry.
* Capacity limits are documented and tested against the expected horizon.

## Requirements For Maintenance

* Central management provides consolidated patch and update management.
* Supported compatibility between management and service versions is documented.
* Management can be updated independently from service instances where required.
* Patches and updates provide a supported rollback or recovery method.
* Upgrade prerequisites, data migrations, compatibility and expected outages are documented.
* Rolling or phased service upgrades are supported where required.
* Daily operations can be scheduled and automated.
* Diagnostic logging can be enabled without uncontrolled service impact or data exposure.
* The solution monitors its own health.
* CPU, memory, disk, interface, database and queue resources are monitored.
* DNS and DHCP services are probed from relevant client perspectives.
* Configuration drift and unsupported local changes are detected.
* Software and operating system support lifecycles are published.
* Backup restoration and disaster recovery are tested regularly.
* Maintenance actions are attributable and auditable.

## Requirements For Source Of Truth And Data Governance

The platform must not be accepted as a source of truth merely because it contains data. Authority must be defined per data domain.

* Authoritative data domains can be declared for IP space, DNS, DHCP, VLANs, VRFs, devices, cloud resources, applications, ownership and metadata.
* A discovery source is distinguishable from an authoritative source.
* An execution point is distinguishable from the system whose state is accepted as correct.
* Data provenance, source, collection time and last observation are visible.
* Relationships and dependencies can be represented and queried.
* Required objects include addresses, prefixes, zones, records, leases, VLANs, VXLANs, VRFs, devices, users, applications, cloud resources, network objects, ownership and location.
* Conflicting values can be detected, reviewed and resolved according to explicit rules.
* Reconciliation can reject, merge, update or preserve data according to object and field level policy.
* Automated reconciliation supports dry run, approval, audit and rollback.
* Stale, orphaned and unmanaged objects can be identified.
* Confidence or validation state can be represented where observed data is uncertain.
* External systems can consume trusted data through supported APIs, events or exports.
* Consumers can identify whether data is authoritative, observed, inferred or pending approval.
* Data quality metrics are available for completeness, accuracy, consistency, timeliness and uniqueness.
* Retention and deletion policies can meet operational, privacy and compliance requirements.

### Data Authority Questions By Domain

The following domains often need different authority and reconciliation rules:

| Data domain | Questions to resolve during evaluation |
|---|---|
| IP networks and addresses | Can authority be defined by space, VRF, cloud account or field? How are observed addresses reconciled with planned allocation? |
| DNS zones and records | Can different zones or record sources have different owners? How are dynamic update, infrastructure as code and manual changes reconciled? |
| DHCP scopes and reservations | Which system owns configuration, and how are changes made directly on retained servers detected or governed? |
| Cloud networks and DNS | Can cloud remain authoritative for native objects while enterprise DDI provides governance and visibility? |
| Metadata and ownership | Can ownership fields come from ITSM or CMDB without overwriting technical state owned elsewhere? |
| Device observations | Can discovered state remain evidence rather than automatically becoming authoritative data? |

The product should support the enterprise authority model rather than forcing every domain into one global synchronization rule.

## Requirements For Workflow And Self Service

* Approved services can be exposed through a portal, ITSM catalogue, API or equivalent interface.
* Requesters can see required input, policy, approval status and completion state.
* Identity, role, tenant and resource scope are enforced consistently.
* Workflows support creation, modification, deletion, reservation and reclamation.
* High value workflows include address allocation, subnet creation, DNS record management, DHCP provisioning, cloud discovery and reconciliation.
* Approval is configurable by service, object, scope, risk and requester.
* Separation of duties can prevent requesters from approving their own high risk changes.
* Workflows validate preconditions before execution.
* Changes are validated at the execution point after deployment.
* Partial failure results in rollback or a controlled exception state.
* Retry behavior is safe and idempotent.
* Every step is attributable to a person, service account or system.
* Audit records link the original request, approval, API calls, deployed change, validation and rollback.
* Templates and policy can be versioned.
* Temporary resources can expire or enter a review process.
* Quotas and guardrails can be applied to delegated teams.
* Emergency and break glass workflows are controlled and audited.

# Component Requirements

## Requirements For Hardware Appliances

Apply this section only when physical appliances are in scope.

* Platforms provide the required redundant power, storage and interfaces.
* Physical or service redundancy supports IPv4 and IPv6.
* Hardware replacement service meets the required service level.
* Replacement procedures preserve supported local configuration and identity.
* Components provide a local firewall or equivalent host protection.
* Only required services are enabled.
* Management and service traffic can use separate interfaces or networks where required.
* Secure erase, disk retention and keep your hard drive services are available where required.
* Hardware lifecycle, end of sale and end of support are published.
* Capacity upgrades and replacement do not require an unplanned architecture redesign.

## Requirements For Management Database

* Published scale limits meet the expected object count, transaction rate and retention horizon.
* Supported administrative access exists for backup, recovery and troubleshooting.
* The management database supports the required redundancy model.
* Built in backup and restore are available.
* Backups can be initiated manually and by schedule.
* External backup storage is supported securely.
* Restore can be scoped where tenancy and architecture permit.
* Point in time, full and configuration only recovery options are documented.
* Backup encryption, key handling, retention and integrity verification are supported.
* Restore is testable in an isolated environment.
* Database maintenance does not create unacceptable service impact.
* Read replicas or dedicated reporting stores are supported where required.

## Requirements For User Management

* Access is based on users, groups, roles and resource scope.
* Roles can be composed without creating uncontrolled privilege inheritance.
* External authentication supports the required identity providers and protocols.
* Single sign on and multi factor authentication are supported.
* Command line access integrates with approved authentication where applicable.
* Multiple authenticators and controlled emergency access are supported.
* Sessions and changes are tracked centrally.
* Object history shows who changed what, when, through which interface and from which previous value.
* History can be searched by user, service account, object, time, workflow and result.
* Retention can be configured.
* Audit data can be forwarded to external security and compliance systems.
* Audit visibility can be restricted without allowing administrators to erase evidence.
* External groups can map to internal roles and resource scopes.
* UI menus and actions respect authorization.
* Access assignments can be imported and reviewed.
* Effective permissions can be reported per user, group, role and resource.
* Service accounts have scoped permissions, rotation and ownership.
* Dormant accounts and excessive privileges can be identified.
* Privileged actions can require step up authentication or approval.

## Requirements For Migration Tooling

* Supported migration tooling can analyze source data before import.
* The tooling identifies duplicates, orphaned records, invalid syntax, unsupported options and inconsistent relationships.
* DNS zones, records, views, policies, forwarding, delegation and transfer settings can be imported where in scope.
* DHCPv4 and DHCPv6 scopes, pools, reservations, leases, classes and options can be imported where in scope.
* IPv4 and IPv6 networks, ranges, addresses and metadata can be imported.
* Access rights, ownership and workflow metadata can be imported or mapped where required.
* Unsupported source constructs are reported explicitly.
* Transformations are reviewable, repeatable and version controlled.
* Imports support dry run and detailed error handling.
* Partial imports can be rejected or rolled back safely.
* Delta imports are supported for changes between initial export and cutover.
* Object counts and checksums can be reconciled before and after migration.
* Import from previous product versions is supported where relevant.
* The vendor documents coexistence, migration sequence and rollback.
* Migration scripts and custom transformations have clear ownership and support boundaries.

## Requirements For Application Programming Interfaces

* The platform provides supported APIs for operational and administrative functions.
* API coverage is documented for the evaluated version and license.
* The API supports read, create, update, delete, deploy, validate and workflow actions as required.
* Authentication supports approved methods such as scoped tokens, certificates or federated identity.
* Authorization is identical to or stricter than UI authorization.
* Service accounts and tokens have ownership, expiry and rotation.
* APIs are versioned with a published compatibility and deprecation policy.
* Documentation includes schemas, examples, errors and common workflows.
* OpenAPI or an equivalent machine readable description is available where applicable.
* Pagination, filtering, sorting and bulk operations support the expected data volume.
* Long running operations provide asynchronous status.
* Idempotency and retry behavior are documented.
* Validation errors are specific and machine readable.
* Rate limits and concurrency limits are documented.
* API calls are included in the audit trail.
* Webhooks, events or message integration are available where required.
* Supported SDKs, modules or automation examples are available.
* API behavior can be tested in a nonproduction environment.
* An agreed end to end workflow is demonstrated through the API.

## Requirements For Discovery

* The platform supports ICMP discovery where permitted.
* SNMPv3 is supported; older SNMP versions can be disabled where required.
* Multiple discovery credentials and credential scopes are supported securely.
* LLDP and CDP can be used where relevant.
* Results include available IP, MAC, device, interface, switch, router, VLAN, location and observation time context.
* Reverse DNS can enrich discovery without being treated automatically as authoritative.
* Port scanning is controlled, rate limited and authorized.
* Virtual infrastructure can be discovered.
* Cloud infrastructure can be discovered across required providers.
* Multiple cloud accounts, subscriptions, projects, regions and tenants are supported.
* Cloud IP space, DNS services, networks, interfaces and ownership context can be collected.
* Discovery can identify overlapping address ranges and unauthorized or unmanaged resources.
* Discovery results are compared with authoritative data.
* Differences can be reviewed before import or remediation.
* Manual and policy controlled automated reconciliation are supported.
* Discovery never overwrites authoritative data without an explicit rule.
* Provenance and last observed time are retained.
* Stale discovery data expires or is flagged according to policy.
* Schedules, rate limits, credentials and failure status are visible.
* Discovery can operate through distributed workers where network segmentation requires it.

## Requirements For Reporting

* User, API, workflow, system and deployment transactions are logged centrally.
* Standard reports cover utilization, free space, stale objects, conflicts, changes, capacity, service health and policy compliance.
* Reports support required formats such as CSV, JSON, HTML, PDF or XLSX.
* Reports can run manually and by schedule.
* Scheduled delivery supports approved email, storage or integration methods.
* UI lists and search results can be exported.
* Reporting can use a secondary or dedicated database where required.
* Read only access is supported only when it does not bypass security or stability controls.
* Report definitions can be versioned and transported between environments.
* Access to report data respects tenancy, role and resource scope.
* Large reports run asynchronously and do not impair service management.
* Retention and aggregation support the required historical horizon.
* APIs provide access to report data where required.
* Data quality, automation adoption and modernization success measures can be reported.

## Requirements For Documentation And Support

* Current quick start, administration, operations, security and troubleshooting guides are available.
* Offline documentation is available where required.
* API documentation and examples are version aligned.
* Architecture, ports, protocols and communication flows are documented.
* Hardening, backup, recovery, upgrade and rollback procedures are documented.
* Known issues and release notes are accessible.
* A supported ticketing and escalation process exists.
* Support response and restoration commitments match service criticality.
* Context sensitive help is available where useful.
* Training exists for administrators, operators, security teams and delegated users.
* Product lifecycle and end of support dates are published.
* Documentation can be searched and exported where required.
* The vendor provides migration guidance and comparable migration experience.

# Requirements For DNS Platform

* Cloud based DNS services in scope can be managed or governed.
* DNS service supports the required high availability patterns, including clustering, anycast or independent secondary service where appropriate.
* Split DNS and DNS views are supported where required.
* Recursive and authoritative roles can be separated.
* Query, update, transfer and recursion access can be restricted.
* Permissions can be applied to all relevant DNS objects and actions.
* DNS service capacity, latency and query rate can be measured against agreed targets.
* DNS service remains operational during management plane outages according to the target architecture.

## Requirements For DNS Zone Management

* Authoritative forward and reverse zones can be managed.
* Dynamic updates can be controlled and audited.
* Full and incremental zone transfers can be configured.
* ACLs and transaction signatures can protect updates and transfers.
* Forward, stub and conditional forwarding zones can be managed.
* Delegations to managed and unmanaged servers can be represented.
* Hidden primary and hidden secondary patterns can be supported where required.
* Secondary zones with external primaries can be managed or observed.
* Internationalized domain names are supported correctly.
* Zones can be moved with records and dependent objects.
* Server assignment can be changed without recreating zones.
* Zone rename and conversion behavior is explicit and validated.
* DNS server groups or equivalent policy groups can be assigned to zones.
* Multi primary DNS is supported where required.
* Zone templates and policy inheritance are visible.
* Zone state, serial, deployment status and transfer status are available.
* Bulk operations provide preview, validation and rollback.

## Requirements For DNS Record Management

* Dependent records and relationships can be linked for consistency.
* Related objects are navigable.
* Move and rename operations account for dependent records.
* Reverse only PTR records are supported where required.
* Records from externally managed secondary zones can be viewed where required.
* Active Directory secure dynamic update using GSS TSIG is supported where in scope.
* Current RFC compliant record types can be represented without product upgrades where feasible.
* Dynamic records are visible in near real time.
* User input is validated.
* Record provenance distinguishes static, dynamic, discovered, imported and externally managed data.
* TTL can be managed at the required level with policy guardrails.
* Bulk record changes provide impact preview and validation.
* Conflicting CNAME, address and delegation states are prevented or flagged.

## Requirements For Further DNS Capabilities

* DANE related records can be managed where required.
* Naming conventions and restrictions can be defined and enforced.
* DNS options can be managed at server, view and zone level.
* Inheritance and overrides are visible.
* Templates are available for zones and records.
* Template changes can be assessed and reapplied safely.
* Response Policy Zones can be managed.
* Unsupported or advanced DNS settings can be represented without losing configuration on later changes.
* Supported service control operations such as cache flush are available and audited.
* DNS logs and statistics are accessible according to role.
* Subdomains can be managed without unnecessary zone boundaries.
* Delegated permissions can apply below a zone where required.
* Product behavior for generated or synthesized records is documented.
* Dynamic and static changes are distinguishable.
* Controlled immediate deployment is available for urgent changes.
* Query and response metrics include relevant opcode, response code, type, latency and failure data.

## Requirements For DNS Security

* Administrative, update and transfer channels are authenticated and encrypted where applicable.
* Recursive service is restricted to authorized clients.
* Authoritative service does not provide unintended recursion.
* Zone transfers are restricted and logged.
* Response rate limiting or equivalent controls are available where required.
* DNS Cookies or equivalent protocol protections are supported where required.
* Query floods, random subdomain attacks and anomalous response patterns can be detected or mitigated according to the architecture.
* RPZ or equivalent policy enforcement supports controlled block, redirect, sinkhole, log and allow actions.
* Threat intelligence sources can be assessed, combined, scoped and audited.
* Exceptions and allow lists have owners, expiry and review.
* DNS tunneling, domain generation algorithms, fast flux and suspicious domain behavior can be detected directly or through supported integration.
* DNS events can be forwarded to SIEM, SOAR, incident response and threat hunting systems.
* Analysts can correlate client, identity, query, answer, policy action and time where permitted.
* Logging and analytics support privacy, retention and data minimization requirements.
* DNS service continuity during attacks is part of the resilience design.
* Protective DNS policy can be tested before enforcement.
* Detection and policy efficacy can be reported.
* Client use of encrypted DNS can be governed according to organizational policy.

## Requirements For DNSSEC Management

* Authoritative DNSSEC signing and recursive validation are supported independently.
* Record types required by [RFC 4034](https://www.rfc-editor.org/rfc/rfc4034.html), [RFC 5155](https://www.rfc-editor.org/rfc/rfc5155.html), [RFC 7344](https://www.rfc-editor.org/rfc/rfc7344.html), [RFC 7671](https://www.rfc-editor.org/rfc/rfc7671.html) and [RFC 8078](https://www.rfc-editor.org/rfc/rfc8078.html) are supported where applicable.
* Signing can be enabled per zone.
* Validation can be enabled per resolver or policy scope.
* Negative trust anchors can be managed and expire according to policy.
* NSEC and NSEC3 parameters and supported algorithms are configurable according to current policy.
* Keys can be stored and managed centrally or through an approved external key management service.
* Signing parameters are assigned through policies.
* Automatic and emergency ZSK and KSK rollover are supported.
* Key export is controlled and available only where required.
* Rollover and expiry notifications are available.
* Prepublication and double signature rollover methods are supported where applicable.
* Multi signer DNSSEC according to [RFC 8901](https://www.rfc-editor.org/rfc/rfc8901.html) is supported where required.
* RRSIG validity is checked before publication.
* DS, DNSKEY, KSK and ZSK consistency is checked before key removal.
* Broken chains of trust can be detected before deployment.
* Rollover safeguards do not rely solely on manual validation.
* Expired signatures, incomplete signing states and algorithm policy violations generate alerts.
* Parent interaction, DS publication and registrar responsibilities are documented.
* Current safeguards, limitations and roadmap items are documented separately.

# Requirements For DHCP Platform

* DHCPv4 and DHCPv6 services support the required high availability model.
* Permissions apply to DHCP servers, scopes, pools, reservations, options, classes and leases as required.
* DHCP logs and operational state are accessible according to role.
* Management plane failure does not stop lease service according to the target architecture.
* Lease events and configuration state reconcile safely after management recovery.

## Requirements For DHCP Scope Management

* DHCPv4 and DHCPv6 scopes can be managed.
* Scope split, merge, move and resize operations are supported where technically valid.
* Reservations support required client identifiers, DUIDs and identity associations.
* Lease state is visible in near real time.
* Leases can be converted into reservations under controlled rules.
* Lease history retention is configurable.
* Lease deletion and release are authorized and audited.
* DDNS cleanup behavior is configurable and safe.
* Hostnames can be generated for clients that do not provide one where policy permits.
* Allocation can use MAC address, client identifier or other supported classification.
* Duplicate or conflicting client identity behavior is documented.
* Ping check or conflict detection can be configured where required.
* Legacy BOOTP support is available only where explicitly required.
* Multiple scopes per segment and shared networks are supported where required.
* Relay information such as Option 82 can be recorded and used safely.
* Scope utilization, exhaustion risk and failover state are visible.

## Requirements For DHCP Options

* DHCP classification and match rules can be managed.
* Standard DHCPv4 options, including those defined by [RFC 2132](https://www.rfc-editor.org/rfc/rfc2132.html), are supported.
* DHCPv6 options required by the organization and the current DHCPv6 standard [RFC 8415](https://www.rfc-editor.org/rfc/rfc8415.html) are supported.
* Custom and vendor specific options can be defined without unsupported code.
* Option definitions can be changed consistently wherever used.
* Options can be applied at server, shared network, network, pool, class and reservation levels where applicable.
* Inheritance and overrides are visible.
* Option validation prevents invalid type, length and encoding.
* Bulk changes provide impact preview and rollback.

## Requirements For DHCP Templates

* Templates support IPv4 and IPv6 networks, scopes, pools, options and reservations as required.
* Template inheritance and overrides are visible.
* Template changes can be assessed before reapplication.
* Existing objects can be reconciled with updated templates.
* Templates can be versioned and promoted between environments.

## Requirements For Further DHCP Capabilities

* Scope utilization thresholds support UI, email, SNMP or API alerting as required.
* MAC addresses and approved MAC pools can be managed centrally.
* DHCP fingerprinting information is available where required and its confidence is explicit.
* Statistics include lease rate, utilization, failures, latency and failover state.
* Threshold monitoring and alerting are supported.
* Bulk changes are available for reservations, scopes and options.
* Lease query and integration with access control systems are supported where required.
* DHCPv6 prefix delegation is supported where required.

## Requirements For DHCP Security

* Administrative and deployment channels are authenticated and encrypted where applicable.
* Unauthorized configuration changes are detected and audited.
* Lease, reservation, relay and client identity data can be forwarded to security monitoring.
* Rogue DHCP detection is provided directly or through documented integration with network controls.
* DHCP snooping, dynamic ARP inspection and access control dependencies can be represented and monitored where required.
* Relay trust, Option 82 handling and source validation are configurable.
* Rate limits and resource exhaustion protections are available where required.
* Failover communication is protected according to platform capabilities and network design.
* Sensitive DHCP options and client data follow access and retention policy.
* DHCP events can support incident investigation and device attribution.

# Requirements For Address Space Management

* Private, public and multicast IPv4 space can be managed.
* Unique local, global unicast, link local and multicast IPv6 space can be represented appropriately.
* Reserved and special use ranges are identified or validated.
* Next available networks, ranges and addresses can be allocated according to policy.
* Allocation can start from an offset or constrained range where required.
* Overlapping address spaces are supported with explicit tenancy or routing context.
* Prefix length policies can be enforced.
* Reservations for future use can be represented without appearing available.
* Address state, owner, purpose, lifecycle and evidence are visible.
* Duplicate address and overlap checks are context aware.

## Requirements For Address Space Access Rights

* Permissions apply to all IPAM objects and actions.
* Rights can apply to unallocated addresses and ranges.
* Search, reports and API responses respect effective permissions.
* Delegation can be scoped by tenant, VRF, address hierarchy, location, business unit or metadata.
* Effective rights can be reviewed before assignment.

## Requirements For Metadata

* Metadata is available for all required object types.
* Supported field types include text, integer, date, email, boolean, reference and controlled values as required.
* Fields can be mandatory by object type, scope or workflow.
* Controlled values and dependent selections are supported.
* Validation prevents invalid values.
* Unused definitions and inconsistent values can be reported.
* Geographic, organizational, service and lifecycle structures can be represented.
* Objects can be tagged or grouped.
* Metadata has ownership, definition and lifecycle.
* Sensitive metadata can have restricted access.
* Metadata is included in API, import, export, reporting and migration.

## Requirements For Further Address Space Capabilities

* DNS, DHCP and IPAM objects can be managed from relevant operational contexts.
* IPAM networks provide a consolidated view of related DNS and DHCP objects.
* Allowed DNS zones can be constrained by network or policy.
* Networks can be organized into ranges and child ranges.
* Split, merge, move and resize operations are available with validation.
* DNS and DHCP policy can be associated with address hierarchy where appropriate.
* Objects can be cloned safely.
* Dependencies between devices, reservations, leases, records, interfaces and networks are linked.
* Related objects can be navigated.
* Networks and addresses can be moved with required dependencies.
* Active Directory sites can be associated with address ranges where required.
* MAC addresses can be documented for static IPv4 assignments.
* Utilization monitoring and alerting are available.
* Bulk changes support preview, authorization, validation and rollback.
* VLAN, VXLAN, VRF and routing context can be represented where required.
* Cloud network objects can be linked to enterprise address plans.
* Lifecycle states support planned, reserved, active, deprecated, quarantined and retired objects as required.

## Requirements For IPv6

* UI and API are accessible over IPv6 where required.
* DNS service and management operate over IPv6.
* DHCPv6 service and management operate over IPv6.
* DUID and IAID information is visible where applicable.
* Required DHCPv6 high availability or redundancy behavior is supported and documented.
* Service clusters and health checks operate over IPv6 where required.
* Enterprise IPv6 prefixes can be planned and delegated centrally.
* Dual stack devices can be represented without assuming a one to one address mapping.
* Navigation between related IPv4 and IPv6 objects is available.
* IPv4 and IPv6 networks can be associated using the organization's chosen relationship model.
* IPv6 reverse DNS is supported.
* Prefix delegation, SLAAC related information and router advertisement dependencies can be represented where required.
* IPv6 special use ranges and prefix length policy are validated.
* IPv6 discovery, reporting and audit are functionally equivalent to IPv4 where required.

# Commercial, Deployment And Vendor Requirements

## Cost And Licensing

* Licensing metrics are explicit and measurable.
* Initial and expansion costs are predictable for the expected growth model.
* Required licenses for management, DNS, DHCP, discovery, reporting, security, API and nonproduction are identified.
* Disaster recovery, test, development and training environments are priced explicitly.
* Subscription, support, maintenance and hardware costs are separated.
* Cloud licensing and data transfer implications are identified.
* License portability between appliance, virtual and cloud deployment is documented.
* Contract terms cover acquisitions, divestitures, temporary coexistence and migration peaks where relevant.
* Audit rights and true up processes are clear.
* Data export and exit do not require an unreasonable additional license.

## Deployment And Professional Services

* A deployment approach and timeline are provided for a comparable environment.
* Customer and vendor responsibilities are explicit.
* Mandatory professional services are separated from optional optimization.
* Required skills, access, data and infrastructure are listed.
* Assumptions and exclusions are documented.
* Proof of concept, pilot and phased production deployment are supported.
* Migration tooling, custom transformations and rollback support are priced.
* Knowledge transfer and operational handover are included.
* Acceptance criteria and remediation obligations are contractual where appropriate.

## Support And Vendor Fit

* Support coverage, response, escalation and restoration targets meet service criticality.
* Product lifecycle and upgrade policy are credible.
* The roadmap addresses relevant automation, cloud, source of truth, security and integration needs.
* Roadmap statements are separated from currently delivered capability.
* Research and development investment is sufficient for the strategic role of the platform.
* Financial and organizational stability are assessed through procurement processes.
* The vendor has relevant migration experience.
* Comparable customer references are available.
* Partner and channel responsibilities are clear.
* Security vulnerability disclosure and remediation processes are documented.
* Data ownership, portability and termination assistance are contractually clear.


# Final Decision

The final decision should be understandable without reading every evaluation note. It should explain both why the selected solution fits and what the enterprise must still manage.

## Critical Requirement Findings

Highlight:

* Mandatory requirements that were fully demonstrated
* Mandatory requirements that remain conditional
* Any unsupported or unproven requirement with material impact
* Security or resilience concerns
* Scale limits and architecture constraints
* Retained services that influence the design
* Dependencies on separate products, custom code or professional services

## Material Conditions

Conditions should be specific enough to govern delivery. Common examples include:

* A required feature becomes available only in a stated supported version.
* A custom integration must have an owner, test suite and upgrade commitment.
* A retained Microsoft or cloud service must remain the execution point for a defined domain.
* A migration transformation must be validated against the full data set.
* An architecture limit requires a different placement or capacity model.
* A security control requires an external SIEM, DNS security service or secrets platform.
* A licensing condition must cover test, recovery and temporary coexistence.

Every accepted condition should have an accountable owner and a point at which it is reviewed again.

## Proof Of Concept Findings

Summarize:

* Which critical workflows were proven
* Which failure and recovery behaviors were observed
* Which migration and reconciliation behaviors remain uncertain
* Which manual steps or privileges were required
* Which evidence should be reused by the migration team
* Which findings change architecture, cost or schedule assumptions

## Recommendation

A recommendation may be:

* Select the solution for the full approved scope
* Select the solution for a reduced scope
* Select conditionally, subject to named controls or deliverables
* Continue evaluation because material behavior remains unproven
* Reject because mandatory requirements or risk thresholds are not met

## Rationale

A strong rationale connects:

* Business and operational outcomes
* Target architecture and operating model
* Demonstrated product behavior
* Material gaps and conditions
* Migration and coexistence fit
* Security and operational readiness
* Cost and delivery assumptions
* Long term support and exit considerations

The recommendation should not rely on a total score alone.

# Minimum Handover To The Migration Plan

The following package is the minimum input expected by [`ddi-migration-plan`](https://github.com/ataudte/ddi-migration-plan). The names and intent are deliberately identical in both repositories.

| Handover item | Minimum content |
|---|---|
| Selection decision | Selected solution, scope, decision authority and principal rationale |
| Architecture mapping | Selected components, roles, locations, external services and relationship to the approved architecture |
| Requirement baseline | Mandatory and material requirements, demonstrated behavior, dependencies and accepted exceptions |
| Gaps and conditions | Workarounds, roadmap items, custom components, compensating controls, owners and review points |
| Proof of concept package | Scenarios, data, observations, evidence, failures and conclusions |
| Data migration findings | Import coverage, transformations, limitations, reconciliation behavior and data quality impact |
| Coexistence findings | Behavior with retained Microsoft, cloud native, open source, external and legacy services |
| Integration dependencies | APIs, connectors, identities, network flows, certificates, service accounts and external responsibilities |
| Operational requirements | Monitoring, backup, recovery, patching, support, skills, audit and administration |
| Capacity and placement assumptions | Sizing, service locations, failure domains, traffic, object counts, retention and expansion |
| Delivery assumptions | Versions, licensing, professional services, implementation responsibilities and schedule constraints |
| Decision record | Final decisions, rejected alternatives, open conditions and accountable owners |

## Handover Acceptance

The migration team should confirm that:

* The selected architecture can be explained without relying on sales terminology.
* All mandatory conditions are visible.
* Proof of concept evidence is available for reuse.
* Data migration and coexistence assumptions are explicit.
* Required licenses and professional services cover lab, test, recovery, coexistence and production.
* Capacity and placement assumptions are sufficient for design.
* Open questions have owners and do not create hidden production risk.

# Optional Scoring Approach

Some enterprises use scoring to summarize a large evaluation. This framework does not prescribe a formula because procurement methods, risk appetite and mandatory controls differ.

A useful scoring approach may consider:

* Requirement priority
* Degree of demonstrated support
* Evidence quality
* Delivery complexity
* Operational impact
* Migration risk
* Cost and lifecycle impact

Important safeguards:

* Keep scoring separate from the technical content.
* Use mandatory gates for requirements that cannot be traded away.
* Do not let many low value features compensate for one critical failure.
* Distinguish unsupported from not demonstrated.
* Show material conditions beside any score.
* Avoid false precision when the evidence is qualitative.
* Use the score to support discussion, not replace architecture and risk judgment.

Each enterprise can create its own scoring method and result tables around the content in this repository.

# Appendix

## Shared Terminology

| Term | Meaning |
|---|---|
| Authoritative source | The system whose value is accepted when sources disagree |
| Discovery source | A system that observes state without automatically owning it |
| Execution point | The service that publishes DNS, assigns DHCP leases or performs another action |
| Source of truth | A governed collection of authoritative data, ownership and reconciliation rules |
| Delivery model | How a capability is provided, such as native product, configuration, integration or custom code |
| Demonstrated | Observed with sufficient evidence in the evaluated version and scope |
| Condition | A dependency, control or future action required for acceptance |
| Critical workflow | An end to end process that materially influences solution fit and migration risk |
| Coexistence | Temporary or permanent operation with retained services |

## Acronyms

| Acronym | Meaning |
|---|---|
| AD | Active Directory |
| API | Application Programming Interface |
| CMDB | Configuration Management Database |
| DDI | DNS, DHCP and IP Address Management |
| DHCP | Dynamic Host Configuration Protocol |
| DNS | Domain Name System |
| DNSSEC | Domain Name System Security Extensions |
| DR | Disaster Recovery |
| IaC | Infrastructure as Code |
| IPAM | IP Address Management |
| ITSM | IT Service Management |
| NAC | Network Access Control |
| RBAC | Role Based Access Control |
| RPZ | Response Policy Zone |
| SIEM | Security Information and Event Management |
| SOAR | Security Orchestration, Automation and Response |
| TSIG | Transaction Signature |
| VRF | Virtual Routing and Forwarding |
