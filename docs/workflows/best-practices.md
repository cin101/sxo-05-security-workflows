---
layout: page
title: Best Practices
permalink: /workflows/best-practices
parent: Workflows
nav_order: 10
---

# Best Practices
The following best practices should be followed when building a workflow.

[<i class="fa fa-video mr-1"></i> Building a Workflow](https://www.youtube.com/watch?v=gs-XWrCXQbE&list=PLPFIie48Myg2tu2gHbgm-moYg8LDaXsSo){: .btn-cisco-outline }

<div class="cisco-alert cisco-alert-info"><i class="fa fa-info-circle mr-1 cisco-icon-info"></i> Want to see how well your workflow adheres to our standards? Try the new <a href="{{ site.baseurl }}/analyzer/">Workflow Analyzer</a></div>

---

## Overall
* Name the workflow something meaningful.
* Provide a detailed description. For example:

```text
This workflow takes a Talos blog post, conducts an investigation into it using Threat Response, and then puts the results in a casebook. If a Webex Teams room name and bot token are provided, a message with the investigation's results will be sent.

Target Group: Default TargetGroup

Targets Used: CTR_For_Access_Token, CTR_API, Private_CTIA_Target, Webex Teams

Steps:
[] Fetch the blog post content and strip out any HTML
[] Request a Threat Response access token and inspect the blog post content for observables
[] Loop through each observable and get its Threat Response disposition
[] For observables that weren't clean, conduct Threat Response enrichment to get sightings
[] For modules with sightings, build the text to post to Webex
[] Create the SecureX casebook and, if a teams room is provided, post a message to Webex
```

* Be mindful of how you handle errors:
	* If an error occurs that prevents a workflow from continuing, it's best to use a `Completed` activity to fail the workflow and return a descriptive error.
	* If an error occurs that can be ignored, either make note of the error so you can inform someone at the end of the workflow or ignore it.
* Workflows should have a clear purpose and a user should be able to walk through a workflow and understand what it's doing.

### Notes Specific to Working with Infrastructure
* Workflows should be predictable and make easily quantifiable changes to infrastructure. For example, if the workflow tries to add an object to a group and the group doesn't exist, you may attempt to create that group. However, you should not attempt to create a *different* group as that's not a predictable change.
* The user should always be able to understand in advance what a workflow is capable of changing in their infrastructure. Many large enterprises require change control or pre-approved standard changes and being able to explain the nature of potential changes is crucial.

---

## Variables
* Give all of your variables (input, output, and local) meaningful names and descriptions. In our workflows, we typically use formal variable names like: `Variable Name`. Descriptions should include information about the variable's purpose and useful hints about possible values.
* Make input variables required if the workflow will fail to function if the variables are left blank.
* If a local variable is necessary for a workflow to function, check that is isn't blank and fail the workflow if it is.
* For numeric variables, provide an appropriate default value.
* Use `Secure Strings` for sensitive values such as API keys, passwords, or other credentials that should be hidden from view.
* When using date/time stamps, try to use the actual `Date Time` variable type where possible, especially for input and output variables. You can always use the `Format Date` and `Parse Date` activities to convert to/from strings.

---

## Targets
* Workflows should use Target Groups where possible to make them more portable. See [this page]({{ site.baseurl }}/targets/groups) for more information.

---

## Account Keys
* Workflows and their activities should use their targets' default account keys whenever possible. As in, account keys should be defined as part of the target's configuration. Overriding a target's account keys within a workflow is uncommon.