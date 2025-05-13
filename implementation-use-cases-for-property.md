# Implementation Use Cases

- [Implementation Use Cases](#implementation-use-cases)
  - [Objective of Use Cases](#objective-of-use-cases)
  - [0 Set Currency](#0-set-currency)
  - [1 Get Token](#1-get-token)
  - [2 Create Guest Profile](#2-create-guest-profile)
  - [3 Create Company Profile OPTIONAL](#3-create-company-profile-optional)
  - [4 Create AR Account for Company Profile OPTIONAL](#4-create-ar-account-for-company-profile-optional)
  - [5-Create Travel Agent Profile OPTIONAL](#5-create-travel-agent-profile-optional)
  - [6 Create AR Account for Travel Agent Profile OPTIONAL](#6-create-ar-account-for-travel-agent-profile-optional)
  - [7-Fetch Hotel Availability](#7-fetch-hotel-availability)
  - [8-Create Reservation](#8-create-reservation)
  - [9-Create Multi Leg Reservation OPTIONAL](#9-create-multi-leg-reservation-optional)
  - [10-Modify Reservation Add Preference OPTIONAL](#10-modify-reservation-add-preference-optional)
  - [11-Create Routing Instruction to Company on Window 2 OPTIONAL](#11-create-routing-instruction-to-company-on-window-2-optional)
  - [12-Modify Reservation to update Payment Method on Window 2 OPTIONAL](#12-modify-reservation-to-update-payment-method-on-window-2-optional)
  - [13-Create Routing Instruction to Travel Agent on Window 3 OPTIONAL](#13-create-routing-instruction-to-travel-agent-on-window-3-optional)
  - [14-Modify Reservation to update Payment Method on Window 3 OPTIONAL](#14-modify-reservation-to-update-payment-method-on-window-3-optional)
  - [15-Convert PAN into Token OPTIONAL](#15-convert-pan-into-token-optional)
  - [16-Modify Reservation to Insert Credit Card Token as Payment Method on Window 1 OPTIONAL](#16-modify-reservation-to-insert-credit-card-token-as-payment-method-on-window-1-optional)
  - [16a-Modify Reservation to Insert Credit Card Token as Payment Method on Window 1 with OPI inactive OPTIONAL](#16a-modify-reservation-to-insert-credit-card-token-as-payment-method-on-window-1-with-opi-inactive-optional)
  - [17-Pre Authorize Credit Card OPTIONAL](#17-pre-authorize-credit-card-optional)
  - [18-Fetch Available Hotel Rooms](#18-fetch-available-hotel-rooms)
  - [19-Assign Inspected Vacant Rooms to Reservation](#19-assign-inspected-vacant-rooms-to-reservation)
  - [20-Modify Reservation to Pre-Register the Arrival OPTIONAL](#20-modify-reservation-to-pre-register-the-arrival-optional)
  - [21-Checkin the reservation](#21-checkin-the-reservation)
  - [22-Create Room Key](#22-create-room-key)
  - [23-Create a Service Request OPTIONAL](#23-create-a-service-request-optional)
  - [24-Set Wake up Call OPTIONAL](#24-set-wake-up-call-optional)
  - [25-Create Cashier](#25-create-cashier)
  - [26-Post Billing Charges on windows 1 and 2 OPTIONAL](#26-post-billing-charges-on-windows-1-and-2-optional)
  - [27-Create Advance Room Charges](#27-create-advance-room-charges)
  - [28-Fetch Folio postings from each window](#28-fetch-folio-postings-from-each-window)
  - [29-Post Payment on each Window 1 OPTIONAL](#29-post-payment-on-each-window-1-optional)
  - [30-Post Payment on each Window 2 OPTIONAL](#30-post-payment-on-each-window-2-optional)
  - [31-Post Payment on each Window 3 OPTIONAL](#31-post-payment-on-each-window-3-optional)
  - [32-Modify Reservation status to Early Departure](#32-modify-reservation-status-to-early-departure)
  - [33-Close Folio Windows 1-3](#33-close-folio-windows-1-3)
  - [34-Posting CheckOut](#34-posting-checkout)
  - [35-Email Invoice OPTIONAL](#35-email-invoice-optional)

## Objective of Use Cases

* Understand key implementation use cases for property-related data.

* Explore different methods for managing and utilizing property attributes.

* Learn how to integrate property data into various applications.

* Gain hands-on experience with tools and techniques for property data handling.

* Analyze real-world scenarios to improve decision-making with property data.

* Develop skills to optimize property data usage for efficiency and accuracy.

## 0 Set Currency

Before starting, set the `CurrencyCode` environment variable to reflect the currency of the hotel you're using.

## 1 Get Token

This is required to access Oracle Hospitality OPERA Cloud REST APIs.

To obtain a token include the following headers:

* A Basic authentication header using the base64 hash of your Client ID and Client Secret in the format ClientID:ClientSecret - base64 encoded to the Basic Access Authorization standard
* Your application key in the x-app-key header

And the following body parameters:

* Body parameters for obtaining your initial access token
* `grant_type`. Required to be  `client_credentials`
* scope. `grant_type` is client_credentials, set this to your assigned scope. Check within Sandbox environment for OHIPLAB in your Partner Developer Portal

## 2 Create Guest Profile

Create a guest Profile with minimum data. This is the main Guest Profile who is staying in the hotel.

Within the payload we have included Postman default variables for First name and Last name, but ensure you set the `emailAddress` to be your email address.  Otherwise, you will not receive an email at step 35.

Also note that within the postman collection provided there are scripts inserted whereby from the POST response `ProfileId` will be automatically inserted into the Postman environment variables.

## 3 Create Company Profile OPTIONAL

Create Company Profile where by adding an AR address in the payload. This is required for successful checkout of the folio to Accounts Receivable. This is to show that Reservation can be linked to other Profile types as well. Please note that you can only attach maximum of one Company Profile.

Kindly note that there are test scripts which take Company Profile Id and inserts it into Postman environment variable `CompanyId`

1. Change `companyName`and `address` as required. Not mandatory to change but Postman has default variables. Do not change the address type 'AR ADDRESS'
2. Once Company Profile is created, ensure `getProfile` API is executed so that `AR address id` is inserted into environment variables `CompanyArAddressId` and also `CompanyName`

## 4 Create AR Account for Company Profile OPTIONAL

This API is to create an Account Receivable Number (AR Number) to the Company Profile created previously. This is required later if you want to check out the Opera Folio Window to City Ledger (Direct Billing).

1. Account Receivable account types (AR Types) enable you to categorize AR accounts. The account type selected in each AR Account is used for filtering in both the application and also on reports, such as when generating an AR aging report subtotaled by account type. Account types also determine the stationery templates to use when generating statements and reminder letters for each AR account. Fetch AR types which is required to create Company AR account and set environment variable `CompanyArAccountType`
2. Create Company AR Account. Create your own AR account number in the format `AAAA<nnn>` where `<nnn>` are three digits.  
3. Copy `accountNo` from 4a and insert into query parameter. Use getProfile API to check all of the above values are responded correctly. Copy `accountNo` into `CompanyAccountNo` and `accountId` into `CompanyAccountId`.

## 5-Create Travel Agent Profile OPTIONAL

Create Travel Agent Profile with AR Address. This is to show that a Reservation can be linked to other Profile types as well.

Please note that you can only attach a maximum of one Travel Agent Profile. The `TravelAgentProfileId` is auto populated in Environment variables with Test Scripts inserted into the collection.

1. Change `companyName`and `address` as required. Not mandatory to change. Do not change the address type 'AR ADDRESS'. The payload contains multiple address. This is just to show that multiple addresses can be inserted with one API call.  
2. Once Travel Agent Profile is created, ensure `getProfile` API is executed so that `TA ArAddress Id` and also `CompanyName` is inserted into environment variables `TravelAgentArAddressId` & `TravelAgentName`. Note that there are 2 addresses in the response. Make sure you insert correct Address into Environment variable.

## 6 Create AR Account for Travel Agent Profile OPTIONAL

1. Account Receivable account types (AR Types) enable you to categorize AR accounts. The account type selected in each AR Account is used for filtering in both the application and also on reports, such as when generating an AR aging report subtotaled by account type. Account types also determine the stationery templates to use when generating statements and reminder letters for each AR account. Fetch AR types which is required to create Travel Agent AR account and set environment variable `TravelAgentArAccountType`.
2. Create Travel Agent AR Account. Create your own Travel Agent AR account number in the format `AAAA<nnn>` where `<nnn>` are three digits.  
3. Copy `accountNo` from 6a and insert into query parameter. Use getProfile API to check all of the above values are responded correctly. Copy `accountNo` into `TravelAgentAccountNo` and `accountId` into `TravelAgentAccountId`.

## 7-Fetch Hotel Availability

Fetch Hotel Availability which is required for creating a Reservation. This provides available ratePlanCode, room type and room rate amount.

After successful fetch, make sure following are inserted into Environment variables:

1. Room Type
2. RatePlanCode

For testing purposes please pick Room type `DEL` and RatePlanCode `BARRO` as they are relevant later for updating a reservation. Set environment variables `RoomType` and `RatePlanCode` respectively by selecting the appropriate text, right clicking and choosing `Set:Bootcamp` then choose `RoomType` or `RatePlanCode` as appropriate.

The variables `Currentdate` and `Currentdateplus1` variable are created from getToken API test scripts.

## 8-Create Reservation

Create Reservation with Company and Travel Agent attached. Make sure all of required items are fetched and environment variables are populated.

Hotel Currency Code is `USD`.

Values within `TaRecordLocator`and `Expedia` will be autopopulated with postman default variables.

1. Fetch MarketCode.  This API is required so that the variable `MarketCode` can be inserted into the environment variable
2. Fetch SourceCode.  This API is required so that the variable `SourceCode` can be inserted into the environment variable
3. Fetch BookingMedium.  This API is required so that the variable `BookingMedium` can be inserted into the environment variable. This is commonly called Origin Code in OPERA Cloud UI.
4. Fetch Guarantee Code (Reservation Type).  This API is required so that the variable `GuaranteeCode` can be inserted into the environment variable
5. Fetch Payment Method.  This API is required so that the variable `PaymentMethod` can be inserted into the environment variable
6. Create Reservation. This API will create the Reservation.
7. Fetch Reservation.  Once postReservation is executed, please check whether all required details are entered correctly with this API. Ensure the value from reservationIdList type=Confirmation is copied into environment variable `Confirmationid` and also `id` from `externalReferences` into `ExternalReferences`

## 9-Create Multi Leg Reservation OPTIONAL

Create Reservation which is multi leg reservation. This API is to show you how to create Multileg and will not be further used in this collection and therefore do not require any environment variables.

1. After successful post, Postman will automatically populate environment variable `ReservationId2`
2. Verify the data with `getReservations`, making use of the `confirmationNumberList` query parameter which shows you can fetch all leg Reservations with one API. You should get 2 Reservations in the response.

## 10-Modify Reservation Add Preference OPTIONAL

Pre Arrival where a preference will be added.

1. Fetch Preference.  To insert the preference, you will need to fetch all preferences which can be attached on the reservation. For testing purposes, use the preference group `ROOM FEATURES`. Choose one of the preferences in the response to set as the environment variable `PreferenceCode`.  _Note_: The preference code must be configured on the room type chosen - see [Adding Room Types](https://docs.oracle.com/en/industries/hospitality/opera-cloud/25.1/ocsuh/t_rooms_managing_room_types.htm) item `aa`.
2. Modify Reservation to insert the Preference Code from step 1
3. Fetch Reservation.  Once putReservation is executed, check whether your preference has been attached on the reservation

## 11-Create Routing Instruction to Company on Window 2 OPTIONAL

Posting a routing instruction to existing reservation where `Food` charges goes to the Company which is linked to the reservation. Determine which routing code you will use for your environment then ensure it is directed to window 2.

1. Fetch the routing Codes with `getRoutingCodes` and set Environment Variable of `CompanyRoutingCode`
2. Create Routing Instructions

## 12-Modify Reservation to update Payment Method on Window 2 OPTIONAL

1. To find the Payment Method use `getPaymentMethod` API. Use whichever code is configured in your environment for City Ledger or Direct Billing.  Set this to be the `CompanyPaymentMethod` environment variable.
2. Modify Payment Method on Reservation.  Once Routing is done, modification is required to the existing Reservation to inform that window 2 will be paid by Direct Billing as the Payment Method. Kindly note Routing Instructions and Payment Method are 2 different APIs at present.
3. Use fetch Reservation to check whether the modification of the Payment Method was successful on Window 2

## 13-Create Routing Instruction to Travel Agent on Window 3 OPTIONAL

Posting a routing instruction to an existing reservation where Room charges go to the Travel Agent linked to the reservation. Make sure the routing is done to window 3. Use whichever code is configured in your environment for City Ledger or Direct Billing and direct it to window 3.

1. Fetch the routing Codes with `getRoutingCodes` API and set the value corresponding to the routing code for City Ledger or Direct Billing in your environment in the Environment Variable  `TravelAgentRoutingCode`
2. Create Routing Instructions on Reservation
3. Check whether Routing Instructions was successful on Window 3

## 14-Modify Reservation to update Payment Method on Window 3 OPTIONAL

1. To find the Payment Method use `getPaymentMethod` API. Use whichever code in configured in your environment for City Ledger or Direct Billing. Set this to be the `TravelAgentPaymentMethod` environment variable.
2. Modify Payment Method on Reservation.  Once Routing is done, modification is required to the existing Reservation to inform that window 3 will be paid by Direct Billing as the Payment Method. Kindly note Routing Instructions and Payment Method are 2 different APIs at present.
3. Use fetch Reservation to check whether the modification  of the Payment Method was successful on Window 3

## 15-Convert PAN into Token OPTIONAL

1. Verify whether OPI cloud is active.  *Note* that if you do not have OPI cloud active please skip to step 16a but note that this configuration will not be supported in the future.
2. Convert Primary Account Number (PAN) into Token issued by Payment Service Providers.
This is required to updated Window 1 payment method to the payment method which belongs to guest.
Take any [test Credit Card numbers](https://www.paypalobjects.com/en_AU/vhelp/paypalmanager_help/credit_card_numbers.htm) and insert into the payload within the tag `pan`.

Kindly note that this environment is linked to a PSP simulator and therefore every PAN number conversion will respond with different Token numbers for same PAN number.

## 16-Modify Reservation to Insert Credit Card Token as Payment Method on Window 1 OPTIONAL

*Note* Use this only if OPI is active (see step 15).

Update an existing Payment Method using this API. Make sure you update the request body:

1. Set `cardNumber` to be the value in the `token` property you received from the response body to `openPaymentTokenExchange`
2. Set `cardNumberMasked` to be the value in the `pan` property you received from the response body to `openPaymentTokenExchange`
3. Set `expirationDate` to be some time in the future

And any other value which you changed.

## 16a-Modify Reservation to Insert Credit Card Token as Payment Method on Window 1 with OPI inactive OPTIONAL

*Note* Use this only if OPI is not active (see step 15).  This configuration will not be supported in the future.

Update an existing Payment Method using this API. Make sure you update the request body:

1. Set `cardNumber` to be the plaintext card number
2. Set `expirationDate` to be some time in the future

And any other value which you changed.

## 17-Pre Authorize Credit Card OPTIONAL

This API is useful for many Kiosk Partners who want to save time to Pre Authorize the card prior to calling the Checkin API.

1. getHotelInterface API will show whether OPI is installed and configured. Look for `activeFlag=true`
2. Pre Authorize card. Make sure the `terminalId` value matches the terminalId in the `logo` value of the response to getHotelInterface (step 1). After execution, make sure the following values are inserted into Environment variables:
   1. `cardId`
   2. `approvalCode`
   3. `vendorTranId` Kindly note that there may be a space after the last digit. Do not include this in your environment.
3. Check whether PreAuthorization was successful with the fetchAuthorizationHistory API

## 18-Fetch Available Hotel Rooms

Find vacant and inspected rooms so that you can assign one to the reservation.

Make sure you insert the `RoomNumber` into the environment variable.

## 19-Assign Inspected Vacant Rooms to Reservation

Assign the room which you got from the earlier API call.

## 20-Modify Reservation to Pre-Register the Arrival OPTIONAL

Pre-Register Or Pre-Checkin

You can offer your guests the ability to check in for their reservations by pre-registering. When a reservation is pre-registered, all of the guest's information to finish the registration process is collected, including authorizing the guest's credit card for the reservation. This makes it easy to check in the reservation when the guests arrive and the assigned room is available.

You can search for and manage pre-registered arrival reservations from Arrivals search by selecting the Pre-registered check box in advanced search.

1. Pre Register the guest. Ensure the `arrivalTime` is updated in the payload

Additional functionality - `Advanced Checkin`
At times, when guests arrive to the property prior to a room being ready, you can flag a reservation as Advance Checked In for arrivals due in on the current business date. This enables guests to post charges to their reservation folio prior to check in, and helps the rooms management team prioritize room cleaning and assignment. Individual reservations (including Walk In reservations, Pre Registered reservations, and reservations that are in Queue) and group block reservations can be Advance Checked In.

*Benefits to the Guest and to the Property*
Advance Check In with the Expected Time of Return (ETR) parameter turned On provides the following benefits.  The guest can:

* Post charges to their reservation folio prior to checking in.
* Receive notifications when the room is ready.
The rooms management and front office teams can:
* Easily identify which reservations are flagged Advance Checked In.
* Prioritize and sort Advance Checked In reservations by expected time of return (ETR).
* Assign rooms to reservations based on expected time of return (ETR).
* Add ETR comments that link to the ETR time.
* Set Advance Checked In reservations to automatically check in based on room status.
* Check in multiple Advance Checked In reservations (Mass Advance Check In).

2. Ensure `expectedReturnTime` is updated and execute Advance checkin API

## 21-Checkin the reservation

Checkin the guest using this API.

## 22-Create Room Key

1. Fetch the key options and insert these values as needed in 22b
2. This API is to fetch the key encoder id which you need for 22b. For sandbox it is default value which is already inserted into 22b. There are no physical encoders configured and therefore this API will not return any response for Sandbox
3. Creating a Key 22b. KeyType by default should be `New`

## 23-Create a Service Request OPTIONAL

1. Fetch Service request codes
2. Create a Service request to provide towel by Housekeeping department. Ensure you change the tag `openDate` within the payload
3. Fetch the Service Request Codes applied to the reservation to see whether it was successfully inserted

## 24-Set Wake up Call OPTIONAL

Create a Wakeup call on the reservation. Ensure you change the dates within the payload

1. Check whether Wakeup call Opera Control is active
2. Create a Wakeup call on the reservation.
3. getWakeUpcall.  Use this API to check whether the postWakeUpcall was inserted successfully into the reservation

## 25-Create Cashier

This API is required for `postBillingCharges` in which the cashier id is mandatory.

1. Fetch the next available cashier number id and insert into `CashierId` environment variable
2. Create Cashier  
3. Use this API to check whether postCashier API has successfully inserted cashier id.

In production, ensure you ask the customer which cashierId to use and consistently use that cashierId for that environment.

## 26-Post Billing Charges on windows 1 and 2 OPTIONAL

1. getTransactionCode
Use this API to find the required transaction Code. Find telecommunications or similar transaction codes you'll choose to assign to Window 1.  Note down the transaction code. Make sure this transaction code is inserted into the environment variable `TransactionCode`. Kindly note that transactionCodes should be created with the `manualPost` tag set to `true`. Only these transaction codes can be used at preset to be able to post through OHIP.

2. Post charges to the window 1. The amount can be of your choice

3. getTransactionCode
Use this API to find the required transaction Code. Find food or similar transaction codes to assign to Window 2. Overwrite the environment variable `TransactionCode` with this new transaction code. Kindly note that transactionCodes should be created with the `manualPost` tag set to `true`. Only these transaction Codes can be used at preset to be able to post through OHIP.

4. Post charges to the window 2. The amount can be of your choice

## 27-Create Advance Room Charges

As we are testing and no End of Day Routine will be run, use this API to post Room Charges in advance which will post room charges to window 3 as per the Routing instructions you inserted earlier.

## 28-Fetch Folio postings from each window

Use this API to fetch Folios from each window. Remember there are 3 Windows which should have Charges (Balances)

## 29-Post Payment on each Window 1 OPTIONAL

1. Use this API to post payment against the folio on each Window. There should be no balance left. Window 1 should be paid against Credit Card.

## 30-Post Payment on each Window 2 OPTIONAL

Use this API to post payment against the folio on each Window. There should be no balance left

1. Window 2 should be paid against the payment Method determined in step 12a, which is invoiced to Company

## 31-Post Payment on each Window 3 OPTIONAL

Use this API to post payment against the folio on each Window. There should be no balance left

1. Window 3 should be paid against payment Method determined in step 14a, which is invoiced to Travel Agent

## 32-Modify Reservation status to Early Departure

As we are testing and no End of Day Routine will be run, use this API to change the Reservation to be able checkout Early.

## 33-Close Folio Windows 1-3

Use this folio to settle the folio prior to checkout.

*This API needs to be executed on all 3 windows separately as charges were on all these 3 windows*.

Make sure that you change the `folioWindow` value for each of the API calls.

## 34-Posting CheckOut

Use this API to post a checkout.

## 35-Email Invoice OPTIONAL

Send a copy of the invoice to email.

1. getFolioTypes.  Use this API to fetch the folio type configured for executing the postEmailFolioReport API

2. Send a copy of the invoice to email.  Optionally, change the `emailAddress`

3. Fetch a copy of the invoice in Base64 format. Use any public website to convert Base64 into pdf to view it, for example [Base64 Guru](https://base64.guru/converter/decode/pdf).
