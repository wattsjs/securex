## Overview
This SecureX workflow allows you to syncronise your existing sanctioned applications in Microsoft Defender for Cloud Apps (formally known as MCAS) with an Umbrella DNS destination list.

Microsoft provides a REST API of all domains associated with your sanctioned applications, and this workflow will syncronise these domains with a destination list in Cisco Umbrella - allowing you to block access to these sanctioned applications at a DNS level across your entire organisation.

<!-- GETTING STARTED -->
## Getting Started

### Prerequisites

This is an example of how to list things you need to use the software and how to install them.
* Microsoft Defender for Cloud Apps subscription
  * If you do not have access to this (for example for development purposes), Microsoft provides free access via their [Microsoft 365 Developer Program](https://docs.microsoft.com/en-us/office/developer-program/microsoft-365-developer-program)
* Cisco Umbrella DNS subscription
### Installation

1. [Create an application context that will be used to access the Defender for Cloud Apps API](https://docs.microsoft.com/en-us/defender-cloud-apps/api-authentication-application)
   1. Keep note of your `TENANT_ID`, `CLIENT_ID`, and `CLIENT_SECRET`
   2. You will need to provision the application with the `Discovery.read` permission scope
2. [Make a note of the API URL Structure for your Defender for Cloud Apps tenant](https://docs.microsoft.com/en-us/defender-cloud-apps/api-introduction#api-url-structure)
   1. This will most likely be in the form of `https://XXXX.XX.portal.cloudappsecurity.com`
3. Ensure you have [created management API keys for your Cisco Umbrella tenant](https://developer.cisco.com/docs/cloud-security/#getting-started-overview/generate-an-api-key)
   1. Keep a note of your `MANAGEMENT_API_KEY`, `MANAGEMENT_API_SECRET`
   2. Your `ORG_ID` is a 7 digit number that is found in your Cisco Umbrella URL path in the format `https://dashboard.umbrella.com/o/{YOUR_ORG_ID}/`
4. Import the workflow into your SecureX Orchestration instance
   1. The simplest way is to manually import [this workflow](https://raw.githubusercontent.com/wattsjs/securex/main/workflows/Umbrella-SyncMicrosoftDefenderForCloudApps__definition_workflow_01ZA78KI6QSLC6gcXhudQZDRoakc3qqNwkC/definition_workflow_01ZA78KI6QSLC6gcXhudQZDRoakc3qqNwkC.json) into your SecureX Orchestration instance via the `Import Workflow` button in the dashboard, then select the `Browse` tab and paste the contents of the json workflow file
   2. Alternatively, you may [setup this repository as a Git Repo](https://ciscosecurity-sx-00-integration-workflows.readthedocs-hosted.com/en/latest/orchestration/import_export.html#importing-from-git) inside your SecureX instance in order to enable future updates
6. Configure the relevant workflow variables according to the values noted earlier for `CLIENT_ID`, `CLIENT_SECRET`, `PORTAL_URL`, `TENANT_ID`, `UMBRELLA_MANAGEMENT_KEY`, `UMBRELLA_MANAGEMENT_SECRET`, and `UMBRELLA_ORG_ID`



<!-- USAGE EXAMPLES -->
## Usage

The workflow will be automatically configured to run on a trigger at a scheduled interval of 30 minutes. This means that every 30 minutes - SecureX will perform the syncronisation between the platforms and there may be a delay between updating an application's status in Defender for Cloud Apps and any enforcement from Cisco Umbrella.

In order to enforce the blocking of these domains, you will need to use the destination list within an Umbrella DNS policy. By itself - the destination list will be do anything until it is included within a policy.

<!-- CONTACT -->
## Contact
Any questions related to this workflow you can reach out to me at:

Jamie Watts - jamiwatt@cisco.com
