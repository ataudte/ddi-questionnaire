
# Motivation

This document provides a vendor-neutral starting point for evaluating DNS, DHCP, and IP address management (DDI) solutions. It covers functional, architectural, operational, security, automation, and support requirements. The questionnaire should be adapted to the organization’s risks, operating model, regulatory obligations, and deployment scenarios. Drawings and sketches should be included where they improve clarity.

# Table of Contents
<details>
  <summary>Table of Contents</summary>
  
- [Weighting of Requirements](#weighting-of-requirements)
- [Overall Requirements](#overall-requirements)
  - [Requirements for Accessibility](#requirements-for-accessibility)
  - [Requirements for Reliability](#requirements-for-reliability)
  - [Requirements for Architecture](#requirements-for-architecture)
  - [Requirements for Maintenance](#requirements-for-maintenance)
- [Component Requirements](#component-requirements)
  - [Requirements for Hardware Appliances](#requirements-for-hardware-appliances)
  - [Requirements for Management Database](#requirements-for-management-database)
  - [Requirements for User Management](#requirements-for-user-management)
  - [Requirements for Migration Tool](#requirements-for-migration-tool)
  - [Requirements for Application Programming Interface](#requirements-for-application-programming-interface)
  - [Requirements for Discovery](#requirements-for-discovery)
  - [Requirements for Reporting](#requirements-for-reporting)
  - [Requirements for Documentation and Support](#requirements-for-documentation-and-support)
- [Requirements for DNS Platform](#requirements-for-dns-platform)
  - [Requirements for DNS Zone Management](#requirements-for-dns-zone-management)
  - [Requirements for DNS Record Management](#requirements-for-dns-record-management)
  - [Requirements for further DNS Capabilities](#requirements-for-further-dns-capabilities)
  - [Requirements for DNS Security](#requirements-for-dns-security)
    - [DNS Security Architecture and Hardening](#dns-security-architecture-and-hardening)
    - [Authoritative DNS Protection](#authoritative-dns-protection)
    - [Recursive DNS Protection and Threat Defense](#recursive-dns-protection-and-threat-defense)
    - [DNS Transaction and Data Protection](#dns-transaction-and-data-protection)
    - [DNS Monitoring, Detection and Response](#dns-monitoring-detection-and-response)
    - [DNS Privacy and Encrypted DNS](#dns-privacy-and-encrypted-dns)
    - [Requirements for DNSSEC Management](#requirements-for-dnssec-management)
    - [DNSSEC Validation and Deployment Safeguards](#dnssec-validation-and-deployment-safeguards)
- [Requirements for DHCP Platform](#requirements-for-dhcp-platform)
  - [Requirements for DHCP Scope Management](#requirements-for-dhcp-scope-management)
  - [Requirements for DHCP Options](#requirements-for-dhcp-options)
  - [Requirements for DHCP Templates](#requirements-for-dhcp-templates)
  - [Requirements for further DHCP Capabilities](#requirements-for-further-dhcp-capabilities)
- [Requirements for Address Space Management](#requirements-for-address-space-management)
  - [Requirements for Address Space Access Rights](#requirements-for-address-space-access-rights)
  - [Requirements for Meta Data](#requirements-for-meta-data)
  - [Requirements for further Address Space Capabilities](#requirements-for-further-address-space-capabilities)
  - [Requirements for IPv6](#requirements-for-ipv6)
- [Appendix](#appendix)
  - [Footnotes](#footnotes)
</details>

# Weighting of Requirements

- must-have (critical to meet the requirements)
- should-have (important but not necessary to meet the requirements)
- could-have (desirable but not necessary to meet the requirements)

# Overall Requirements

## Requirements for Accessibility

- management provides a web-based user interface (no fat client required)
- management web UI allows deployment of custom SSL certificate
- web UI supports standard browsers (Microsoft Edge, Firefox, Chrome, etc.)
- web UI prevents invalid inputs (IPs, MACs, FQDNs, etc.)
- web UI is compliant with at least WCAG[^1] 2.1 Level AA guidelines
- web UI supports assistive technologies (screen readers, voice control tools, etc.)
- web UI supports keyboard navigation and skip-to-content features
- web UI uses accessible color contrasts and scalable fonts
- web UI provides tree-view for hierarchical objects (domain structure, address space, etc.)
- tree-view has no limitation regarding the number of hierarchy levels
- web UI provides global & user-based data restore
- deleting an entity in web UI removes linked entities (network > IPs, IP > A/PTR, etc.)
- web UI provides global search functionality
- multiple search properties can be combined
- complex search properties can be saved for later re-use

## Requirements for Reliability

- communication between all components must be encrypted
- passwords aren't stored in clear-text (config. files, database, etc.)
- no limitations in terms of special characters used within passwords
- system level access (root access) is available for all components
- system level access is not required for job routine operations
- failure of central management must not affect DNS and DHCP services
- updates from DNS and DHCP servers (DDNS, leases) queued till management available
- all components provide an integration with external logging (syslog, SIEM[^2], etc.)
- high reliability of the core services DNS and DHCP
- automated restart in case service is down

## Requirements for Architecture

- possible separation of services (DNS and DHCP)
- options for appliance-based or container-based solution
- management of 3rd party DNS and DHCP services (Microsoft, Linux, cloud, etc.)
- central management of all DNS and DHCP data and services
- IPAM instance responsible for creation of DNS and DHCP configuration files
- IPAM instance supports multi-tenancy (overlapping address and name space)
- conflicts between tenants can be reviewed in web UI
- selected duplicated objects allowed in IPAM instance (hostnames, addresses, etc.)
- IPAM instance allows enabling and disabling objects (hostnames, reservations, etc.)
- IPAM instance can lock objects for other user accounts (prevents parallel administration)

## Requirements for Maintenance

- central management allows consolidated patch and update management
- central management provides backward compatibility (version of IPAM & service)
- patch or update of IPAM instance without the need to patch or update service instances
- built-in roll-back mechanism for all patches and updates
- web UI provides scheduled tasks for daily routine operations (add, modify, delete objects)
- debug mode can be activated easily (e.g. within the web UI)
- solution must monitor itself
- monitoring of general OS resources (CPU, RAM, Disk, etc.)
- monitoring and probing of DNS and DHCP services

# Component Requirements

## Requirements for Hardware Appliances

- platform comes with fail-safe components (power, disks, interfaces, etc.)
- platform provides physical redundancy for IPv4 and IPv6 (clustering)
- platform of the IPAM instance comes with next business day hardware refresh
- service instance comes with next business day hardware refresh
- local settings of service instace is stored in database for easy hardware replacement
- all components provide a local firewall
- only required services are running on all components (e.g. no web UI on service instances)
- service instance provides dedicated management interface over IPv4 and IPv6 (separate management and service provisioning)
- platform manufacturer provides KYHD[^3] service

## Requirements for Management Database

- IPAM instance has no technical limitations (number of managed DNS/DHCP objects)
- IPAM instance provides system level access (root access)
- IPAM instance provides redundancy option for its database
- IPAM instance comes with built-in backup & restore capabilities
- backups can be initiated manually or time-controlled
- backup & restore process works with external storage
- database allows tenant-specific restore

## Requirements for User Management

- access rights in the IPAM instance are based on users, groups & roles
- groups & roles can be nested and combined
- IPAM instance provides external authentication (AD[^4], LDAP, Radius, TACACS+, etc.)
- web UI provides single-sign-on (SSO) and multi-factor-authentication (MFA)
- all components provide external authentication for command line accounts (Unix-Shell)
- IPAM instance supports multiple authenticators (fallback to secondary authenticator)
- web UI provides centralized session & change tracking (who, when, what)
- web UI provides object-based session & change tracking (who, when, what)
- session & change tracking displays previous and new value of changed property
- tracking history allows to search for changes (e.g. by account or time frame)
- time frame of changes to keep in tracking history can be controlled (automated deletion)
- tracking history can be forwarded to party systems (syslog, SIEM[^2], Splunk, etc.)
- access rights for tracking history can be controlled (who can see what in history)
- groups or roles in web UI can be mapped against external authentication (e.g. AD[^4] groups)
- access to menus & actions in the web UI can be controlled based on permissions
- IPAM instance supports the import of access rights
- web UI provides an overview of assigned access rights per user, group or role

## Requirements for Migration Tool

- manufacturer provides migration tool for analysis & design
- migration tool provides optimization feature (multi-homed records, orphaned records)
- IPAM instance supports the import of DNS and DHCP data
  - import of DNS zones, records & options
  - import of DHCPv4 scopes, reservations, leases & options
  - import of DHCPv6 scopes, reservations, leases & options
  - import of IPv4 networks & network ranges
  - import of IPv6 networks & network ranges
  - import of meta data
  - error handling (syntax issues, etc.)
- IPAM instance supports the import of data from previous versions into newer versions

## Requirements for Application Programming Interface

- web UI provides a dashboard for daily routine (add host, delete device, etc.)
- IPAM instance provides pre-defined command line interface (CLI[^5])
- IPAM instance comes with web service API (REST[^6], SOAP[^7], etc.)
- IPAM instances provides custom UI to hide features & functions

## Requirements for Discovery

- IPAM instance provides ping sweep (ICMP[^8] echo request & reply)
- IPAM instance and service instance provide SNMP discovery capability (v1, v2c, v3)
- multiple SNMP community strings can be provided
- discovery supports of link layer discovery protocol (LLDP)
- discovery support of Cisco discovery protocol (CDP)
- discovery results include IP, MAC, connected switch, connected router & time
- discovery takes name resolution into account (PTR Records)
- discovery provides port scan (e.g. nmap)
- VMware infrastructure can be discovered
- cloud-based infrastructure can be discovered
- IPAM instance lists differences between discovery results & the database
- IPAM instance provides manual & automatic import of discovery results

## Requirements for Reporting

- all transactions are logged centrally (user access, API calls, system changes, etc.)
- IPAM instance provides report templates (utilization, unused objects, etc.)
- reporting supports various formats (CSV, HTML, PDF, XLS, etc.)
- reporting can be initiated manually or time-controlled (emailing, upload, etc.)
- enhanced reporting through read-only direct database access is supported
- lists displayed in web UI can be exported (including search results & tracking history)
- reporting through a secondary or dedicated database is supported

## Requirements for Documentation and Support

- manufacturer provides quick start guides (PDF, e-learning, videos, etc.)
- manufacturer provides offline admin guides (PDF)
- manufacturer provides API guides (PDF)
- manufacturer provides API examples (Perl, Python, etc.)
- manufacturer operates knowledge base (known issues, best practices, etc.)
- manufacturer operates ticketing system (issue tracking system)
- web UI provides context-sensitive or mouse-over help

# Requirements for DNS Platform

- IPAM instance can manage cloud-based DNS services (Azure DNS, Route 53, etc.)
- service instance provides high available DNS (cluster, anycast, HA DNS, etc.)
- IPAM instance and service instance can handle split DNS & DNS views
- service instance supports recursive DNS
- service instance supports restrictions (access lists, signatures, etc.)
- IPAM instance provides access rights for all DNS objects (hide, view, add, change, delete)

## Requirements for DNS Zone Management

- IPAM instance supports management for all DNS objects
  - management of authoritative forward zones
  - management of authoritative reverse zones
  - management of DNS updates (DDNS)
  - management of zone transfers (AXFR & IXFR)
  - management of ACLs for dynamic DNS & zone transfers
  - management of forwarding and stub zones (selective/conditional forwarding)
  - management of delegations within the environment
  - management of delegations to non-managed party server
  - management of hidden primary DNS server
  - management of hidden secondary DNS server
  - management of secondary with external non-managed primary
- web UI support management of international domain names (IDN)
- web UI allows to move zones including child zones & records
- web UI allows to move zones from existing DNS server to another
- web UI supports to rename zones including dependencies (delegations, etc.)
- web UI supports to change zone type (primary zone $\Rightarrow$ hidden primary zone, etc.)
- web UI offers grouping for DNS servers\ (assignment of server group to zone instead of individual servers)
- IPAM instance and service instance support multi-primary DNS

## Requirements for DNS Record Management

- dependant records are linked in IPAM instance for data consistency (CNAME, SRV, A/PTR, etc.)
  - linked and dependant entities of a record can be accessed easily
  - movement of record takes dependant records into account
  - renaming of record takes dependant records into account
- IPAM instance supports the management of reverse-only records (PTR without A)
- web UI lists records of secondary zones of non-managed primary
- IPAM instance and service instance support the integration with Active Directory (GSS-TSIG signed dynamic DNS updates)
- IPAM instance and service instance support RFC-compliant DNS records
  - [RFC 1035](https://www.rfc-editor.org/rfc/rfc1035.html) records (A, CNAME, PTR, etc.)
  - [RFC 2782](https://www.rfc-editor.org/rfc/rfc2782.html) records (SRV)
  - [RFC 3596](https://www.rfc-editor.org/rfc/rfc3596.html) records (AAAA)
- web UI provides real-time visibility for dynamic DNS records
- web UI validates user input for zones, records & options

## Requirements for further DNS Capabilities

- IPAM instance manages of DNS-based authentication of named entities (DANE)
- web UI provides naming convention for records
- web UI provides naming restriction for records
- web UI supports management of DNS options at server, view and zone level
- web UI provides visibility for inheritance of DNS options
- web UI provides templates for zones and records (e.g. www, mail, etc.)
- changes to a template can be re-applied with linked objects
- web UI supports management of DNS options missing in UI (extensions)
- web UI provides access to name server control utility (RNDC) features (flush DNS, etc.)
- web UI provides access DNS logs
- web UI manages sub domains without the need for subzones (dotted hostnames)
- web UI provides access rights for sub domains of dotted hostnames
- web UI supports the `$GENERATE` zone statement
- web UI provides visibility to differentiate dynamic updates (DDNS) from static records
- web UI allows on-the-fly DNS changes through the user (by using dynamic DNS)
- time to live (TTL) values can be managed for each DNS record individually
- web UI allows access to DNS statistics (op codes, query types, etc.)
- web UI supports bulk changes for DNS records (e.g. renaming based on patterns)

## Requirements for DNS Security

DNS security must be evaluated as a combination of service resilience, configuration integrity, transaction protection, abuse prevention, threat detection, privacy, operational controls, and DNSSEC. DNSSEC provides origin authentication and integrity protection for DNS data, but does not by itself protect DNS availability, endpoint confidentiality, recursive resolvers from abuse, or organizations from malicious use of DNS.

### DNS Security Architecture and Hardening

- security functions can be applied independently to authoritative DNS, recursive DNS, forwarding DNS and DNS management components
- authoritative and recursive DNS roles can be separated onto different service instances
- external authoritative DNS, internal authoritative DNS and recursive DNS can be separated into distinct trust zones
- management, control-plane and DNS service traffic can use separate interfaces, networks or security policies
- service instances support least-functionality deployment with unnecessary services and interfaces disabled
- DNS software, operating system and packaged dependencies can be patched independently according to documented support policies
- security configuration can be managed centrally through reusable and version-controlled policies or templates
- configuration changes support validation, approval, staged deployment and rollback
- configuration drift between intended and running DNS configuration is detected and reported
- administrative access supports role-based access control, multi-factor authentication and separation of duties
- privileged actions, policy changes and emergency changes are recorded in a tamper-evident audit trail
- cryptographic keys and shared secrets can be stored in a protected key store, HSM or external secrets-management system
- the platform documents secure configuration baselines for each supported DNS role

### Authoritative DNS Protection

- authoritative servers can be configured as authoritative-only and do not provide recursion to untrusted clients
- zone transfers are restricted to explicitly authorized secondary servers
- dynamic updates are restricted to explicitly authorized clients and zones
- NOTIFY, update and transfer relationships can be authenticated
- source-based and destination-based access control lists can be applied to queries, transfers, updates and administrative operations
- hidden-primary and stealth-secondary architectures are supported
- authoritative service supports geographic, network and failure-domain diversity
- authoritative service supports anycast or equivalent distributed service architectures where required
- the solution supports response rate limiting or an equivalent mechanism to reduce reflection and amplification abuse
- the solution supports DNS Cookies or equivalent protections against off-path spoofing where applicable
- minimal responses for `ANY` queries or equivalent amplification-reduction behavior can be configured
- EDNS UDP response sizes and fallback to TCP can be controlled to reduce fragmentation and amplification risk
- query and connection limits can be applied by client, server, zone, query type or policy
- protections are available for floods, malformed traffic and pseudorandom-subdomain attacks without blocking legitimate traffic indiscriminately
- delegation consistency, lame delegations, missing glue, unreachable authoritative servers and other resilience defects are detected
- external authoritative zones can be monitored from multiple independent vantage points

### Recursive DNS Protection and Threat Defense

- recursive service is restricted to authorized clients and cannot operate as an unintended open resolver
- recursion, forwarding and cache behavior can be configured independently by client group, network, view or policy
- the resolver performs source-port and transaction-ID randomization and implements current cache-poisoning defenses
- DNS Cookies can be used where supported by communicating parties
- DNSSEC validation can be enabled centrally and overridden only through controlled exceptions
- negative trust anchors are time-bounded, documented, auditable and automatically reviewed or expired
- response policy zones or equivalent policy mechanisms can block, redirect, sinkhole, rewrite or log selected domain names and responses
- security policies can use multiple internal and external threat-intelligence sources
- threat-intelligence sources include provenance, confidence, age, expiration and update status
- allow lists and exception policies take precedence predictably and are auditable
- policies can identify or mitigate phishing, malware, command-and-control, domain-generation algorithms, newly observed domains, DNS tunneling, data exfiltration, fast flux and suspicious DNS behavior
- detection can use query names, response data, client identity, destination, timing, volume and behavioral context
- policies support monitor-only, alert, block, redirect, sinkhole and custom-response actions
- security enforcement can continue during temporary loss of the central management or cloud control plane
- cached threat intelligence and policy data have defined freshness, fail-open and fail-closed behavior
- blocked responses preserve sufficient context for investigation and user support
- policy bypass by hard-coded external resolvers, encrypted DNS or unauthorized forwarding can be detected or controlled where within scope

### DNS Transaction and Data Protection

- zone transfers and dynamic updates support TSIG according to [RFC 8945](https://www.rfc-editor.org/rfc/rfc8945.html) or an equivalent standards-based authentication mechanism
- strong current TSIG algorithms are supported and deprecated algorithms can be disabled
- shared keys can be generated, distributed, rotated, revoked and audited centrally
- separate keys can be assigned per relationship, server, zone or purpose
- zone transfers can use TLS according to [RFC 9103](https://www.rfc-editor.org/rfc/rfc9103.html) where confidentiality is required and supported
- GSS-TSIG is supported for secure dynamic updates in Microsoft Active Directory environments
- DNS management APIs and control channels use authenticated encryption
- DNS data at rest, backups and exported configuration files can be encrypted
- exported zones, logs, packet captures and support bundles can be access-controlled and sanitized
- the integrity of zone data is checked before publication
- the platform detects unauthorized, out-of-band or unexpected changes to authoritative data
- registrar, registry, DNS-hosting and internal approval workflows can be documented and reconciled for critical domains

### DNS Monitoring, Detection and Response

- the platform provides real-time and historical visibility into DNS queries, responses, errors, latency, cache behavior and policy actions
- monitoring distinguishes authoritative, recursive, forwarding and encrypted DNS traffic
- logs include sufficient context to correlate client, source network, queried name, query type, response code, answer, policy, server and timestamp
- logging can be filtered and sampled without losing security-relevant events
- log retention and deletion can be configured by data type, tenant and legal or operational requirement
- sensitive DNS telemetry can be masked, minimized or pseudonymized
- events and telemetry can be exported using syslog and documented APIs and integrated with SIEM, SOAR, NDR and observability platforms
- alerts can be generated for anomalous query volume, error rates, latency, cache misses, NXDOMAIN spikes, SERVFAIL spikes and unusual record types
- the platform detects DNS tunneling, data exfiltration, domain-generation behavior, fast flux, cache poisoning indicators and denial-of-service conditions
- detections provide the evidence, confidence and affected clients or domains needed for investigation
- response actions can be automated through APIs, workflows or integrations while retaining approval and rollback controls
- analysts can search historical DNS activity for a domain, client, IP address, policy or time range
- packet capture or equivalent detailed diagnostics can be enabled selectively and for a limited duration
- security events preserve chain-of-custody and audit information where required
- health monitoring covers DNS service availability from the client perspective, not only process or appliance health
- recovery procedures support cache flush, policy rollback, zone restore, key recovery and controlled service isolation

### DNS Privacy and Encrypted DNS

- recursive resolvers support QNAME minimisation according to [RFC 9156](https://www.rfc-editor.org/rfc/rfc9156.html)
- DNS logging and analytics follow documented data-minimisation, retention and access-control policies
- the platform can provide a documented recursive-resolver privacy statement aligned with [RFC 8932](https://www.rfc-editor.org/rfc/rfc8932.html) where applicable
- encrypted DNS support is evaluated separately for client-to-resolver, resolver-to-resolver and resolver-to-authoritative communication
- DNS over TLS and DNS over HTTPS can be enabled for authorized clients where required
- discovery of designated encrypted resolvers can be supported where applicable
- encrypted DNS endpoints use managed certificates, strong TLS configuration and authenticated service identities
- policy, logging and troubleshooting behavior for encrypted DNS is documented
- the organization can define whether external encrypted resolvers are allowed, blocked, redirected or monitored
- encrypted DNS does not silently bypass required security controls, split DNS, internal namespaces or regulatory logging obligations
- the resolver can distinguish privacy protection from anonymity and documents which parties retain visibility into query data
- recursive-to-authoritative encryption can be supported where standards, interoperability and operational requirements permit

### Requirements for DNSSEC Management

- authoritative DNS supports DNSSEC-enabled zones and the record types required by the DNSSEC standards, including `DNSKEY`, `RRSIG`, `NSEC`, `NSEC3`, `DS`, `CDS` and `CDNSKEY`
- DNSSEC origin authentication and integrity protection are implemented in alignment with [RFC 9364](https://www.rfc-editor.org/rfc/rfc9364.html) and the applicable DNSSEC standards
- DNSSEC signing can be enabled per zone and inherited through centrally managed policies
- DNSSEC validation can be enabled per recursive server, view or policy
- validation exceptions and negative trust anchors are documented, time-bounded and audited
- NSEC and NSEC3 are supported, with configurable denial-of-existence parameters
- supported signing algorithms and key sizes are documented and can be restricted by policy
- deprecated or prohibited DNSSEC algorithms can be identified and disabled
- signing keys can be generated and stored centrally, in an HSM or through an external key-management service
- access to private keys is controlled separately from routine DNS administration
- separate KSK and ZSK operation and combined signing keys are supported where required
- signing parameters, signature validity, refresh intervals and key lifetimes can be assigned through reusable policies
- automated scheduled and emergency key rollovers are supported
- algorithm rollover is supported
- parent-side DS publication and removal can be tracked and coordinated
- CDS and CDNSKEY automation according to [RFC 8078](https://www.rfc-editor.org/rfc/rfc8078.html) is supported where accepted by the parent
- multi-signer DNSSEC according to [RFC 8901](https://www.rfc-editor.org/rfc/rfc8901.html) is supported where required
- keys can be backed up, restored, imported, exported, revoked and securely destroyed according to policy
- the system reports upcoming key, signature and trust-anchor events before they become service-affecting
- DNSSEC status is visible per zone, signer, key, algorithm, parent and validation state

### DNSSEC Validation and Deployment Safeguards

- signed zone contents and RRSIG validity are checked before publication
- DS, DNSKEY, KSK and ZSK consistency is checked before key activation or removal
- the platform detects broken, incomplete or unexpected chains of trust before and after deployment
- safeguards account for propagation delays, TTLs, signature validity and parent-zone processing time
- automated rollover workflows prevent premature removal of keys or DS records
- deployment can be staged, validated externally and rolled back safely
- independent external validation is performed for public signed zones
- alerts identify expired or near-expiry signatures, missing signatures, unsupported algorithms, stale DS records and validation failures
- DNSSEC failures can be correlated with configuration changes and key-management events
- trust-anchor distribution and rollover are managed and monitored for validating resolvers
- the platform documents implemented safeguards, operational limitations and any roadmap dependencies

# Requirements for DHCP Platform

- service instance provides high available DHCP (cluster, DHCP failover, etc.)
- IPAM instance provides access rights for all DHCP objects (hide, view, add, change, delete)
- web UI provides access DHCP logs

## Requirements for DHCP Scope Management

- IPAM instance supports management of DHCPv4 & DHCPv6 scopes
- IPAM instance supports splitting & merging DHCPv4 & DHCPv6 scopes
- IPAM instance supports moving scopes from existing DHCP server to another
- IPAM instance supports management of DHCPv4 & DHCPv6 reservations (DUID[^9])
- web UI provides real-time visibility for DHCP leases
- lease can be converted into Reservation in the web UI
- web UI provides DHCPv4 & DHCPv6 lease history
- existing leases can be deleted and freed in the web UI
- expiration or deletion of lease triggers removal of associated entities (dynamic DNS)
- service instance supports generation of hostnames for clients not sending a name
- leases can be assigned based on MAC address or client ID (`dhcp-client-identifier`)
- service instance supports one lease per client
- ping-before-assign functionality can be managed in web UI
- service instance supports legacy implementations (BOOTP, etc.)

## Requirements for DHCP Options

- IPAM instance supports management of DHCP match classes
- IPAM instance supports management of DHCPv4 options ([RFC 2132](https://www.rfc-editor.org/rfc/rfc2132.html))
- IPAM instance supports management of DHCPv6 options ([RFC 3319](https://www.rfc-editor.org/rfc/rfc3319.html))
- web UI supports management of DHCP options missing in UI (extensions)
- certain DHCPv4 option value can be changed in web UI wherever used in the system
- certain DHCPv6 option value can be changed in web UI wherever used in the system
- web UI manages of DHCP options at server, network, pool & reservation level
- web UI provides visibility for inheritance of DHCP options
- IPAM instance supports management of custom options (128  - 254)

## Requirements for DHCP Templates

- web UI provides templates for IPv4 & IPv6 networks
- web UI provides templates for IPv4 & IPv6 scopes
- web UI provides templates for IPv4 & IPv6 reservations
- changes to a template can be re-applied with linked objects

## Requirements for further DHCP Capabilities

- IPAM instance provides utilization altering for DHCP scopes (UI, mails, SNMP[^10], etc.)
- web UI provides centralized management of MAC addresses & MAC pools
- web UI provides visibility into DHCP fingerprinting details
- web UI allows access to DHCP statistics (leases per second, etc.)
- web UI provides monitoring & alarming of DHCP thresholds
- web UI supports bulk changes for DHCP reservations and & scopes

# Requirements for Address Space Management

- web UI allows management of private IPv4 address space ([RFC 1918](https://www.rfc-editor.org/rfc/rfc1918.html))
- web UI allows management of public IPv4 address space
- web UI allows management of multicast IPv4 address space (`224.0.0.0/4`)
- web UI support the allocation of next available IPv4 address range
- web UI support the allocation of next available IPv4 address network
- web UI support the allocation of next available IPv4 address
- web UI support the allocation of next available IPv4 address from offset
- web UI support the allocation of next available IPv4 address within specific range
- web UI support the management of unique local address (ULA) ranges (`fc00::/7`)
- web UI support the management of global unicast address (GUA) ranges (`2000::/3`)
- web UI support the management of multicast IPv6 ranges (`ff00::/8`)
- web UI prevents or warns about reserved address ranges (TEREDO, 6to4, etc.)
- link-local addresses (`fe80::/10`) can be documented in web UI
- web UI is able to restrict allowed subnet sizes (e.g. `/24` for IPv4, `/64` for IPv6)
- web UI support the allocation of next available IPv6 address range
- web UI support the allocation of next available IPv6 address network
- web UI support the allocation of next available IPv6 address
- web UI support the allocation of next available IPv6 address from offset
- web UI support the allocation of next available IPv6 address within specific range
- web UI support the allocation of overlapping address spaces

## Requirements for Address Space Access Rights

- IPAM instance provides access rights for all IPAM objects (hide, view, add, change, delete)
- IPAM instance provides access rights for non-allocated addresses & address ranges
- user's access rights are taken into account when searching in the web UI

## Requirements for Meta Data

- IPAM instance provides unlimited meta data (number of field per object)
- IPAM instance provides meta data for all object types (DNS, DHCP, users, etc.)
- web UI supports various values for meta data (text, integer, mail, boolean, etc.)
- meta data fields can be mandatory in the web UI
- predefined values create drop-down menus for meta data in the web UI
- drop-down menus of meta data fields can be nested
- web UI prevents invalid inputs for meta data
- web UI provides report of unused meta data definitions
- web UI provides non-DNS/DHCP-related structures (geographical, organizational, etc.)
- objects in the web UI can be tagged or grouped

## Requirements for further Address Space Capabilities

- management of DNS, DHCP & IPAM objects in the web UI is context-independent
- web UI provides a consolidated view of DNS & DHCP objects in IPAM networks
- available DNS zones per subnet can be restricted in the web UI
- networks can be structured into ranges and child ranges in the web UI
- web UI provides structuring tools (split, merge, move, resize, etc.)
- web UI allows the management of DNS & DHCP options at IPAM level
- IP addresses or ranges can be reserved for future use in the web UI
- objects can be cloned in the web UI (IPs, subnets, zones, etc.)
- dependencies of entities are linked for data consistency (device, reservation, record, etc.)
- linked entities can be accessed easily in the web UI
- networks can be moved incl. all IPs and dependencies in the web UI
- IP addresses can be moved incl. all dependencies in the web UI
- associations of AD sites can be managed in the web UI
- MAC addresses for static non-DHCP IPv4 addresses can be documented in the web UI
- web UI provides monitoring & alarming of network utilization
- web UI supports bulk changes for IP addresses, networks and ranges

## Requirements for IPv6

- web UI is accessible via IPv6 (dual-stack, native)
- API is accessible via IPv6 (dual-stack, native)
- service instance provides DNS via IPv6
- IPAM instance manages DNS via IPv6
- service instance provides DHCP via IPv6 (stateful and stateless)
- IPAM instance manages DHCP via IPv6
- web UI displays DUID[^9] and IAID[^11] for DHCPv6 clients
- web UI support management of DHCPv6 redundancy ([RFC 6853](https://www.rfc-editor.org/rfc/rfc6853.html))
- service instances can form an IPv6 cluster
- web UI allows central management of company's IPv6 prefix (given GUA[^12] of company)
- web UI supports management of dual-stack devices (multi-homed)
- web UI provides navigation between IPv4 & IPv6 information of dual-stack devices
- IPv6 networks can be linked with corresponding IPv4 networks in the web UI (1:1, 1:n & n:n associations)
- web UI provides navigation between linked IPv4 & IPv6 networks

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