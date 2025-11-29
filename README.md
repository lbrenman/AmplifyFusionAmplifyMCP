# Amplify Fusion Amplify MCP

An MCP Server implemented in [Amplify Fusion](https://docs.axway.com/bundle/amplify_integration/page/docs/index.html) for interacting with [Amplify Central and Engage](https://docs.axway.com/category/platform).

Supported use cases include:
* List/Approve pending Amplify Marketplace product subscription request. [Demo video](https://youtu.be/S9oTX9gWYmw)
* List/Approve pending Amplify Marketplace application registration request
* Retrieve API Metrics for analysis
* List Marketplace products
* Create/Update Marketplace product documentation. [Demo video](https://youtu.be/HFuLi2XcSKQ)
* Create/Update Marketplace product icon

## Current MCP Server Tools

* **GetAmplifyMarketplacePendingProductSubscriptions** - Get Amplify marketplace pending subscription requests
* **UpdateAmplifyMarketplacePendingProductSubscription** - Updated Amplify marketplace pending subscription request to approved or rejected

* **GetAmplifyMarketplacePendingApplicationRegistrations** - Get Amplify marketplace pending application registration requests
* **UpdateAmplifyMarketplacePendingApplicationRegistration** - Updated Amplify marketplace pending application registration request to approved or rejected

* **GetAmplifyAPIMetrics**	- Get Engage Business Insights (API Metrics) by duration

* **GetAmplifyMarketplaceProducts** - Get a list of your marketplace products
* **GetAmplifyMarketplaceProductDetails** - Get Amplify Marketplace product details by product name. Used by UpdateAmplifyMarketplaceProductDocumentation to create documentation
* **UpdateAmplifyMarketplaceProductDocumentation** - Update product documentation. Use product name and markdown contents to update the product
* **UpdateAmplifyMarketplaceProductIcon** - Update product icon. Uses OpenAI API image generation which requires OpenAI API organization validation

* **WhatCanFusionAmplifyMCPServerDo** - What can Fusion Amplify MCP Server do. What capabilities and features does this MCP have

## Setup

Prerequisites:
* Amplify Service Account client id and secret with the following Roles:
  * Administrator
  * Engage Admin
* OpenAI API Token (for creating product icon)

Steps to install:
* Export project zip file and import in your Amplify Fusion tenant
* Create and set an Environment property, AMPLIFY_APICENTRAL_BASE_URL to https://apicentral.axway.com, https://central.eu-fr.axway.com or https://central.ap-sg.axway.com depending on your region
* Go to connector override in Manager and enter you credentials for the connectors
* Optionally set your security (eg. api key)
* Activate your MCP Server and get the URL
* Configure your LLM to use the MCP Server URL