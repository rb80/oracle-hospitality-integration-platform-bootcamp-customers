# Basic Setup

Getting started with Oracle Hospitality Integration Platform is easy.  Follow these steps.

- [Basic Setup](#basic-setup)
  - [0. Objective](#0-objective)
  - [1. Accessing the Developer Portal](#1-accessing-the-developer-portal)
  - [1a. Accessing the Developer Portal as a Customer on SSD (Resource Owner)](#1a-accessing-the-developer-portal-as-a-customer-on-ssd-resource-owner)
  - [1b. Accessing the Developer Portal as a Customer on OCIM (Client Credentials)](#1b-accessing-the-developer-portal-as-a-customer-on-ocim-client-credentials)
  - [2. Understanding the Developer Portal](#2-understanding-the-developer-portal)
    - [2a. Finding APIs and workflows (optional)](#2a-finding-apis-and-workflows-optional)
    - [2b. Creating an application](#2b-creating-an-application)
  - [3. Obtaining credentials](#3-obtaining-credentials)
  - [4. Authentication Flows (background)](#4-authentication-flows-background)
  - [5. Setting up Postman](#5-setting-up-postman)
    - [5a. Postman Environment variables for a Client Credentials (OCIM) environment](#5a-postman-environment-variables-for-a-client-credentials-ocim-environment)
    - [5b. Postman Environment variables for a Resource Owner (SSD) environment](#5b-postman-environment-variables-for-a-resource-owner-ssd-environment)
  - [6. Obtaining an oAuth token](#6-obtaining-an-oauth-token)
  - [7. Calling the getHotelDetails API](#7-calling-the-gethoteldetails-api)
  - [8. Finding the OPERA version of the environment (Optional)](#8-finding-the-opera-version-of-the-environment-optional)
  - [9. View analytics](#9-view-analytics)

## 0. Objective

After completing this lab you will have:

1. Become familiar with the OHIP developer portal
2. Created an application in the OHIP developer portal
3. Set up Postman
4. Obtained an oAuth token
5. Called two Oracle Hospitality APIs
6. Viewed analytics of API usage

## 1. Accessing the Developer Portal

## 1a. Accessing the Developer Portal as a Customer on SSD (Resource Owner)

1. Create a chain level user and assign the DEVELOPERPORTALACCESS role to that user.  See [Adding Developer Portal Users](https://docs.oracle.com/en/industries/hospitality/integration-platform/ohipu/t_users_adding_customers.htm)
2. Sign in to the Oracle Hospitality Developer Portal.  See [Signing In to the Oracle Hospitality Developer Portal](https://docs.oracle.com/en/industries/hospitality/integration-platform/ohipu/t_signing_in_to_the_developer_portal-01.htm)

## 1b. Accessing the Developer Portal as a Customer on OCIM (Client Credentials)

1. Create a chain level user and assign the DEVELOPERPORTALACCESS role to that user.  See [Adding Developer Portal Users](https://docs.oracle.com/en/industries/hospitality/integration-platform/ohipu/t_users_adding_customers_ocim.htm)
2. Sign in to the Oracle Hospitality Developer Portal.  See [Signing In to the Oracle Hospitality Developer Portal](https://docs.oracle.com/en/industries/hospitality/integration-platform/ohipu/t_signing_in_to_the_developer_portal_ocim.htm)

## 2. Understanding the Developer Portal

### 2a. Finding APIs and workflows (optional)

These steps are *optional* but familiarize you with finding APIs in the Developer Portal.

1. Searching for the Enterprise Configuration API.  See [API Search Engine](https://docs.oracle.com/en/industries/hospitality/integration-platform/ohipu/ch_discover_and_subscribe_to_APIs.htm#OHIPU-APISearchEngine-3C569607)
2. View the API specifications for the V1 Enterprise Configuration API
3. Search for the operation `getHotelDetails`
4. Find the example request in Postman for `getHotelDetails` ![alt text](images/getting_started_2_4.png "screenshot of Oracle Hospitality Integration Platform developer portal searching for getHotelDetails highlighting the method to get to the Postman sample")
5. Find the workflow for checking in

### 2b. Creating an application

1. Create an application and subscribe it to the Property APIs.  See [Registering an Application](https://docs.oracle.com/en/industries/hospitality/integration-platform/ohipu/c_register_and_manage_applications.htm#OHIPU-CreatingAnApplication-D59E4A5D).  Note down the Application Key.

## 3. Obtaining credentials

In this lab, you'll use your own environment.  We recommend using your UAT environment.  Follow these instructions:

1. On the Environments page click `View Details` on your environment and note down the gateway URL and clientId.
2. If your environment is on OCIM the environment card will show Client Credentials; if so, jot down your enterprise Id.
3. If the clientId and clientSecret are already known to you, then stop here
4. If you don't know the clientId and clientSecret then click `Reissue` to recreate the clientSecret.  Jot this down.

## 4. Authentication Flows (background)

Oracle Hospitality APIs are protected by oAuth2.  There are two "flows" used in Oracle Hospitality APIs: Client Credentials, and Resource Owner.  These flows refer to which credentials are needed to obtain an oAuth token.

## 5. Setting up Postman

1. Download the latest [Property Postman Collection](https://github.com/oracle/hospitality-api-docs/blob/main/postman-collections/property/oracle-hospitality-property-workflows.postman_collection.json) from our Github repository
2. Download the [Bootcamp Postman collection in this repository](Bootcamp.postman_collection.json)
3. Download the [Bootcamp Postman environment in this repository](Bootcamp.postman_environment.json)
4. Import these Postman collections and Environment into Postman
5. In the Postman Environment fill in the below details:

### 5a. Postman Environment variables for a Client Credentials (OCIM) environment

| **Variable Name** | **Value** |
| --- | --- |
| AppKey | Application key you noted down in [Creating an application](#2b-creating-an-application) |
| CLIENT_ID | ClientId obtained from the Environment card in [Obtaining Credentials](#3-obtaining-credentials) |
| CLIENT_SECRET | ClientSecret obtained from the Environment card in [Obtaining Credentials](#3-obtaining-credentials) |
| HostName | Gateway URL obtained from the Environment card in [Obtaining Credentials](#3-obtaining-credentials) |
| HotelId | A property code (hotel) in your chain |
| EnterpriseId | `EnterpriseId` shown on the environment card in [Credentials](#3-obtaining-credentials) |

### 5b. Postman Environment variables for a Resource Owner (SSD) environment

| **Variable Name** | **Value** |
| --- | --- |
| AppKey | Application key you noted down in [Creating an application](#2b-creating-an-application) |
| CLIENT_ID | ClientId obtained from the Environment card in [Obtaining Credentials](#3-obtaining-credentials) |
| CLIENT_SECRET | ClientSecret obtained from the Environment card in [Obtaining Credentials](#3-obtaining-credentials) |
| HostName | Gateway URL obtained from the Environment card in [Obtaining Credentials](#3-obtaining-credentials) |
| HotelId | A property code (hotel) in your chain |
| Password | `Interface Key` from the Vendor Self-Registration Portal in [Credentials](#3-obtaining-credentials) |
| Username | `Interface ID` from the Vendor Self-Registration Portal in [Credentials](#3-obtaining-credentials) |

## 6. Obtaining an oAuth token

1. Expand the "Bootcamp" collection, inside the "Implementation Use Cases" folder
2. Click the saved request `01. Get oAuth Token`
3. Click Send
4. Note that this populates the variable `Token` in the Postman environment with the value `access_token` returned in the response

## 7. Calling the getHotelDetails API

1. Search for the getHotelDetails saved request in Postman (it's in the "Property REST APIs by Module" collection in the folder "OPERA Property APIs by Module" > "Enterprise Configuration (ENT Config)").  *Note* for ease of reading, operationIds are separated by spaces, thus `getHotelDetails` appears as `get Hotel Details` ![alt text](images/getting_started_7_1.png "Searching for get Hotel Details in the Postman collections")
2. Click Send.  This works because it uses the oAuth token in the Postman Environment

## 8. Finding the OPERA version of the environment (Optional)

1. Search for the `get OPERA version` saved request in Postman (it's in the "Property REST APIs by Module" collection in the folder "List of Values (LOV)" > "M-R") ![alt text](images/getting_started_8_1.png "Searching for get OPERA version in the Postman collections")
2. Click Send.  Read the `operaVersion` from the response payload

## 9. View analytics

1. Go back to the Developer Portal and click on the Analytics tab.  See [Analytics](https://docs.oracle.com/en/industries/hospitality/integration-platform/ohipu/c_analytics.htm#OHIPU-Analytics-EC725F0D)
2. See the calls made just now in the analytics
3. Filter down to the Enterprise Configuration API to see just the calls we made to `getHotelDetails`, along with any other operations we called in the Enterprise Configuration API
