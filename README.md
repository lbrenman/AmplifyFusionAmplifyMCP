# Amplify Fusion Amplify MCP

An MCP Server for interacting with [Amplify Central and Engage](https://docs.axway.com/category/platform) implemented in [Amplify Fusion](https://docs.axway.com/bundle/amplify_integration/page/docs/index.html).

Supported use cases include:
* List/Approve pending Amplify Marketplace product subscription request. [Demo video](https://youtu.be/S9oTX9gWYmw)
* List/Approve pending Amplify Marketplace application registration request

* List Marketplace products
* Create/Update Marketplace product documentation. [Demo video](https://youtu.be/HFuLi2XcSKQ)
* Create/Update Marketplace product icons

* List APIs by Design Compliance Linting Grades
* Get detailed linting results
* Get API specification for LLM to assist in improving


## Current MCP Server Tools
* General
  * **WhatCanFusionAmplifyMCPServerDo** - What can Fusion Amplify MCP Server do. What capabilities and features does this MCP have
* Product Subscription/Application Registration Request Tools
  * **GetAmplifyMarketplacePendingProductSubscriptions** - Get Amplify marketplace pending subscription requests
  * **UpdateAmplifyMarketplacePendingProductSubscription** - Updated Amplify marketplace pending subscription request to approved or rejected
  * **GetAmplifyMarketplacePendingApplicationRegistrations** - Get Amplify marketplace pending application registration requests
  * **UpdateAmplifyMarketplacePendingApplicationRegistration** - Updated Amplify marketplace pending application registration request to approved or rejected
* Product Tools
  * **GetAmplifyMarketplaceProducts** - Get a list of your marketplace products
  * **GetAmplifyMarketplaceProductDetails** - Get Amplify Marketplace product details by product name. Used by UpdateAmplifyMarketplaceProductDocumentation to create documentation
  * **UpdateAmplifyMarketplaceProductDocumentation** - Update product documentation. Use product name and markdown contents to update the product
  * **UpdateAmplifyMarketplaceProductIcon** - Update product icon. Uses OpenAI API image generation which requires OpenAI API organization validation
  * **ActivateAmplifyMarketplaceProduct** - Activate an amplify marketplace product based on product name and release type. Use product name from GetAmplifyMarketplaceProducts tool. Release type is major, minor or patch. Default is patch
* API Tools
  * **GetAmplifyAPIMetrics**	- Get Engage Business Insights (API Metrics) by duration
  * **LintingResultsByGrade** - Provides linting/design compliance results grouped by across all the APIs. Just the grade numbers are provided
  * **ListAPIsForDesignLintingGrade** - Retrieves a list of all the apis and their linting/design compliance results for a specific design linting grade
  * **APIDetailedLintingResults** - Retrieves the detailed lintingdesign compliance results for an API providing the API ID
  * **GetAPISpecificationForAPI** - 	Retrieves the Open API/Swagger Specification for a specific API providing the API ID

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

## Prompts

---

### Marketplace Product Management

#### Viewing Products & Details

| Prompt | Tool Used |
|--------|-----------|
| "Get my marketplace products" | `GetAmplifyMarketplaceProducts` |
| "List all marketplace products" | `GetAmplifyMarketplaceProducts` |
| "Get products" | `GetAmplifyMarketplaceProducts` |
| "What products are in my marketplace?" | `GetAmplifyMarketplaceProducts` |
| "Get product translate" | `GetAmplifyMarketplaceProductDetails` |
| "Get my products and put in a table" | `GetAmplifyMarketplaceProducts` |
| "Get details for the Translate product" | `GetAmplifyMarketplaceProductDetails` |

#### Updating Product Documentation

| Prompt | Tool Used |
|--------|-----------|
| "Update product documentation for product: Translate. Documentation should be very brief. 10 lines max" | `UpdateAmplifyMarketplaceProductDocumentation` |
| "Update the documentation for the Translate API" | `UpdateAmplifyMarketplaceProductDocumentation` |

#### Updating Product Icons

| Prompt | Tool Used |
|--------|-----------|
| "Update icon for product Translate. Make it brick red, square with rounded corners and a drop shadow. Have it connote language translation" | `UpdateAmplifyMarketplaceProductIcon` |
| "Update the icons for all my products. For each use a different color from a nice modern color palette of your choosing. Each icon should be square, with rounded corners and have a drop shadow. Each icon should have a transparent background and be 100 pixels by 100 pixels. In each icon place a pictogram that related to the product title." | `UpdateAmplifyMarketplaceProductIcon` (called multiple times) |
| "Please redo stock watchlist mcp so it looks more similar to fusion finance in style" | `UpdateAmplifyMarketplaceProductIcon` |

#### Activating Products

| Prompt | Tool Used |
|--------|-----------|
| "Activate the Translate product" | `ActivateAmplifyMarketplaceProduct` |

---

### Subscription Management

#### Viewing Pending Subscriptions

| Prompt | Tool Used |
|--------|-----------|
| "Get marketplace product subscriptions" | `GetAmplifyMarketplacePendingProductSubscriptions` |
| "Get amplify marketplace product subscriptions" | `GetAmplifyMarketplacePendingProductSubscriptions` |
| "Do I have any marketplace product subscription requests?" | `GetAmplifyMarketplacePendingProductSubscriptions` |
| "Are there any pending marketplace subscriptions?" | `GetAmplifyMarketplacePendingSubscriptions` |
| "What pending product subscriptions do I have?" | `GetAmplifyMarketplacePendingProductSubscriptions` |
| "Get my marketplace product subscription requests" | `GetAmplifyMarketplacePendingProductSubscriptions` |

#### Approving/Rejecting Subscriptions

| Prompt | Tool Used |
|--------|-----------|
| "Approve the Translate API Silver Plan subscription" | `UpdateAmplifyMarketplacePendingProductSubscription` |
| "Approve" (in response to pending subscription) | `UpdateAmplifyMarketplacePendingProductSubscription` |
| "Approve Fusion Finance - Free Plan" | `UpdateAmplifyMarketplacePendingProductSubscription` |
| "Approve with reason 'good luck with your application'" | `UpdateAmplifyMarketplacePendingProductSubscription` |

---

### Application Registration Management

#### Viewing Pending Application Registrations

| Prompt | Tool Used |
|--------|-----------|
| "What application requests are there?" | `GetAmplifyMarketplacePendingApplicationRegistrations` |
| "Get amplify marketplace pending application registrations" | `GetAmplifyMarketplacePendingApplicationRegistrations` |

#### Approving/Rejecting Application Registrations

| Prompt | Tool Used |
|--------|-----------|
| "Approve the application registration" | `UpdateAmplifyMarketplacePendingApplicationRegistration` |
| "Reject the application registration with reason 'Does not meet requirements'" | `UpdateAmplifyMarketplacePendingApplicationRegistration` |

---

### API Management & Analysis

#### API Linting & Quality

| Prompt | Tool Used |
|--------|-----------|
| "Get my linting results by grade" | `LintingResultsByGrade` |
| "Get my apis for linting grade D" | `GetAPIsForDesignLintingGrade` |
| "Get my marketplace apis by linting grade C" | `GetAPIsForDesignLintingGrade` |
| "Get linting results for api translate" | `GetDetailedLintingResultsForAPI` |
| "Get linting results for Rekognition" | `GetDetailedLintingResultsForAPI` |
| "Get linting results for the Comprehend API" | `GetDetailedLintingResultsForAPI` |

#### API Specifications

| Prompt | Tool Used |
|--------|-----------|
| "Get api spec for translate" | `GetAPISpecificationForAPI` |
| "Get api spec for Comprehend" | `GetAPISpecificationForAPI` |
| "Get the OpenAPI specification for the Translate API" | `GetAPISpecificationForAPI` |

#### API Metrics & Performance

| Prompt | Tool Used |
|--------|-----------|
| "Get API performance metrics for the last 6 months" | `GetAmplifyAPIMetrics` |
| "Get my API performance metrics" | `GetAmplifyAPIMetrics` |
| "Compare my API metrics from last week to last year" | `GetAmplifyAPIMetrics` |

---

### Server Information & Capabilities

| Prompt | Tool Used |
|--------|-----------|
| "What can Fusion Amplify MCP Server do?" | `WhatCanFusionAmplifyMCPServerDo` |
| "What can fusion MCP server do?" | `WhatCanFusionAmplifyMCPServerDo` |
| "What capabilities does the Fusion Amplify MCP Server provide?" | `WhatCanFusionAmplifyMCPServerDo` |