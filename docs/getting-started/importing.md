---
layout: page
title: Importing Git Content
permalink: /importing
parent: Getting Started
nav_order: 15
---

# Importing Git Content
Using the Git repositories configured in Orchestration, you can import a wide variety of content published by Cisco.

[<i class="fa fa-video mr-1"></i> Import and Export](https://www.youtube.com/watch?v=qmJk994qLOg&list=PLPFIie48Myg2tu2gHbgm-moYg8LDaXsSo){: .btn-cisco-outline }

---

**Note on the "Import as a New Workflow (Clone)" Checkbox**

When importing workflows and atomic actions, you'll see a checkbox labeled: **Import as a New Workflow (Clone)**. If you're trying to import an object that already exists, you need to be careful whether or not you check this box.

If you're importing something that **already exists** and:
* The box is **checked**: A copy of the object will be made.
* The box is **NOT checked**: You will be asked if you want to overwrite the existing object. This cannot be undone and any changes made to a workflow will be lost if you overwrite it.

---

## Importing from GitHub
The process for importing workflows and atomic actions is exactly the same. The only different is which Git repository you select since we keep workflows in one folder and atomic actions in another.

1. On your **Workflows** page, click the **Import** button (next to the **New Workflow** button)
1. Select the **Git Repository** you want to import content from. If you followed our [configuration instructions]({{ site.baseurl }}/configuration), you should select:
	* `CiscoSecurity_Workflows` for workflows
	* `CiscoSecurity_Atomics` for atomic actions
	* Note: You can have other GitHub repositories, so feel free to select whichever repository you intend to import content from!
1. Once the **Filename** list loads, look for the item you want to import and select it
1. Next, the **Git Version** list will populate. Select the version of the item you want to import (you'll usually want the latest version)
1. If applicable, check the **Import as a New Workflow (Clone)** box (see note above)
1. Click the **Import** button
1. If the workflow contains `Secure Strings`, you may be asked to provide their values during import. If you don't have the values handy, you can provide placeholder values and update them later

---

## Importing from Text or a File
If you want to import a workflow that's not committed to GitHub, you can simply copy/paste its definition JSON into SecureX orchestration or import it from a file (containing the workflow definition JSON).

1. On your **Workflows** page, click the **Import** button (next to the **New Workflow** button)
1. Under the **Import From** heading, select the **Browse** tab
1. If you have a workflow's JSON to import, you can paste it into the box. If the workflow JSON is in a file, click **Browse** and select the file
1. If applicable, check the **Import as a New Workflow (Clone)** box (see note above)
1. Click the **Import** button
1. If the workflow contains `Secure Strings`, you may be asked to provide their values during import. If you don't have the values handy, you can provide placeholder values and update them later