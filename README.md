
# Motivation

This questionnaire provides a vendor-neutral list of topics organizations should consider when selecting, reviewing, or replacing a DNS, DHCP, and IP address management solution.

It is intended as a comprehensive checklist rather than a prescribed procurement model. Each organization can decide which requirements apply, how they are prioritized, and how capabilities should be validated.

For requirements that are relevant to an evaluation, customers may optionally record:

| Field | Suggested use |
| --- | --- |
| Priority | Mandatory, important, or optional |
| Applicability | Applicable, not applicable, or to be clarified |
| Support approach | Native, configurable, integration, customization, roadmap, or unsupported |
| Evidence | Documentation, demonstration, proof of concept, or reference deployment |
| Limitations | Scale, platform, license, dependency, or operational constraint |
| Acceptance criteria | The environment-specific condition that must be demonstrated |

Roadmap statements should be clearly distinguished from capabilities available in the evaluated release.

# Table of Contents
<details>
  <summary>Table of Contents</summary>

- [Motivation](#motivation)
- [Optional Prioritization of Requirements](#optional-prioritization-of-requirements)
  - [Writing and Validation Guidance](#writing-and-validation-guidance)
- [Solution Architecture and Operations](#solution-architecture-and-operations)
  - [User Experience and Accessibility](#user-experience-and-accessibility)
  - [Availability and Resilience](#availability-and-resilience)
  - [Solution Architecture](#solution-architecture)
  - [Operations and Lifecycle](#operations-and-lifecycle)
- [Security, Risk and Governance](#security-risk-and-governance)
- [Platform, Administration and Integration](#platform-administration-and-integration)
  - [Deployment Models and Infrastructure](#deployment-models-and-infrastructure)
  - [Management Plane and Data Repository](#management-plane-and-data-repository)
  - [Identity and Delegated Administration](#identity-and-delegated-administration)
  - [Workflow and Change Control](#workflow-and-change-control)
  - [Data Migration](#data-migration)
  - [Automation and APIs](#automation-and-apis)
  - [Discovery](#discovery)
  - [Data Quality and Reconciliation](#data-quality-and-reconciliation)
  - [Observability, Reporting and Audit](#observability-reporting-and-audit)
- [Vendor Services and Support](#vendor-services-and-support)
- [Cloud and Hybrid Infrastructure](#cloud-and-hybrid-infrastructure)
- [Performance, Capacity and Scalability](#performance-capacity-and-scalability)
- [DNS Platform](#dns-platform)
  - [Requirements for DNS Zone Management](#requirements-for-dns-zone-management)
  - [Requirements for DNS Record Management](#requirements-for-dns-record-management)
  - [Requirements for further DNS Capabilities](#requirements-for-further-dns-capabilities)
  - [Requirements for DNS Security](#requirements-for-dns-security)
- [DHCP Platform](#dhcp-platform)
  - [Requirements for DHCP Security](#requirements-for-dhcp-security)
  - [Requirements for DHCP Scope Management](#requirements-for-dhcp-scope-management)
  - [Requirements for DHCP Options](#requirements-for-dhcp-options)
  - [Requirements for DHCP Templates](#requirements-for-dhcp-templates)
  - [Requirements for further DHCP Capabilities](#requirements-for-further-dhcp-capabilities)
- [IPAM and Address Space Management](#ipam-and-address-space-management)
  - [Requirements for Address Space Access Rights](#requirements-for-address-space-access-rights)
  - [Requirements for Meta Data](#requirements-for-meta-data)
  - [Requirements for further Address Space Capabilities](#requirements-for-further-address-space-capabilities)
  - [Requirements for IPv6](#requirements-for-ipv6)
- [Appendix](#appendix)
  - [Footnotes](#footnotes)
</details>

# Optional Prioritization of Requirements

Customers can apply their own prioritization method. A simple option is:

- must-have: critical to meet the requirements
- should-have: important but not essential
- could-have: desirable but optional
- not applicable: outside the scope of the evaluation

This questionnaire does not prescribe scoring, weighting, or a procurement method.

## Writing and Validation Guidance

Requirements should describe the required outcome rather than mandate a particular product architecture. Deployment-specific expectations should be marked as applicable only where the customer genuinely requires them.

Subjective terms such as *high reliability*, *real-time*, *easy*, *large scale*, or *no technical limitations* should be replaced during an evaluation with environment-specific acceptance criteria. Examples include:

- DNS and DHCP services continue operating during a management-plane outage for the required duration.
- Service failures are detected and reported within the required interval.
- Lease, DNS, and discovery data become visible within an agreed interval.
- Bulk operations support the required number of objects within an acceptable completion time.
- Tested capacity supports current demand and the expected growth margin.

Architecture diagrams, operational workflows, limitations, dependencies, and licensing assumptions should be documented where relevant.

# Solution Architecture and Operations

## User Experience and Accessibility

- Management provides a web-based user interface (no fat client required).
- Management Web UI allows deployment of custom SSL certificate.
- Web UI supports standard browsers (Microsoft Edge, Firefox, Chrome, etc.).
- Web UI prevents invalid inputs (IPs, MACs, FQDNs, etc.).
- Web UI is compliant with at least WCAG[^1] 2.1 Level AA guidelines.
- Web UI supports assistive technologies (screen readers, voice control tools, etc.).
- Web UI supports keyboard navigation and skip-to-content features.
- Web UI uses accessible color contrasts and scalable fonts.
- Web UI provides tree-view for hierarchical objects (domain structure, address space, etc.).
- Hierarchical views support the maximum depth required by the customer environment.
- Web UI provides global and user-based data restore.
- Deleting an entity in Web UI removes linked entities (network > IPs, IP > A/PTR, etc.).
- Web UI provides global search functionality.
- Multiple search properties can be combined.
- Complex search properties can be saved for later re-use.

## Availability and Resilience

For applicable requirements, define the expected operating condition, scale, response time, retention period, or failure scenario used for validation.

- Communication between all components must be encrypted.
- Passwords aren't stored in clear-text (config. files, database, etc.).
- No limitations in terms of special characters used within passwords.
- Authorized administrators have sufficient diagnostic access without requiring unrestricted operating-system access for routine operations.
- System level access is not required for job routine operations.
- Failure of central management must not affect DNS and DHCP services.
- DNS and DHCP updates, such as DDNS changes and leases, are queued until the management plane becomes available.
- All components provide an integration with external logging (syslog, SIEM[^2], etc.).
- DNS and DHCP availability targets can be demonstrated against the required failure scenarios.
- Failed services can restart automatically according to a controlled recovery policy.

## Solution Architecture

- Possible separation of services (DNS and DHCP).
- The solution supports the deployment models required by the customer environment.
- Management of 3rd party DNS and DHCP services (Microsoft, Linux, cloud, etc.).
- Central management of all DNS and DHCP data and services.
- DNS and DHCP configuration remains consistent with the authoritative management data and approved change process.
- Management plane supports multi-tenancy (overlapping address and name space).
- Conflicts between tenants can be reviewed in Web UI.
- Selected duplicated objects allowed in management plane (hostnames, addresses, etc.).
- Management plane allows enabling and disabling objects (hostnames, reservations, etc.).
- Management plane can lock objects for other user accounts (prevents parallel administration).

## Operations and Lifecycle

For applicable requirements, define the expected operating condition, scale, response time, retention period, or failure scenario used for validation.

- Central management allows consolidated patch and update management.
- Management and service versions support a documented compatibility matrix during staged upgrades.
- Patch or update of management plane without the need to patch or update service nodes.
- Built-in roll-back mechanism for all patches and updates.
- Web UI provides scheduled tasks for daily routine operations (add, modify, delete objects).
- Debug mode can be activated easily (e.g. within the Web UI).
- The solution monitors the health of its management, database, DNS, DHCP and integration components.
- Monitoring of general OS resources (CPU, RAM, Disk, etc.).
- Monitoring and probing of DNS and DHCP services.


# Security, Risk and Governance

- Management and service components follow documented security-hardening guidelines.
- Default accounts, passwords, certificates and unnecessary services must be changed or disabled before production use.
- Role-based access control supports least privilege and separation of duties.
- Multi-factor authentication is available for privileged and administrative access.
- Break-glass access is supported, restricted, monitored and audited.
- Administrative, API and service credentials can be rotated without service interruption.
- Secrets, private keys and certificates can be stored in a protected key store, HSM or external secrets-management system.
- Certificate inventory, expiration monitoring and renewal workflows are available.
- Security-relevant configuration changes are logged with previous and new values.
- Audit records can be protected against unauthorized alteration and deletion.
- Security logs can be exported to external SIEM, SOAR and observability platforms.
- The solution supports vulnerability assessment and provides a documented process for security advisories and patches.
- Software components, third-party dependencies and supported operating systems are documented.
- The vendor can provide information about secure development, software supply-chain controls and vulnerability disclosure.
- Data location, data residency, retention and deletion requirements can be defined for hosted or SaaS components.
- Configuration compliance and drift from approved baselines can be detected.
- Security policies and exceptions can be reviewed periodically.

# Platform, Administration and Integration

## Deployment Models and Infrastructure

Customers should mark only the deployment profiles relevant to their environment:

- physical appliance
- virtual appliance
- container or Kubernetes
- public cloud or cloud marketplace
- SaaS or managed service

- Physical deployments provide the component redundancy required by the target availability design.
- The deployment model supports redundant service delivery for IPv4 and IPv6 across the required failure domains.
- Hardware support and replacement objectives meet the customer-defined service level.
- Service-node hardware support and replacement objectives meet the customer-defined service level.
- Local service-node settings can be restored from the management repository to support replacement and recovery.
- All components provide a local firewall.
- Only required services are running on all components (e.g. no Web UI on service nodes).
- A dedicated management interface over IPv4 and IPv6 is available where separation of management and service traffic is required.
- Keep Your Hard Drive (KYHD[^3]) or equivalent media-retention service is available where required by policy.

## Management Plane and Data Repository

- Documented and tested platform limits meet the required number of managed DNS, DHCP and IPAM objects, including expected growth.
- The management plane provides supported diagnostic and troubleshooting access appropriate to the selected deployment model.
- Management plane provides redundancy option for its database.
- Management plane comes with built-in backup and restore capabilities.
- Backups can be initiated manually or time-controlled.
- Backup and restore processes support external storage.
- Database allows tenant-specific restore.

## Identity and Delegated Administration

- Access rights in the management plane are based on users, groups and roles.
- Groups and roles can be nested and combined.
- Management plane provides external authentication (AD[^4], LDAP, Radius, TACACS+, etc.).
- Web UI provides single-sign-on (SSO) and multi-factor-authentication (MFA).
- All components provide external authentication for command line accounts (Unix-Shell).
- Management plane supports multiple authenticators (fallback to secondary authenticator).
- Web UI provides centralized session and change tracking (who, when, what).
- Web UI provides object-based session and change tracking (who, when, what).
- Session and change tracking displays the previous and new value of each changed property.
- Tracking history allows to search for changes (e.g. by account or time frame).
- Time frame of changes to keep in tracking history can be controlled (automated deletion).
- Tracking history can be forwarded to third-party systems (syslog, SIEM[^2], Splunk, etc.).
- Access rights for tracking history can be controlled (who can see what in history).
- Groups or roles in Web UI can be mapped against external authentication (e.g. AD[^4] groups).
- Access to menus and actions in the Web UI can be controlled based on permissions.
- Management plane supports the import of access rights.
- Web UI provides an overview of assigned access rights per user, group or role.


## Workflow and Change Control

For applicable requirements, define the expected operating condition, scale, response time, retention period, or failure scenario used for validation.

- Requests for DNS, DHCP and IPAM changes can follow an approval workflow.
- Requester, approver and implementer roles can be separated.
- Different workflows can be assigned by object type, tenant, business unit or risk level.
- Multi-stage approvals are supported where required.
- Emergency changes can use a controlled break-glass process.
- Changes can be scheduled for a defined deployment window.
- Proposed changes can be validated before deployment.
- The expected impact and affected dependent objects can be reviewed before approval.
- Approved changes can be deployed automatically or manually.
- Failed or incorrect changes can be rolled back.
- Notifications can be sent for requests, approvals, rejections, deployments and failures.
- Workflow status, comments and decisions are retained in the audit history.
- Workflows can integrate with IT service management and ticketing systems.

## Data Migration

- The vendor provides supported tools or services for migration analysis, design, data transformation and validation.
- Migration tool provides optimization feature (multi-homed records, orphaned records).
- Management plane supports the import of DNS and DHCP data.
- Import of DNS zones, records & options.
- Import of DHCPv4 scopes, reservations, leases & options.
- Import of DHCPv6 scopes, reservations, leases & options.
- Import of IPv4 networks & network ranges.
- Import of IPv6 networks & network ranges.
- Import of meta data.
- Error handling (syntax issues, etc.).
- Management plane supports the import of data from previous versions into newer versions.

## Automation and APIs

For applicable requirements, define the expected operating condition, scale, response time, retention period, or failure scenario used for validation.

- The solution provides a documented web service API, such as REST[^6], for DNS, DHCP, IPAM and administrative functions.
- API coverage is comparable to the functionality available in the Web UI.
- The API uses documented versioning and deprecation policies, including for legacy interfaces such as SOAP[^7] where supported.
- API documentation includes schemas, examples and error responses.
- An OpenAPI specification or equivalent machine-readable description is available.
- Authentication supports scoped service accounts or API tokens.
- Tokens and credentials can expire, be rotated and be revoked.
- API permissions follow the same access-control model as the Web UI.
- API requests and changes are included in the audit history.
- The API supports filtering, searching, sorting and pagination.
- Bulk operations are supported for common DNS, DHCP and IPAM tasks.
- Long-running operations provide status and error information.
- Validation or dry-run capabilities are available before applying changes.
- APIs provide predictable behavior for retries and duplicate requests.
- Rate limits and platform limits are documented.
- Events can be delivered through webhooks, message queues or equivalent integrations.
- The solution supports common automation tools or infrastructure-as-code workflows where relevant.
- A command line interface (CLI[^5]) is available for administration and automation where required.
- The Web UI can provide simplified dashboards or restricted views for delegated users.

## Discovery

- Management plane provides ping sweep (ICMP[^8] echo request & reply).
- Discovery supports the SNMP versions required by the environment, with SNMPv3 preferred for production use.
- Multiple SNMP community strings can be provided.
- Discovery supports link layer discovery protocol (LLDP).
- Discovery supports Cisco discovery protocol (CDP).
- Discovery results include IP, MAC, connected switch, connected router & time.
- Discovery takes name resolution into account (PTR Records).
- Discovery provides port scan (e.g. nmap).
- VMware infrastructure can be discovered.
- Cloud-based infrastructure can be discovered.
- Management plane lists differences between discovery results & the database.
- Management plane provides manual & automatic import of discovery results.


## Data Quality and Reconciliation

For applicable requirements, define the expected operating condition, scale, response time, retention period, or failure scenario used for validation.

- The solution can identify duplicate, conflicting and overlapping objects.
- Stale, unused and orphaned DNS, DHCP and IPAM objects can be detected.
- Forward and reverse DNS consistency can be checked.
- DNS records, DHCP leases and IPAM assignments can be reconciled.
- Discovery data can be compared with managed IPAM data.
- Cloud network and DNS data can be compared with the central DDI data model.
- An authoritative source can be defined for each managed data type.
- Conflicts between authoritative sources can be reported and resolved through a controlled workflow.
- Reconciliation does not overwrite data automatically unless explicitly configured.
- The origin, freshness and last verification time of discovered or synchronized data are visible.
- Data-quality metrics and exceptions can be reported.
- Data-cleanup operations preserve an audit trail and support review before deletion.

## Observability, Reporting and Audit

- All transactions are logged centrally (user access, API calls, system changes, etc.).
- Management plane provides report templates (utilization, unused objects, etc.).
- Reporting supports various formats (CSV, HTML, PDF, XLS, etc.).
- Reporting can be initiated manually or time-controlled (emailing, upload, etc.).
- Enhanced reporting through read-only direct database access is supported.
- Lists displayed in Web UI can be exported (including search results & tracking history).
- Reporting through a secondary or dedicated database is supported.

# Vendor Services and Support

- Vendor provides quick start guides (PDF, e-learning, videos, etc.).
- Vendor provides offline admin guides (PDF).
- Vendor provides API guides (PDF).
- Vendor provides API examples (Perl, Python, etc.).
- Vendor operates knowledge base (known issues, best practices, etc.).
- Vendor operates ticketing system (issue tracking system).
- Web UI provides context-sensitive or mouse-over help.


# Cloud and Hybrid Infrastructure

- The solution can discover and manage relevant DNS and network objects in AWS, Microsoft Azure and Google Cloud.
- Multiple cloud accounts, subscriptions, projects and regions can be managed.
- VPCs, VNets, subnets, addresses and cloud metadata can be synchronized with IPAM.
- Cloud-native public and private DNS services can be managed or integrated.
- Ownership between the DDI platform and cloud-native services can be defined clearly.
- Synchronization conflicts and out-of-band changes are detected.
- Cloud tags and labels can be mapped to DDI metadata.
- Ephemeral cloud resources can be discovered without creating permanently stale IPAM objects.
- Kubernetes clusters, services, ingress objects and related DNS data can be discovered or integrated where required.
- Cloud automation can request and release networks, addresses and DNS records through APIs.
- The solution supports private connectivity and restricted egress for cloud-hosted components.
- Cloud integrations document required permissions and follow least-privilege principles.


# Performance, Capacity and Scalability

For applicable requirements, define the expected operating condition, scale, response time, retention period, or failure scenario used for validation.

- The vendor documents supported and recommended limits for managed IP addresses, networks and prefixes.
- The vendor documents supported and recommended limits for DNS zones and records.
- The vendor documents supported and recommended limits for DHCP scopes, reservations and leases.
- DNS query capacity and expected latency are documented for supported deployment models.
- DHCP lease allocation capacity is documented for supported deployment models.
- Limits for concurrent administrators, API requests, reports and bulk operations are documented.
- Capacity planning accounts for expected growth and peak demand.
- The solution reports capacity trends and approaching limits.
- Performance behavior during management outages, synchronization backlogs and recovery is documented.
- Scaling can be performed without redesigning the complete environment.
- Performance and capacity assumptions can be validated during a proof of concept where required.

# DNS Platform

- Management plane can manage cloud-based DNS services (Azure DNS, Route 53, etc.).
- Service instance provides high available DNS (cluster, anycast, HA DNS, etc.).
- Management plane and service node can handle split DNS & DNS views.
- Service instance supports recursive DNS.
- Service instance supports restrictions (access lists, signatures, etc.).
- Management plane provides access rights for all DNS objects (hide, view, add, change, delete).

## Requirements for DNS Zone Management

- Management plane supports management for all DNS objects.
- Management of authoritative forward zones.
- Management of authoritative reverse zones.
- Management of DNS updates (DDNS).
- Management of zone transfers (AXFR & IXFR).
- Management of ACLs for dynamic DNS & zone transfers.
- Management of forwarding and stub zones (selective/conditional forwarding).
- Management of delegations within the environment.
- Management of delegations to non-managed party server.
- Management of hidden primary DNS server.
- Management of hidden secondary DNS server.
- Management of secondary with external non-managed primary.
- Web UI supports management of international domain names (IDN).
- Web UI allows to move zones including child zones & records.
- Web UI allows to move zones from existing DNS server to another.
- Web UI supports to rename zones including dependencies (delegations, etc.).
- Web UI supports to change zone type (primary zone $\Rightarrow$ hidden primary zone, etc.).
- Web UI offers grouping for DNS servers\ (assignment of server group to zone instead of individual servers).
- Management plane and service node support multi-primary DNS.

## Requirements for DNS Record Management

- Dependent records are linked in management plane for data consistency (CNAME, SRV, A/PTR, etc.).
- Linked and dependent entities of a record can be accessed easily.
- Movement of record takes dependent records into account.
- Renaming of record takes dependent records into account.
- Management plane supports the management of reverse-only records (PTR without A).
- Web UI lists records of secondary zones of non-managed primary.
- Management plane and service node support the integration with Active Directory (GSS-TSIG signed dynamic DNS updates).
- Management plane and service node support RFC-compliant DNS records.
- [RFC 1035](https://www.rfc-editor.org/rfc/rfc1035.html) records (A, CNAME, PTR, etc.).
- [RFC 2782](https://www.rfc-editor.org/rfc/rfc2782.html) records (SRV).
- [RFC 3596](https://www.rfc-editor.org/rfc/rfc3596.html) records (AAAA).
- Web UI provides real-time visibility for dynamic DNS records.
- Web UI validates user input for zones, records & options.

## Requirements for further DNS Capabilities

- Management plane manages DNS-based authentication of named entities (DANE).
- Web UI provides naming convention for records.
- Web UI provides naming restriction for records.
- Web UI supports management of DNS options at server, view and zone level.
- Web UI provides visibility for inheritance of DNS options.
- Web UI provides templates for zones and records (e.g. www, mail, etc.).
- Changes to a template can be re-applied with linked objects.
- Web UI supports management of DNS options missing in UI (extensions).
- Web UI provides access to name server control utility (RNDC) features (flush DNS, etc.).
- Web UI provides access to DNS logs.
- Web UI manages sub domains without the need for subzones (dotted hostnames).
- Web UI provides access rights for sub domains of dotted hostnames.
- Web UI supports the `$GENERATE` zone statement.
- Web UI provides visibility to differentiate dynamic updates (DDNS) from static records.
- Web UI allows on-the-fly DNS changes through the user (by using dynamic DNS).
- Time to live (TTL) values can be managed for each DNS record individually.
- Web UI allows access to DNS statistics (op codes, query types, etc.).
- Web UI supports bulk changes for DNS records (e.g. renaming based on patterns).

## Requirements for DNS Security

For applicable requirements, define the expected operating condition, scale, response time, retention period, or failure scenario used for validation.

### DNS Security Architecture and Hardening

- Security functions can be applied independently to authoritative DNS, recursive DNS, forwarding DNS and DNS management components.
- Authoritative and recursive DNS roles can be separated onto different service nodes.
- External authoritative DNS, internal authoritative DNS and recursive DNS can be separated into distinct trust zones.
- Management, control-plane and DNS service traffic can use separate interfaces, networks or security policies.
- Service instances support least-functionality deployment with unnecessary services and interfaces disabled.
- DNS software, operating system and packaged dependencies can be patched independently according to documented support policies.
- Security configuration can be managed centrally through reusable and version-controlled policies or templates.
- Configuration changes support validation, approval, staged deployment and rollback.
- Configuration drift between intended and running DNS configuration is detected and reported.
- Administrative access supports role-based access control, multi-factor authentication and separation of duties.
- Privileged actions, policy changes and emergency changes are recorded in a tamper-evident audit trail.
- Cryptographic keys and shared secrets can be stored in a protected key store, HSM or external secrets-management system.
- The platform documents secure configuration baselines for each supported DNS role.

### Authoritative DNS Protection

- Authoritative servers can be configured as authoritative-only and do not provide recursion to untrusted clients.
- Zone transfers are restricted to explicitly authorized secondary servers.
- Dynamic updates are restricted to explicitly authorized clients and zones.
- NOTIFY, update and transfer relationships can be authenticated.
- Source-based and destination-based access control lists can be applied to queries, transfers, updates and administrative operations.
- Hidden-primary and stealth-secondary architectures are supported.
- Authoritative service supports geographic, network and failure-domain diversity.
- Authoritative service supports anycast or equivalent distributed service architectures where required.
- The solution supports response rate limiting or an equivalent mechanism to reduce reflection and amplification abuse.
- The solution supports DNS Cookies or equivalent protections against off-path spoofing where applicable.
- Minimal responses for `ANY` queries or equivalent amplification-reduction behavior can be configured.
- EDNS UDP response sizes and fallback to TCP can be controlled to reduce fragmentation and amplification risk.
- Query and connection limits can be applied by client, server, zone, query type or policy.
- Protections are available for floods, malformed traffic and pseudorandom-subdomain attacks without blocking legitimate traffic indiscriminately.
- Delegation consistency, lame delegations, missing glue, unreachable authoritative servers and other resilience defects are detected.
- External authoritative zones can be monitored from multiple independent vantage points.

### Recursive DNS Protection and Threat Defense

- Recursive service is restricted to authorized clients and cannot operate as an unintended open resolver.
- Recursion, forwarding and cache behavior can be configured independently by client group, network, view or policy.
- The resolver performs source-port and transaction-ID randomization and implements current cache-poisoning defenses.
- DNS Cookies can be used where supported by communicating parties.
- DNSSEC validation can be enabled centrally and overridden only through controlled exceptions.
- Negative trust anchors are time-bounded, documented, auditable and automatically reviewed or expired.
- Response policy zones or equivalent policy mechanisms can block, redirect, sinkhole, rewrite or log selected domain names and responses.
- Security policies can use multiple internal and external threat-intelligence sources.
- Threat-intelligence sources include provenance, confidence, age, expiration and update status.
- Allow lists and exception policies take precedence predictably and are auditable.
- Policies can identify or mitigate phishing, malware, command-and-control, domain-generation algorithms, newly observed domains, DNS tunneling, data exfiltration, fast flux and suspicious DNS behavior.
- Detection can use query names, response data, client identity, destination, timing, volume and behavioral context.
- Policies support monitor-only, alert, block, redirect, sinkhole and custom-response actions.
- Security enforcement can continue during temporary loss of the central management or cloud control plane.
- Cached threat intelligence and policy data have defined freshness, fail-open and fail-closed behavior.
- Blocked responses preserve sufficient context for investigation and user support.
- Policy bypass by hard-coded external resolvers, encrypted DNS or unauthorized forwarding can be detected or controlled where within scope.

### DNS Transaction and Data Protection

- Zone transfers and dynamic updates support TSIG according to [RFC 8945](https://www.rfc-editor.org/rfc/rfc8945.html) or an equivalent standards-based authentication mechanism.
- Strong current TSIG algorithms are supported and deprecated algorithms can be disabled.
- Shared keys can be generated, distributed, rotated, revoked and audited centrally.
- Separate keys can be assigned per relationship, server, zone or purpose.
- Zone transfers can use TLS according to [RFC 9103](https://www.rfc-editor.org/rfc/rfc9103.html) where confidentiality is required and supported.
- GSS-TSIG is supported for secure dynamic updates in Microsoft Active Directory environments.
- DNS management APIs and control channels use authenticated encryption.
- DNS data at rest, backups and exported configuration files can be encrypted.
- Exported zones, logs, packet captures and support bundles can be access-controlled and sanitized.
- The integrity of zone data is checked before publication.
- The platform detects unauthorized, out-of-band or unexpected changes to authoritative data.
- Registrar, registry, DNS-hosting and internal approval workflows can be documented and reconciled for critical domains.

### DNS Monitoring, Detection and Response

- The platform provides real-time and historical visibility into DNS queries, responses, errors, latency, cache behavior and policy actions.
- Monitoring distinguishes authoritative, recursive, forwarding and encrypted DNS traffic.
- Logs include sufficient context to correlate client, source network, queried name, query type, response code, answer, policy, server and timestamp.
- Logging can be filtered and sampled without losing security-relevant events.
- Log retention and deletion can be configured by data type, tenant and legal or operational requirement.
- Sensitive DNS telemetry can be masked, minimized or pseudonymized.
- Events and telemetry can be exported using syslog and documented APIs and integrated with SIEM, SOAR, NDR and observability platforms.
- Alerts can be generated for anomalous query volume, error rates, latency, cache misses, NXDOMAIN spikes, SERVFAIL spikes and unusual record types.
- The platform detects DNS tunneling, data exfiltration, domain-generation behavior, fast flux, cache poisoning indicators and denial-of-service conditions.
- Detections provide the evidence, confidence and affected clients or domains needed for investigation.
- Response actions can be automated through APIs, workflows or integrations while retaining approval and rollback controls.
- Analysts can search historical DNS activity for a domain, client, IP address, policy or time range.
- Packet capture or equivalent detailed diagnostics can be enabled selectively and for a limited duration.
- Security events preserve chain-of-custody and audit information where required.
- Health monitoring covers DNS service availability from the client perspective, not only process or appliance health.
- Recovery procedures support cache flush, policy rollback, zone restore, key recovery and controlled service isolation.

### DNS Privacy and Encrypted DNS

- Recursive resolvers support QNAME minimisation according to [RFC 9156](https://www.rfc-editor.org/rfc/rfc9156.html).
- DNS logging and analytics follow documented data-minimisation, retention and access-control policies.
- The platform can provide a documented recursive-resolver privacy statement aligned with [RFC 8932](https://www.rfc-editor.org/rfc/rfc8932.html) where applicable.
- Encrypted DNS support is evaluated separately for client-to-resolver, resolver-to-resolver and resolver-to-authoritative communication.
- DNS over TLS and DNS over HTTPS can be enabled for authorized clients where required.
- Discovery of designated encrypted resolvers can be supported where applicable.
- Encrypted DNS endpoints use managed certificates, strong TLS configuration and authenticated service identities.
- Policy, logging and troubleshooting behavior for encrypted DNS is documented.
- The organization can define whether external encrypted resolvers are allowed, blocked, redirected or monitored.
- Encrypted DNS does not silently bypass required security controls, split DNS, internal namespaces or regulatory logging obligations.
- The resolver can distinguish privacy protection from anonymity and documents which parties retain visibility into query data.
- Recursive-to-authoritative encryption can be supported where standards, interoperability and operational requirements permit.

### Requirements for DNSSEC Management

- Authoritative DNS supports DNSSEC-enabled zones and the record types required by the DNSSEC standards, including `DNSKEY`, `RRSIG`, `NSEC`, `NSEC3`, `DS`, `CDS` and `CDNSKEY`.
- DNSSEC origin authentication and integrity protection are implemented in alignment with [RFC 9364](https://www.rfc-editor.org/rfc/rfc9364.html) and the applicable DNSSEC standards.
- DNSSEC signing can be enabled per zone and inherited through centrally managed policies.
- DNSSEC validation can be enabled per recursive server, view or policy.
- Validation exceptions and negative trust anchors are documented, time-bounded and audited.
- NSEC and NSEC3 are supported, with configurable denial-of-existence parameters.
- Supported signing algorithms and key sizes are documented and can be restricted by policy.
- Deprecated or prohibited DNSSEC algorithms can be identified and disabled.
- Signing keys can be generated and stored centrally, in an HSM or through an external key-management service.
- Access to private keys is controlled separately from routine DNS administration.
- Separate KSK and ZSK operation and combined signing keys are supported where required.
- Signing parameters, signature validity, refresh intervals and key lifetimes can be assigned through reusable policies.
- Automated scheduled and emergency key rollovers are supported.
- Algorithm rollover is supported.
- Parent-side DS publication and removal can be tracked and coordinated.
- CDS and CDNSKEY automation according to [RFC 8078](https://www.rfc-editor.org/rfc/rfc8078.html) is supported where accepted by the parent.
- Multi-signer DNSSEC according to [RFC 8901](https://www.rfc-editor.org/rfc/rfc8901.html) is supported where required.
- Keys can be backed up, restored, imported, exported, revoked and securely destroyed according to policy.
- The system reports upcoming key, signature and trust-anchor events before they become service-affecting.
- DNSSEC status is visible per zone, signer, key, algorithm, parent and validation state.

### DNSSEC Validation and Deployment Safeguards

- Signed zone contents and RRSIG validity are checked before publication.
- DS, DNSKEY, KSK and ZSK consistency is checked before key activation or removal.
- The platform detects broken, incomplete or unexpected chains of trust before and after deployment.
- Safeguards account for propagation delays, TTLs, signature validity and parent-zone processing time.
- Automated rollover workflows prevent premature removal of keys or DS records.
- Deployment can be staged, validated externally and rolled back safely.
- Independent external validation is performed for public signed zones.
- Alerts identify expired or near-expiry signatures, missing signatures, unsupported algorithms, stale DS records and validation failures.
- DNSSEC failures can be correlated with configuration changes and key-management events.
- Trust-anchor distribution and rollover are managed and monitored for validating resolvers.
- The platform documents implemented safeguards, operational limitations and any roadmap dependencies.

# DHCP Platform

- Service instance provides high available DHCP (cluster, DHCP failover, etc.).
- Management plane provides access rights for all DHCP objects (hide, view, add, change, delete).
- Web UI provides access to DHCP logs.


## Requirements for DHCP Security

For applicable requirements, define the expected operating condition, scale, response time, retention period, or failure scenario used for validation.

- DHCP service can be restricted to approved interfaces, networks and relay sources.
- Access controls can limit which administrators and automation accounts may view or change scopes, reservations, leases and options.
- DHCP server and relay communications can be monitored for unexpected or unauthorized sources.
- Rogue DHCP servers and unexpected DHCP responses can be detected directly or through integration with network infrastructure.
- DHCP starvation, address exhaustion and abnormal lease-consumption behavior can be detected.
- Rate limiting or equivalent protections can reduce abusive DHCP traffic without disrupting legitimate clients.
- DHCP relay information such as Option 82 can be validated and used in policy decisions.
- Untrusted or malformed relay information can be rejected or logged.
- Secure dynamic DNS updates use controlled identities, permissions and keys.
- DHCP-generated DNS records are traceable to the corresponding lease or reservation.
- Lease history includes sufficient client, relay, interface and timing information for investigation.
- Client identification can use MAC address, client identifier, DUID, relay information or other available attributes.
- Policies can distinguish managed, unmanaged, unknown and quarantined clients where required.
- Integration with DHCP snooping, network access control, 802.1X or equivalent controls is supported where required.
- Administrative and failover communication between DHCP components is authenticated and encrypted where supported.
- DHCP failover state, synchronization problems and split-brain conditions are monitored and alerted.
- Unauthorized or out-of-band changes to DHCP configuration can be detected.
- DHCP logs and security events can be exported to SIEM, SOAR, NDR and observability platforms.
- Security monitoring covers DHCPv4 and DHCPv6.
- DHCPv6 controls consider rogue servers, relay behavior, DUID-based identity and prefix delegation.
- Lease data is treated as potentially sensitive and supports access control, retention and deletion policies.

## Requirements for DHCP Scope Management

- Management plane supports management of DHCPv4 & DHCPv6 scopes.
- Management plane supports splitting & merging DHCPv4 & DHCPv6 scopes.
- Management plane supports moving scopes from existing DHCP server to another.
- Management plane supports management of DHCPv4 & DHCPv6 reservations (DUID[^9]).
- Web UI provides real-time visibility for DHCP leases.
- Lease can be converted into Reservation in the Web UI.
- Web UI provides DHCPv4 & DHCPv6 lease history.
- Existing leases can be deleted and freed in the Web UI.
- Expiration or deletion of lease triggers removal of associated entities (dynamic DNS).
- Service instance supports generation of hostnames for clients not sending a name.
- Leases can be assigned based on MAC address or client ID (`dhcp-client-identifier`).
- Service instance supports one lease per client.
- Ping-before-assign functionality can be managed in Web UI.
- Service instance supports legacy implementations (BOOTP, etc.).

## Requirements for DHCP Options

- Management plane supports management of DHCP match classes.
- Management plane supports management of DHCPv4 options ([RFC 2132](https://www.rfc-editor.org/rfc/rfc2132.html)).
- Management plane supports management of DHCPv6 options ([RFC 3319](https://www.rfc-editor.org/rfc/rfc3319.html)).
- Web UI supports management of DHCP options missing in UI (extensions).
- Certain DHCPv4 option value can be changed in Web UI wherever used in the system.
- Certain DHCPv6 option value can be changed in Web UI wherever used in the system.
- Web UI manages DHCP options at server, network, pool & reservation level.
- Web UI provides visibility for inheritance of DHCP options.
- Management plane supports management of custom options (128  - 254).

## Requirements for DHCP Templates

- Web UI provides templates for IPv4 & IPv6 networks.
- Web UI provides templates for IPv4 & IPv6 scopes.
- Web UI provides templates for IPv4 & IPv6 reservations.
- Changes to a template can be re-applied with linked objects.

## Requirements for further DHCP Capabilities

- Management plane provides utilization alerting for DHCP scopes (UI, mails, SNMP[^10], etc.).
- Web UI provides centralized management of MAC addresses & MAC pools.
- Web UI provides visibility into DHCP fingerprinting details.
- Web UI allows access to DHCP statistics (leases per second, etc.).
- Web UI provides monitoring & alarming of DHCP thresholds.
- Web UI supports bulk changes for DHCP reservations and & scopes.

# IPAM and Address Space Management

- Web UI allows management of private IPv4 address space ([RFC 1918](https://www.rfc-editor.org/rfc/rfc1918.html)).
- Web UI allows management of public IPv4 address space.
- Web UI allows management of multicast IPv4 address space (`224.0.0.0/4`).
- Web UI supports allocation of next available IPv4 address range.
- Web UI supports allocation of next available IPv4 address network.
- Web UI supports allocation of next available IPv4 address.
- Web UI supports allocation of next available IPv4 address from offset.
- Web UI supports allocation of next available IPv4 address within specific range.
- Web UI supports management of unique local address (ULA) ranges (`fc00::/7`).
- Web UI supports management of global unicast address (GUA) ranges (`2000::/3`).
- Web UI supports management of multicast IPv6 ranges (`ff00::/8`).
- Web UI prevents or warns about reserved address ranges (TEREDO, 6to4, etc.).
- Link-local addresses (`fe80::/10`) can be documented in Web UI.
- Web UI is able to restrict allowed subnet sizes (e.g. `/24` for IPv4, `/64` for IPv6).
- Web UI supports allocation of next available IPv6 address range.
- Web UI supports allocation of next available IPv6 address network.
- Web UI supports allocation of next available IPv6 address.
- Web UI supports allocation of next available IPv6 address from offset.
- Web UI supports allocation of next available IPv6 address within specific range.
- Web UI supports allocation of overlapping address spaces.

## Requirements for Address Space Access Rights

- Management plane provides access rights for all IPAM objects (hide, view, add, change, delete).
- Management plane provides access rights for non-allocated addresses & address ranges.
- User's access rights are taken into account when searching in the Web UI.

## Requirements for Meta Data

- Management plane provides unlimited meta data (number of field per object).
- Management plane provides meta data for all object types (DNS, DHCP, users, etc.).
- Web UI supports various values for meta data (text, integer, mail, boolean, etc.).
- Meta data fields can be mandatory in the Web UI.
- Predefined values create drop-down menus for meta data in the Web UI.
- Drop-down menus of meta data fields can be nested.
- Web UI prevents invalid inputs for meta data.
- Web UI provides report of unused meta data definitions.
- Web UI provides non-DNS/DHCP-related structures (geographical, organizational, etc.).
- Objects in the Web UI can be tagged or grouped.

## Requirements for further Address Space Capabilities

- Management of DNS, DHCP & IPAM objects in the Web UI is context-independent.
- Web UI provides a consolidated view of DNS & DHCP objects in IPAM networks.
- Available DNS zones per subnet can be restricted in the Web UI.
- Networks can be structured into ranges and child ranges in the Web UI.
- Web UI provides structuring tools (split, merge, move, resize, etc.).
- Web UI allows the management of DNS & DHCP options at IPAM level.
- IP addresses or ranges can be reserved for future use in the Web UI.
- Objects can be cloned in the Web UI (IPs, subnets, zones, etc.).
- Dependencies of entities are linked for data consistency (device, reservation, record, etc.).
- Linked entities can be accessed easily in the Web UI.
- Networks can be moved incl. all IPs and dependencies in the Web UI.
- IP addresses can be moved incl. all dependencies in the Web UI.
- Associations of AD sites can be managed in the Web UI.
- MAC addresses for static non-DHCP IPv4 addresses can be documented in the Web UI.
- Web UI provides monitoring & alarming of network utilization.
- Web UI supports bulk changes for IP addresses, networks and ranges.

## Requirements for IPv6

- Web UI is accessible via IPv6 (dual-stack, native).
- API is accessible via IPv6 (dual-stack, native).
- Service instance provides DNS via IPv6.
- Management plane manages DNS via IPv6.
- Service instance provides DHCP via IPv6 (stateful and stateless).
- Management plane manages DHCP via IPv6.
- Web UI displays DUID[^9] and IAID[^11] for DHCPv6 clients.
- Web UI supports management of DHCPv6 redundancy ([RFC 6853](https://www.rfc-editor.org/rfc/rfc6853.html)).
- Service instances can form an IPv6 cluster.
- Web UI allows central management of company's IPv6 prefix (given GUA[^12] of company).
- Web UI supports management of dual-stack devices (multi-homed).
- Web UI provides navigation between IPv4 & IPv6 information of dual-stack devices.
- IPv6 networks can be linked with corresponding IPv4 networks in the Web UI (1:1, 1:n & n:n associations).
- Web UI provides navigation between linked IPv4 & IPv6 networks.

# Appendix

## Footnotes

[^1]: Web Content Accessibility Guidelines
[^2]: Security Information & Event Management
[^3]: Keep Your Hard Drive
[^4]: Active Directory
[^5]: Command-Line Interface
[^6]: Representational State Transfer Application Programming Interface
[^7]: Simple Object Access Protocol
[^8]: Internet Control Message Protocol
[^9]: DHCP Unique Identifier
[^10]: Simple Network Management 
[^11]: Identity Association Identifier
[^12]: Global Unicast Address
