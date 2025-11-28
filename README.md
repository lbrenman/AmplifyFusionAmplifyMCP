# Amplify Fusion Amplify MCP

An MCP Server implemented in Amplify Fusion for interacting with Amplify Central and Engage.

Supported use cases include:
* List/Approve pending Amplify Marketplace product subscription requests. [Demo video](https://youtu.be/S9oTX9gWYmw)
* List/Approve pending Amplify Marketplace application registration requests
* Retrieve API Metrics for analysis
* List Marketplace products
* Create/Update Marketplace product documentation. [Demo video](https://youtu.be/HFuLi2XcSKQ)
* Create/Update Marketplace product icon

## Current MCP Server Tools

* GetAmplifyMarketplacePendingSubscriptions - Get Amplify marketplace pending subscription requests
* UpdateAmplifyMarketplacePendingSubscriptions - Updated Amplify marketplace pending subscription requests to approved or rejected
* GetAmplifyMarketplacePendingApplicationRegistrations -  - Get Amplify marketplace pending application registration requests
* UpdateAmplifyMarketplacePendingApplicationRegistrations - Updated Amplify marketplace pending application registration requests to approved or rejected
* GetAPIMetrics	- Get Engage Business Insights (API Metrics) by duration
* GetMarketplaceProducts - Get a list of your marketplace products
* UpdateProductDocumentation - Update product documentation. Use product name and markdown contents to update the product
* UpdateProductIcon - Update product icon. Uses OpenAI image generation which requires organization validation

## Setup

Prerequisites:
* Amplify Service Account client id and secret with the following Roles:
  * Administrator
  * Engage Admin
* OpenAI API Token (for creating product icon)

Steps to install:
* Export project zip file and import in your Amplify Fusion tenant
* Go to connector override in Manager and enter you credentials for the connectors
* Optionally set your security (eg. api key)
* Activate your MCP Server and get the URL
* Configure your LLM to use the MCP Server URL