---
layout: page
title: Quarantine AWS Instances from Alerts
permalink: /workflows/secure-cloud-analytics/0006-quarantine-aws-from-alert
redirect_from:
  - /workflows/sca/0006-quarantine-aws-from-alert
  - /workflows/0006
parent: Cisco Secure Cloud Analytics
grand_parent: Workflows
---

# Quarantine AWS Instances from Alerts
<div markdown="1">
Workflow #0006
{: .label }
</div>

This workflow fetches `Geographically Unusual Remote Access` alerts from the Cisco Secure Cloud Analytics (SCA) API for the past hour. Then, for each of those alerts, it attempts to locate a matching Amazon Web Services (AWS) instance and restrict SSH access to its security group. Notifications are sent using Webex Teams and an approval is requested to lift the quarantine restrictions.

**Note:** To automate handling of the approval tasks generated by this workflow, be sure to also import [this workflow]({{ site.baseurl }}/workflows/secure-cloud-analytics/0007-handle-aws-ssh-quarantine-approvals)!

[<i class="fab fa-github mr-1"></i> GitHub]({{ site.github.repository_url }}/tree/Main/Workflows/0006-SCA-QuarantineAWSInstancesFromAlerts__definition_workflow_01KB7F57QJWPF4vcfJy8tJXanOHelboFJVl/){: .btn-cisco-outline }

---

## Change Log

| Date | Notes |
|:-----|:------|
| Nov 20, 2020 | - Initial release |
| Sep 10, 2021 | - Updated to use the new [system atomics]({{ site.baseurl }}/atomics/system) |

_See the [Important Notes]({{ site.baseurl }}/notes) page for more information about updating workflows_

---

## Requirements
* The following [system atomics]({{ site.baseurl }}/atomics/system) are used by this workflow:
	* SCA - Get Alerts
	* Webex Teams - Post Message to Room
	* Webex Teams - Search for Room
* The following atomic actions must be imported before you can import this workflow:
	* None
* The [targets](#targets) and [account keys](#account-keys) listed below
* (Optional) A Webex Teams access token and room name to post messages to
* Cisco Secure Cloud Analytics (SCA)
* Amazon Web Services (AWS)

---

## Workflow Steps
1. Fetch global variables
1. Calculate the time 1 hour ago
1. Fetch `Geographically Unusual Remote Access` alerts from SCA for that time frame
1. Convert the alerts to a table
1. If a Webex Teams room name was provided, translate it into a room ID
1. For each alert in the table:
	* Check if the instance was already quarantined (if so, skip it)
	* Get information about the instance from AWS and extract its security group
	* Revoke SSH access to the group and add an exception for the CIDR network in the local variable
	* Create an approval request to remove the instance from quarantine
	* Send a Webex Teams notification

---

## Configuration
* Make sure `Default TargetGroup` includes the `AWS Endpoint` target type ([more info]({{ site.baseurl }}/targets/groups))
* Set your AWS region in the `AWS Region` local variable
* Add the CIDR network you want to exclude from SSH restrictions in the `CIDR IP to Exclude` local variable (so you can still get into the instance to fix it)
* Add your Secure Cloud Analytics API key to the `Secure Cloud Analytics API Key` local variable (or, if you have an API key in a global variable already, set the local variable to the global's value using the `Fetch Global Variables` group at the beginning of the workflow)
* The `Approval request to undo AWS SSH quarantine` activity needs to be configured with a task requestor, owner, and assignees (the assignees will be able to approve or deny)
* **Important:** Do not change the `Subject Line` of the approval task or the approval event trigger will stop working
* See [this page]({{ site.baseurl }}/atomics/configuration/webex#configuring-our-workflows) for information on configuring the workflow for Webex Teams

---

## Targets
Target Group: `Default TargetGroup`

| Target Name | Type | Details | Account Keys | Notes |
|:------------|:-----|:--------|:-------------|:------|
| Amazon Web Services | AWS Endpoint | _Region:_ `Your Region`<br /> | Your AWS Account Key (see below) | |
| Secure Cloud Analytics | HTTP Endpoint | _Protocol:_ `HTTPS`<br />_Host:_ `your-tenant.obsrvbl.com`<br />_Path:_ `api` | None | |
| Webex Teams | HTTP Endpoint | _Protocol:_ `HTTPS`<br />_Host:_ `webexapis.com`<br />_Path:_ None | None | Not necessary if Webex Teams activities are removed |

---

## Account Keys

| Account Key Name | Type | Details | Notes |
|:-----------------|:-----|:--------|:------|
| Your AWS Account Key | AWS Credentials | _Access Key:_ AWS API Access Key<br />_Secret Key:_ AWS API Secret Key | |
