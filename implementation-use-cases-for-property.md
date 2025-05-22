# Implementation Use Cases

- [Implementation Use Cases](#implementation-use-cases)
  - [Objective of Use Cases](#objective-of-use-cases)
  - [1 Get Token](#1-get-token)
    - [1a Get Token Resource Owner SSD](#1a-get-token-resource-owner-ssd)
    - [1a Get Token Client Credentials OCIM](#1a-get-token-client-credentials-ocim)
    - [1b get Business Date](#1b-get-business-date)
    - [1c get Hotel](#1c-get-hotel)
  - [2 Create Guest Profile](#2-create-guest-profile)
  - [3 Create Company Profile (Advanced Optional Lab)](#3-create-company-profile-advanced-optional-lab)
  - [4 Create AR Account for Company Profile (Advanced Optional Lab)](#4-create-ar-account-for-company-profile-advanced-optional-lab)
  - [5-Create Travel Agent Profile (Advanced Optional Lab)](#5-create-travel-agent-profile-advanced-optional-lab)
  - [6 Create AR Account for Travel Agent Profile (Advanced Optional Lab)](#6-create-ar-account-for-travel-agent-profile-advanced-optional-lab)
  - [7-Fetch Hotel Availability](#7-fetch-hotel-availability)
  - [8-Create Reservation](#8-create-reservation)
  - [9-Create Multi Leg Reservation](#9-create-multi-leg-reservation)
  - [10-Modify Reservation Add Preference](#10-modify-reservation-add-preference)
  - [11-Create Routing Instruction to Company on Window 2 (Advanced Optional Lab)](#11-create-routing-instruction-to-company-on-window-2-advanced-optional-lab)
  - [12-Modify Reservation to update Payment Method on Window 2 (Advanced Optional Lab)](#12-modify-reservation-to-update-payment-method-on-window-2-advanced-optional-lab)
  - [13-Create Routing Instruction to Travel Agent on Window 3 (Advanced Optional Lab)](#13-create-routing-instruction-to-travel-agent-on-window-3-advanced-optional-lab)
  - [14-Modify Reservation to update Payment Method on Window 3 (Advanced Optional Lab)](#14-modify-reservation-to-update-payment-method-on-window-3-advanced-optional-lab)
  - [15-Convert PAN into Token](#15-convert-pan-into-token)
  - [16a-Modify Reservation to Insert Credit Card Token as Payment Method on Window 1 (Only if you have OPI Cloud Enabled)](#16a-modify-reservation-to-insert-credit-card-token-as-payment-method-on-window-1-only-if-you-have-opi-cloud-enabled)
  - [16b-Modify Reservation to Insert Credit Card Number as Payment Method on Window 1 (Only if you DO NOT have OPI Cloud enabled)](#16b-modify-reservation-to-insert-credit-card-number-as-payment-method-on-window-1-only-if-you-do-not-have-opi-cloud-enabled)
  - [17-Pre Authorize Credit Card (Only if you have OPI Cloud Enabled)](#17-pre-authorize-credit-card-only-if-you-have-opi-cloud-enabled)
  - [18-Fetch Available Hotel Rooms](#18-fetch-available-hotel-rooms)
  - [19-Assign Inspected Vacant Rooms to Reservation](#19-assign-inspected-vacant-rooms-to-reservation)
  - [20-Modify Reservation to Pre-Register the Arrival](#20-modify-reservation-to-pre-register-the-arrival)
  - [21-Checkin the reservation](#21-checkin-the-reservation)
  - [22-Create Room Key OPTIONAL](#22-create-room-key-optional)
  - [23-Create a Service Request](#23-create-a-service-request)
  - [24-Set Wake up Call](#24-set-wake-up-call)
  - [25-Create Cashier](#25-create-cashier)
  - [26-Post Billing Charges on windows 1 and 2](#26-post-billing-charges-on-windows-1-and-2)
  - [27-Create Advance Room Charges](#27-create-advance-room-charges)
  - [28-Fetch Folio postings from each window](#28-fetch-folio-postings-from-each-window)
  - [29a-Post Payment on each Window 1 (Only if you have OPI Cloud Active)](#29a-post-payment-on-each-window-1-only-if-you-have-opi-cloud-active)
  - [29b-Post Payment on each Window 1 (Only if you have OPI Cloud Inactive or to pay cash)](#29b-post-payment-on-each-window-1-only-if-you-have-opi-cloud-inactive-or-to-pay-cash)
  - [30-Post Payment on each Window 2 (Advanced Optional Lab)](#30-post-payment-on-each-window-2-advanced-optional-lab)
  - [31-Post Payment on each Window 3 (Advanced Optional Lab)](#31-post-payment-on-each-window-3-advanced-optional-lab)
  - [32-Modify Reservation status to Early Departure](#32-modify-reservation-status-to-early-departure)
  - [33-Close Folio Windows](#33-close-folio-windows)
  - [34-Posting CheckOut](#34-posting-checkout)
  - [35-Email Invoice](#35-email-invoice)

## Objective of Use Cases

- Understand key implementation use cases for property-related data.

- Explore different methods for managing and utilizing property attributes.

- Learn how to integrate property data into various applications.

- Gain hands-on experience with tools and techniques for property data handling.

- Analyze real-world scenarios to improve decision-making with property data.

- Develop skills to optimize property data usage for efficiency and accuracy.

## 1 Get Token

### 1a Get Token Resource Owner SSD

To obtain a token include the following headers:

- A Basic authentication header using the base64 hash of your Client ID and Client Secret in the format ClientID:ClientSecret - base64 encoded to the Basic Access Authorization standard
- Your application key in the x-app-key header

And the following body parameters:

1. Body parameters for obtaining your initial access token
2. `grant_type`. Required to be  `password`
3. `username` and `password` As a customer, you have 3 ways to do this:
   1. One is to create an integration user within OPERA Cloud UI under Role Manager, User management, Interface Users, Manage Users, New, Choose respective Organization, Interface Type=OHIP and your email address and press SAVE
   2. Create Integration user directly in Identity Manager. Here the organization should be I-org of the chain code
   3. Third is same way as a Partner will do. Is you create through Identity Manager whereby appending the URL at the end by apiuser=y and a chain admin will need to approve the user in identity manager

  For example assuming your identity manager is:
  [https://rp15-uat-ssd-ohs.oracleindustry.com/identity/](https://rp15-uat-ssd-ohs.oracleindustry.com/identity/)

  Now for requesting integration user, you have to append it like below
  [https://rp15-uat-ssd-ohs.oracleindustry.com/identity/faces/register?apiuser=y](https://rp15-uat-ssd-ohs.oracleindustry.com/identity/faces/register?apiuser=y)

  Remember Interface id will be Username and Interface Key will be password

  Once done, chain admin will need to login into Identity Manager and approve your integration request.
  Note above URL is only as example. Check with your administrator for correct URL. Or go into OPERA Cloud URL and press register new user which will re-direct you to identity Manager URL

### 1a Get Token Client Credentials OCIM

To obtain a token include the following headers:

- A Basic authentication header using the base64 hash of your Client ID and Client Secret in the format ClientID:ClientSecret - base64 encoded to the Basic Access Authorization standard
- Your application key in the x-app-key header

And the following body parameters:

- `grant_type`. Required to be  `client_credentials`
- `scope` is always `urn:opc:hgbu:ws:__myscopes__`

### 1b get Business Date

Since your hotel may not be on today's date we need to get the business date for your hotel and set it in the environment variables.

### 1c get Hotel

The currency is required for later examples, so we need to run getHotel to obtain the currency for your hotel and set it in the environment variable `CurrencyCode`. You will find `currencyCode` it under the object `currencyFormatting`
If you response payload is empty, that means your OPERA Cloud UI doesnt have the relevant configuraton. Here we request you to enter the environment variable `CurrencyCode` with the value manually.

## 2 Create Guest Profile

Create a guest Profile with minimum data. This is the main Guest Profile who is staying in the hotel.

Within the payload we have included Postman default variables for First name and Last name, but ensure you set the `emailAddress` to be your email address.  Otherwise, you will not receive an email at step 35.

Also note that within the postman collection provided there are scripts inserted whereby from the POST response `ProfileId` will be automatically inserted into the Postman environment variables.

## 3 Create Company Profile (Advanced Optional Lab)

Create Company Profile where by adding an AR address in the payload. This is required for successful checkout of the folio to Accounts Receivable. This is to show that Reservation can be linked to other Profile types as well. Please note that you can only attach maximum of one Company Profile.

Kindly note that there are test scripts which take Company Profile Id and inserts it into Postman environment variable `CompanyId` and therefore you don't need to set any Profle id variable in this step.

1. Change `companyName`and `address` as required. Not mandatory to change but Postman has default variables. Do not change the address type 'AR ADDRESS' as this will be required for later tests when checking out the Reservation to City Ledger
2. Once Company Profile is created, ensure `getProfile` API is executed so that `AR address id` is inserted into environment variables `CompanyArAddressId` and also `CompanyName`

## 4 Create AR Account for Company Profile (Advanced Optional Lab)

This API is to create an Account Receivable Number (AR Number) to the Company Profile created previously. This is required later if you want to check out the Opera Folio Window to City Ledger (Direct Billing).

1. Account Receivable account types (AR Types) enable you to categorize AR accounts. The account type selected in each AR Account is used for filtering in both the application and also on reports, such as when generating an AR aging report subtotaled by account type. Account types also determine the stationery templates to use when generating statements and reminder letters for each AR account. Fetch AR types which is required to create Company AR account and set environment variable `CompanyArAccountType`
2. Fetching of the AR Account Number sequence for creating Company AR Account in next API. The AR Account format is determined from the OPERA Control `Account_Picture` under the module `Accounts_ Recievable`. For example `A` respresents Alphabet and `X ` represents number. For example your OPERA Control is `AAAAXX` and your value would be like `ABCD12`
3. Create Company AR Account. Make sure `accountNo`tag within the payload is updated to respective code of your choice respecting the OPERA control value from previous step
4. Copy `accountNo` from 4a and insert into query parameter. Use getProfile API to check all of the above values are responded correctly. Copy `accountNo` into `CompanyAccountNo` and `accountId` into `CompanyAccountId`.

## 5-Create Travel Agent Profile (Advanced Optional Lab)

Create Travel Agent Profile with AR Address. This is to show that a Reservation can be linked to other Profile types as well.

Please note that you can only attach a maximum of one Travel Agent Profile. The `TravelAgentProfileId` is auto populated in Environment variables with Test Scripts inserted into the collection.

1. Change `companyName`and `address` as required. Not mandatory to change. Do not change the address type 'AR ADDRESS'. The payload contains multiple address. This is just to show that multiple addresses can be inserted with one API call.  
2. Once Travel Agent Profile is created, ensure `getProfile` API is executed
   1. Copy `TA ArAddress Id`  into environment variables as `TravelAgentArAddressId`.
   2. Copy `CompanyName` into environment variables as `TravelAgentName`.
   3. Note that there are 2 addresses in the response - make sure you insert correct Address (AR) into Environment variables.

## 6 Create AR Account for Travel Agent Profile (Advanced Optional Lab)

1. Account Receivable account types (AR Types) enable you to categorize AR accounts. The account type selected in each AR Account is used for filtering in both the application and also on reports, such as when generating an AR aging report subtotaled by account type. Account types also determine the stationery templates to use when generating statements and reminder letters for each AR account. Fetch AR types which is required to create Travel Agent AR account and set environment variable `TravelAgentArAccountType`.
2. Fetching of the AR Account Number sequence for creating Travel Agent AR Account in next API. The AR Account format is determined from the OPERA Control `Account_Picture` under the module `Accounts_ Recievable`. For example `A` respresents Alphabet and `X ` respresents number. For example your OPERA Control is `AAAAXX` and your value would be like `ABCD12`
3. Create Travel Agent AR Account. Make sure `accountNo`tag within the payload is updated to respective code of your choice respectiing the OPERA control value from previous step
4. Copy `accountNo` from 6a and insert into the `accountNo` query parameter of 6b.
5. Use the `getProfile` API to check all of the above values are returned correctly.
6. Copy `accountNo` into the environment variables as `TravelAgentAccountNo`
7. Set `accountId` into the environment variables as `TravelAgentAccountId`.

## 7-Fetch Hotel Availability

Fetch Hotel Availability which is required for creating a Reservation. This provides available ratePlanCode, room type and room rate amount.

After successful fetch, make sure following items are inserted into Environment variables:

1. `roomType`into variable `RoomType`  
2. `ratePlanCode`into variable `RatePlanCode`

## 8-Create Reservation

Create Reservation with Company and Travel Agent attached. Make sure all of required items are fetched and environment variables are populated.

Hotel Currency Code is `USD`.

Values within `TaRecordLocator`and `Expedia` will be autopopulated with postman default variables.

1. Fetch MarketCode. A market code is required in each reservation and group block and is used track the room nights and revenue generated by each reservation for statistical purposes. Use this to set environment variable `MarketCode`
2. Fetch SourceCode. Use source codes to manage and track the source of business at your hotel, such as mail, telephone, fax, central reservations, travel agency, and so on. OPERA Cloud maintains the source of business statistics. Just like market codes, source codes are attached to reservation records to track how the reservations come to the property. Source codes are also grouped into source groups for reporting. Every property or property chain determines the breakdown of the source information it requires. Use this to set environment variable `SourceCode`
3. Fetch BookingMedium (Origin Code). OPERA Cloud maintains origin of business statistics, which enables you to track reservations by setting up origin codes (the originating media source for the reservation). Just as market codes can be grouped into market groups for reporting purposes, origin codes are attached to reservation records to track how reservations come into the property. Each property or property chain determines the breakdown of the origin information it requires (for example, mail, telephone, fax, central reservations, travel agency, GDS, and so on).  Use this to set environment variable `BookingMedium`
4. Fetch Guarantee Code (Reservation Type). When making a reservation, a reservation type (also called a guarantee code) must be selected for the reservation to identify if the reservation is to deduct a room from inventory. Typical reservation types for standard reservations are 6:00 PM Hold, Guaranteed by Credit Card, Guaranteed by Company, and so on. For tentative reservations, typical reservation types are Deposit Expected or Confirmation Expected,
Non deduct reservations are not included in the availability calculations by default, but they can be included if you select the Non-deduct Rooms Sold and the Available Rooms with Non-deduct (Rooms Sold) view options when you access the Property Availability.
Group blocks and travel agent (block) allotments must also be assigned reservation types. This provides several different combinations to cover guaranteed / deduct blocks, non-guaranteed / non-deduct blocks, or non-deduct allotments with deduct reservations. Use this to set environment variable `GuaranteeCode`
5. Fetch Payment Method.  Use this to set environment variable `PaymentMethod`. Please take a payment method of your choice. You can set as `Cash` respective code at present as in later steps will be setting it to Credit Card
6. Create Reservation. This API will create the Reservation. There are scripts running when you execute this API whereby the environment variable `ReservationId` is set automatically
7. Fetch Reservation.  Once postReservation is executed, please check whether all required details are entered correctly with this API. Ensure the value from reservationIdList type=Confirmation is copied into environment variable `Confirmationid` and also `id` from `externalReferences` into `ExternalReferences`. Also set the `emailAddress` which you set with Step 3, the variable `EmailAddress`.

## 9-Create Multi Leg Reservation

Create Reservation which is multi leg (multi segment) reservation. Multi-Leg Reservation refers to a single guest reservation that includes multiple consecutive stays (or "legs") at the same or different properties. Each "leg" represents a segment of the reservation with different arrival and departure dates, possibly with different room types, rates, or even hotel properties (if managing multiple hotels in the same system).
This API is to show you how to create Multileg and will not be further used in this collection and therefore do not require any environment variables.

1. After successful post, Postman will automatically populate environment variable `ReservationId2`
2. Verify the data with `getReservations`, making use of the `confirmationNumberList` query parameter which shows you can fetch all leg Reservations with one API. You should get 2 Reservations in the response under `reservationInfo`

## 10-Modify Reservation Add Preference

Pre Arrival where a preference will be added.

1. Fetch Preference.  To insert the preference, you will need to fetch all preferences which can be attached on the reservation. For testing purposes, use the preference group `ROOM FEATURES`. Choose one of the preferences in the response to set as the environment variable `PreferenceCode`.  _Note_: The preference code must be configured on the room type chosen - see [Adding Room Types](https://docs.oracle.com/en/industries/hospitality/opera-cloud/25.1/ocsuh/t_rooms_managing_room_types.htm) item `aa`.
2. Modify Reservation to insert the Preference Code from step 1
3. Fetch Reservation.  Once putReservation is executed, check whether your preference has been attached on the reservation

## 11-Create Routing Instruction to Company on Window 2 (Advanced Optional Lab)

A routing instruction is a set of rules applied to a reservation that tells Opera where and how to route charges.
A routing code is a predefined template that contains a routing instruction. It simplifies and standardizes routing for frequent use.

Posting a routing instruction to existing reservation where `Food` charges goes to the Company which is linked to the reservation. Determine which routing code you will use for your environment then ensure it is directed to window 2. You can pick any of your choice except `ALL`. For testing purposes use one of the `Food` respective codes.

1. Fetch the routing Codes with `getRoutingCodes` and set Environment Variable of `CompanyRoutingCode`
2. Create Routing Instructions
3. Check whether Routing Instructions was successful on Window 2

## 12-Modify Reservation to update Payment Method on Window 2 (Advanced Optional Lab)

1. To find the Payment Method use `getPaymentMethod` API. Use whichever code is configured in your environment for City Ledger or Direct Billing. Within the response payload, the relevent code should have DirectBillYN=Y.  Set this code to be the `CompanyPaymentMethod` environment variable.
2. Modify Payment Method on Reservation.  Once Routing is done, modification is required to the existing Reservation to inform that window 2 will be paid by Direct Billing as the Payment Method. Kindly note Routing Instructions and Payment Method are 2 different APIs at present.
3. Use fetch Reservation to check whether the modification of the Payment Method was successful on Window 2

## 13-Create Routing Instruction to Travel Agent on Window 3 (Advanced Optional Lab)

A routing instruction is a set of rules applied to a reservation that tells Opera where and how to route charges.
A routing code is a predefined template that contains a routing instruction. It simplifies and standardizes routing for frequent use.

Posting a routing instruction to an existing reservation where Room charges go to the Travel Agent linked to the reservation. Make sure the routing is done to window 3. Set  whichever code respective to `Room Charges` in environment variable for City Ledger or Direct Billing and direct it to window 3.

1. Fetch the routing Codes with `getRoutingCodes` API and set the value corresponding to the routing code for City Ledger or Direct Billing in your environment in the Environment Variable  `TravelAgentRoutingCode`
2. Create Routing Instructions on Reservation
3. Check whether Routing Instructions was successful on Window 3

## 14-Modify Reservation to update Payment Method on Window 3 (Advanced Optional Lab)

1. To find the Payment Method use `getPaymentMethod` API. Use whichever code is configured in your environment for City Ledger or Direct Billing. Within the response payload, the relevent code should have DirectBillYN=Y. Set this to be the `TravelAgentPaymentMethod` environment variable.
2. Modify Payment Method on Reservation.  Once Routing is done, modification is required to the existing Reservation to inform that window 3 will be paid by Direct Billing as the Payment Method. Kindly note Routing Instructions and Payment Method are 2 different APIs at present.
3. Use fetch Reservation to check whether the modification  of the Payment Method was successful on Window 3

## 15-Convert PAN into Token

1. With this API, you can verify whether OPI cloud is active.  _Note_ that if you do not have OPI cloud active please:
   1. Note that this configuration will not be supported in the future
   2. Set the environment variables `CompanyPaymentMethod` and `TravelAgentPaymentMethod` to `CA`
   3. Skip to step 16a
2. Convert Primary Account Number (PAN) into Token issued by Payment Service Providers.
This is required to updated Window 1 payment method to the payment method which belongs to guest.
Take any [test Credit Card numbers](https://www.paypalobjects.com/en_AU/vhelp/paypalmanager_help/credit_card_numbers.htm) and insert into the payload within the tag `pan`.

Kindly note that this environment is linked to a PSP simulator and therefore every PAN number conversion will respond with different Token numbers for same PAN number.

## 16a-Modify Reservation to Insert Credit Card Token as Payment Method on Window 1 (Only if you have OPI Cloud Enabled)

_Note_ Use this only if OPI is active (see [step 15](#15-convert-pan-into-token)).

Update an existing Payment Method using this API. Make sure you update the request body:

1. Set `cardNumber` to be the value in the `token` property you received from the response body to `openPaymentTokenExchange`
2. Set `cardNumberMasked` to be the value from the `pan` property you received from the response body to `openPaymentTokenExchange`
3. Set `expirationDate` to be some time in the future

And any other value which you changed.

## 16b-Modify Reservation to Insert Credit Card Number as Payment Method on Window 1 (Only if you DO NOT have OPI Cloud enabled)

_Note_ Use this only if OPI is not active (see [step 15](#15-convert-pan-into-token)).  This configuration will not be supported in the future.

Update an existing Payment Method using this API. Make sure you update the request body:

1. Set `cardNumber` to be the plaintext card number
2. Set `expirationDate` to be some time in the future

And any other value which you changed.

## 17-Pre Authorize Credit Card (Only if you have OPI Cloud Enabled)

This API is useful for many Kiosk Partners who want to save time to Pre Authorize the card prior to calling the Checkin API.

1. getHotelInterface API will show whether OPI is installed and configured. Look for `activeFlag=true`. Also set environment variable `logo` into `Logo`which is terminal Id
2. Pre Authorize card.After execution, make sure the following values are set into Environment variables:
   1. `cardId`
   2. `approvalCode`
3. Check whether PreAuthorization was successful with the fetchAuthorizationHistory API

## 18-Fetch Available Hotel Rooms

Ensure there are enough Inspected & Vacant rooms. If not they can be made inspected within OPERA Cloud UI in Inventory > Room Management > Housekeeping Board

With the API find vacant and inspected rooms so that you can assign one to the reservation.

Make sure you set the `RoomNumber` into the environment variable.

## 19-Assign Inspected Vacant Rooms to Reservation

Assign the room which you got from the earlier API call.

## 20-Modify Reservation to Pre-Register the Arrival

Pre-Register Or Pre-Checkin

You can offer your guests the ability to check in for their reservations by pre-registering. When a reservation is pre-registered, all of the guest's information to finish the registration process is collected, including authorizing the guest's credit card for the reservation. This makes it easy to check in the reservation when the guests arrive and the assigned room is available.

You can search for and manage pre-registered arrival reservations from Arrivals search by selecting the Pre-registered check box in advanced search.

1. Pre Register the guest. Ensure the `arrivalTime` is updated in the payload

2. Additional functionality - `Advanced Checkin`
At times, when guests arrive to the property prior to a room being ready, you can flag a reservation as Advance Checked In for arrivals due in on the current business date. This enables guests to post charges to their reservation folio prior to check in, and helps the rooms management team prioritize room cleaning and assignment. Individual reservations (including Walk In reservations, Pre Registered reservations, and reservations that are in Queue) and group block reservations can be Advance Checked In.

_Benefits to the Guest and to the Property_
Advance Check In with the Expected Time of Return (ETR) parameter turned On provides the following benefits.  The guest can:

- Post charges to their reservation folio prior to checking in.
- Receive notifications when the room is ready.

The rooms management and front office teams can:

- Easily identify which reservations are flagged Advance Checked In.
- Prioritize and sort Advance Checked In reservations by expected time of return (ETR).
- Assign rooms to reservations based on expected time of return (ETR).
- Add ETR comments that link to the ETR time.
- Set Advance Checked In reservations to automatically check in based on room status.
- Check in multiple Advance Checked In reservations (Mass Advance Check In).

3. Ensure `expectedReturnTime` is updated and execute Advance checkin API

## 21-Checkin the reservation

Checkin the guest using this API.

## 22-Create Room Key OPTIONAL

This is for illustration purposes, because it relies upon a key card vendor being integrated into your environment.

1. Creating a Key. KeyType by default should be `New`

## 23-Create a Service Request

1. Fetch Service request codes.  Choose one of the service request codes in the response and update the environment variables `ServiceRequestCodes` and `DeptCode` with the values from this service request code.
2. Create a Service request to provide towel by Housekeeping department. Ensure you change the tag `openDate` within the payload
3. Fetch the Service Request Codes applied to the reservation to see whether it was successfully inserted.  _Note_ that due to a known bug this returns all service requests.  Look through the response body to check that the service request created in step 1 exists in the response.

## 24-Set Wake up Call

Create a Wakeup call on the reservation.

1. Check whether Wakeup call Opera Control is active
2. Create a Wakeup call on the reservation.
3. getWakeUpcall.  Use this API to check whether the postWakeUpcall was inserted successfully into the reservation

## 25-Create Cashier

This API is required for `postBillingCharges` in which the cashier id is mandatory.

1. Fetch the next available cashier number id and insert into `CashierId` environment variable
2. Create Cashier  
3. Use this API to check whether postCashier API has successfully inserted cashier id.

In production, ensure you ask the customer which cashierId to use and consistently use that cashierId for that environment.

## 26-Post Billing Charges on windows 1 and 2

1. getTransactionCode
Use this API to find the required transaction Code. Find telecommunications or similar transaction codes you'll choose to assign to Window 1.  Note down the transaction code. Make sure this transaction code is inserted into the environment variable `TransactionCode`. Kindly note that transactionCodes should be created with the `manualPost` tag set to `true`. Only these transaction codes can be used at preset to be able to post through OHIP.

2. Post charges to the window 1. The amount can be of your choice. Remember in Step 13 we created Routing instructions the Food Charges are routed to window 2. Therefore make sure the transaction code you choose here is not related to `Food`.

3. getTransactionCode
Use this API to find the required transaction Code. Find food or similar transaction codes to assign to Window 2. Overwrite the environment variable `TransactionCode` with this new transaction code. Kindly note that transactionCodes should be created with the `manualPost` tag set to `true`. Only these transaction Codes can be used at preset to be able to post through OHIP.

4. Post charges to the window 2. The amount can be of your choice. Remember in Step 13 we created Routing instructions the Food Charges are routed to window 2. Therefore make sure the transaction code you choose here is related to `Food`

## 27-Create Advance Room Charges

As we are testing and no End of Day Routine will be run, use this API to post Room Charges in advance which will post room charges to window 3 as per the Routing instructions you inserted earlier.

## 28-Fetch Folio postings from each window

Use this API to fetch Folios from each window.

> Remember if you did the advanced labs there will 3 Windows which should have Charges (Balances)

## 29a-Post Payment on each Window 1 (Only if you have OPI Cloud Active)

1. Use this API to post payment against the folio on each Window. There should be no balance left. Window 1 should be paid against Credit Card.

## 29b-Post Payment on each Window 1 (Only if you have OPI Cloud Inactive or to pay cash)

_Note_ Use this only if OPI is not active (see [step 15](#15-convert-pan-into-token)).  This configuration will not be supported in the future.

1. Use this API to post payment against the folio on each Window. There should be no balance left. Window 1 should be paid against Cash.

## 30-Post Payment on each Window 2 (Advanced Optional Lab)

Use this API to post payment against the folio on each Window. There should be no balance left

1. Window 2 should be paid against the payment Method determined in step 12a, which is invoiced to Company

## 31-Post Payment on each Window 3 (Advanced Optional Lab)

Use this API to post payment against the folio on each Window. There should be no balance left

1. Window 3 should be paid against payment Method determined in step 14a, which is invoiced to Travel Agent

## 32-Modify Reservation status to Early Departure

As we are testing and no End of Day Routine will be run, use this API to change the Reservation to be able checkout Early.

## 33-Close Folio Windows

Use this folio to settle the folio prior to checkout.

> _This API needs to be executed on all windows where charges were made_.

*Make sure that you change the `folioWindow` value for each of the API calls.*

## 34-Posting CheckOut

Use this API to post a checkout.

## 35-Email Invoice

Send a copy of the invoice to email.

1. Send a copy of the invoice to email.  Optionally, change the `emailAddress`

2. Fetch a copy of the invoice in Base64 format. Use any public website to convert Base64 into pdf to view it, for example [Base64 Guru](https://base64.guru/converter/decode/pdf).
