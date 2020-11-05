---
layout: page
title: Best Practices
permalink: /workflows/best-practices
parent: Workflows
---

# Best Practices
The following best practices should be followed when building a workflow.

---

## Overall
* Name the workflow something meaningful.
* Provide a detailed description. For example:

```text
This workflow takes a Talos blog post, conducts an investigation into it using Cisco Threat Response, and then puts the results in a casebook. If a Webex Teams room name and bot token are provided, a message with the investigation's results will be sent.

Target Group: Default TargetGroup

Targets Used: CTR_For_Access_Token, CTR_API, Private_CTIA_Target, Webex Teams

Steps:
[] Fetch the blog post content and strip out any HTML
[] Request a CTR access token and inspect the blog post content for observables
[] Loop through each observable and get its CTR disposition
[] For observables that weren't clean, conduct CTR enrichment to get sightings
[] For modules with sightings, build the text to post to Webex
[] Create the CTR casebook and, if a teams room is provided, post a message to Webex
```

## Variables
* Give all of your variables (input, output, and local) meaningful names and descriptions. In our workflows, we typically use formal variable names like: `Variable Name`. Descriptions should include information about the variable's purpose and useful hints about possible values.
* Make input variables required if the workflow will fail to function if the variables are left blank.
* For numeric variables, provide an appropriate default value.
* Use `Secure Strings` for sensitive values such as API keys, passwords, or other credentials that should be hidden from view.
* When using date/time stamps, try to use the actual `Date Time` variable type where possible, especially for input and output variables. You can always use the `Format Date` and `Parse Date` activities to convert to/from strings.

## Targets
* Workflows should use Target Groups where possible to make them more portable. See [this page](/workflows/target-groups) for more information.

## Account Keys
* Workflows and their activities should use their targets' default account keys whenever possible. As in, account keys should be defined as part of the target's configuration. Overriding a target's account keys within a workflow is uncommon.