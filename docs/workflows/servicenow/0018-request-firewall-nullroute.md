---
layout: page
title: Request Firewall NullRoute
permalink: /workflows/umbrella/0018-request-firewall-nullroute
redirect_from:
  - /workflows/0018
parent: ServiceNow
grand_parent: Workflows
---

# Request Firewall NullRoute
<div markdown="1">
Workflow #0018
{: .label }

Response Workflow
{: .label }
</div>

This workflow submits a change request in ServiceNow with pre-defined ticket text and the observable provided as input to the workflow. Supported observable: `ip`

[<i class="fab fa-github mr-1"></i> GitHub]({{ site.github.repository_url }}/tree/Main/Workflows/0018-ServiceNow-RequestFirewallNullRoute__definition_workflow_01N181T3IG8ZO3hpAavtoimVvrNmkjIiCuM){: .btn-cisco-outline }

---

## Change Log

| Date | Notes |
|:-----|:------|
| Apr 1, 2021 | - Initial release |
| Sep 10, 2021 | - Updated to use the new [system atomics]({{ site.baseurl }}/atomics/system) |

_See the [Important Notes]({{ site.baseurl }}/notes) page for more information about updating workflows_

---

## Requirements
* The following [system atomics]({{ site.baseurl }}/atomics/system) are used by this workflow:
	* None
* The following atomic actions must be imported before you can import this workflow:
	* ServiceNow - Create Change Request ([CiscoSecurity_Atomics]({{ site.baseurl }}/configuration))
* The [targets](#targets) and [account keys](#account-keys) listed below
* ServiceNow

---

## Workflow Steps
1. Make sure the observable type provided is supported
1. Calculate the ticket start and end time (defaults to three days from now from 2-5 AM eastern time)
1. Create the change request in ServiceNow

---

## Configuration
* Update the input variables on the `ServiceNow - Create Change Request` activity with your change request contents
* Update the activities in the `Calculate Dates` group if you want to adjust the timeframe the change ticket is requested for
* If you want to change the name of this workflow in the pivot menu, change its display name

---

## Targets
Target Group: `Default TargetGroup`

| Target Name | Type | Details | Account Keys | Notes |
|:------------|:-----|:--------|:-------------|:------|
| ServiceNow | HTTP Endpoint | _Protocol:_ `HTTPS`<br />_Host:_ `<instance>.service-now.com`<br />_Path:_ `/api` | ServiceNow_Credentials | Be sure to use your instance URL |

---

## Account Keys

| Account Key Name | Type | Details | Notes |
|:-----------------|:-----|:--------|:------|
| ServiceNow_Credentials | HTTP Basic Authentication | _Username:_ ServiceNow User ID<br />_Password:_ ServiceNow Password | |
