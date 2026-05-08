# Request for stronger DNSSEC validation and rollover safeguards

Hello,

recent [DNSSEC incidents](https://blog.denic.de/en/denic-reports-dnssec-disruption-affecting-de-domains/) have again shown how critical robust DNSSEC handling is, especially around key rollovers, signature validity and deployment validation.

We would like to understand how your DDI platform currently helps prevent DNSSEC related outages and what improvements are planned in this area.

Could you please verify internally and share your position on the following points:
* Support for [RFC 8901](https://datatracker.ietf.org/doc/rfc8901/), if applicable to your DNSSEC roadmap
* Enhanced DS validation before ZSK or KSK material is removed from zones
* Validation of RRSIG availability and correctness as part of the deployment process
* Built in safeguards to detect DNSSEC inconsistencies before they become service impacting
* Roadmap items for reducing dependency on manual checks, user driven monitoring and human remediation

The concern is that DNSSEC remains technically fragile when safeguards are not implemented end to end. A DNSSEC failure can make entire domains, and in some cases even larger namespaces, unavailable. For that reason, we need to understand which technical protection mechanisms exist today and which ones are planned.

As a DDI vendor, we would expect the platform to provide strong validation, automation and preventive controls in this area. DNSSEC should not rely primarily on human validation or operational workarounds after an issue has already occurred.

Please let us know whether these capabilities already exist, are planned, or should be raised as a formal product requirement. If no matching roadmap item exists yet, we ask that one be created and prioritized accordingly.

Thank you.
