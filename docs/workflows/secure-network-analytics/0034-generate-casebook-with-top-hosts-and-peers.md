---
layout: page
title: Generate Casebook with Top Hosts and Peers
permalink: /workflows/secure-network-analytics/0034-generate-casebook-with-top-hosts-and-peers
redirect_from:
  - /workflows/0034
parent: Cisco Secure Network Analytics
grand_parent: Workflows
---

# Generate Casebook with Top Hosts and Peers
<div markdown="1">
Workflow #0034
{: .label }

Response Workflow
{: .label }
</div>

This workflow fetches the top 10 hosts and peers that communicated with the IP address pivoted on from Cisco Secure Network Analytics (SNA). The lists of IPs are then added to a SecureX casebook. Supported observable: `ip`

Hint: If you want to change the name of this workflow in the pivot menu, change its display name.

[<i class="fab fa-github mr-1"></i> GitHub]({{ site.github.repository_url }}/tree/Main/Workflows/0034-SNA-GenerateCasebookWithTopHostsAndPeers__definition_workflow_01OOGJEF9CEVE5ssyxxdxK11rd8d3SSbQOR){: .btn-cisco-outline }

---

## Change Log

| Date | Notes |
|:-----|:------|
| Jun 17, 2021 | - Initial release |
| Sep 10, 2021 | - Updated to use the new [system atomics]({{ site.baseurl }}/atomics/system) |

_See the [Important Notes]({{ site.baseurl }}/notes) page for more information about updating workflows_

---

## Requirements
* The following [system atomics]({{ site.baseurl }}/atomics/system) are used by this workflow:
	* SNA - Get Tenants
	* SNA - Get Tokens
	* SNA - Get Top Hosts by IP Address
	* SNA - Get Top Peers by IP Address
	* Threat Response - Create Casebook
	* Threat Response - Generate Access Token
* The following atomic actions must be imported before you can import this workflow:
	* None
* The [targets](#targets) and [account keys](#account-keys) listed below
* A [SecureX orchestration remote]({{ site.baseurl }}/remote) with connectivity to your Secure Network Analytics instance
* Cisco Secure Network Analytics (SNA)

---

## Workflow Steps
1. Make sure the observable type provided is supported
1. Fetch global variables
1. Calculate date 24 hours ago
1. Get Secure Network Analytics tokens and tenant information
1. Fetch and parse the top peers
1. Fetch and parse the top hosts
1. Make sure at least one of the queries returned data
1. Create a casebook in SecureX

---

## Configuration
* Add your Secure Network Analytics API username and password to `SNA Username` and `SNA Password` (or, if you have them stored in global variables, use the `Fetch Global Variables` group at the beginning of the workflow to update the local variables)
* Set the `SNA Tenant Name` to the name of the tenant you want to work in
* If you want to change the name of this workflow in the pivot menu, change its display name

---

## Targets
**Note:** If your Secure Network Analytics deployment is on-premises and not accessible from the internet, you will need a [SecureX orchestration remote]({{ site.baseurl }}/remote) to use it with orchestration.

Target Group: `Default TargetGroup`

| Target Name | Type | Details | Account Keys | Notes |
|:------------|:-----|:--------|:-------------|:------|
| [CTR_For_Access_Token]({{ site.baseurl }}/targets/default#ctr_for_access_token) | HTTP Endpoint | _Protocol:_ `HTTPS`<br />_Host:_ `visibility.amp.cisco.com`<br />_Path:_ `/iroh` | CTR_Credentials | Created by default |
| [Private_CTIA_Target]({{ site.baseurl }}/targets/default#private_ctia_target) | HTTP Endpoint | _Protocol:_ `HTTPS`<br />_Host:_ `private.intel.amp.cisco.com`<br />_Path:_ None | None | Created by default |
| Secure Network Analytics | HTTP Endpoint | _Protocol:_ `HTTPS`<br />_Host:_ `your-sna-management-center.yourdomain`<br />_Path:_ None | None | |

---

## Account Keys

| Account Key Name | Type | Details | Notes |
|:-----------------|:-----|:--------|:------|
| [CTR_Credentials]({{ site.baseurl }}/account-keys/default#ctr_credentials) | HTTP Basic Authentication | _Username:_ Client ID<br />_Password:_ Client Secret | Created by default |
