---
title: CTC Guarantee Balance API testing guide
weight: 1
description: Software developers, designers, product owners or business analysts. Check your Guarantee Balance.
---

# CTC Guarantee Balance API testing guide

## Useful links to our pages

- [CTC Guarantee Balance Service Guide](/guides/ctc-guarantee-balance-service-guide/)
- [CTC Guarantee Balance Documentation](/api-documentation/docs/api/service/common-transit-convention-guarantee-balance/1.0)

## Introduction

This page provides you with all the information you&#39;ll need for developing and testing your API software with our CTC Guarantee Balance API and HMRC systems.

## Before you start

You must understand:

- the CTC Guarantee Balance API provides a snapshot of the guarantee state at the time the request is submitted
- it is possible that even a very short delay could coincide with events that could change your balance information, such as the release of goods at the office of destination replenishing the guarantee amount locked against that movement
- the balance responses could become out of date quickly if you have a lot of transit movements progressing at the same time

We have released the CTC Guarantee Balance API to HMRC&#39;s sandbox environment. You can now run tests once you have finished your software development.

Before you interact with our API, you must authenticate with HMRC. All endpoints in the CTC Guarantee Balance API are subject to User-Restricted Authentication. Further details are given on the [Authorisation](/api-documentation/docs/authorisation) page.

## How to get set up for testing

1. [Register for a developer account](/api-documentation/docs/using-the-hub). You can do this by following the instructions on the [Using the Developer Hub](/api-documentation/docs/using-the-hub) page.
2. [Sign in to the HMRC Developer Hub](/developer/login).
3. Add a new application to the sandbox or open an existing application.
4. In the left panel, click **API Subscriptions** and subscribe to our Common Transit Convention Guarantee Balance API.
5. Create a Client ID and a Client Secret.
6. Use the [Create Test User API](/api-documentation/docs/api/service/api-platform-test-user/1.0) or the [create a test user service](/api-test-user) to create a test user for either an [individual](/api-documentation/docs/api/service/api-platform-test-user/1.0#_create-a-test-user-which-is-an-individual_post_accordion) or an [organisation](/api-documentation/docs/api/service/api-platform-test-user/1.0#_create-a-test-user-which-is-an-organisation_post_accordion). A test user is a dummy Government Gateway user ID for testing in the sandbox.
7. [Authenticate with HMRC](/api-documentation/docs/authorisation) and follow the instructions on the page, which describes the User-Restricted Authentication process.

You should now be able to send requests to the CTC Guarantee Balance API in the sandbox environment.

## Schemas

Here are the main developer files you will need:

- [JSON schema files, ZIP, 5KB (file unzips and downloads)](documentation/figures/CTC_Guarantee_Balance_API_JSON.zip)

The ZIP file contains JSON files. Open in your preferred file viewer.

## What is trader test?

Trader Test is where you can use our sandbox environment to test your software against our RESTful APIs before you are given access to the live environment. This sandbox environment does not support our XML APIs - these must be tested as explained in the [Basic guide for software developers](https://www.gov.uk/government/publications/basic-guide-for-software-developers).

## Test your scenarios

Our API lets software developers and test engineers submit Guarantee Balance request notifications into our sandbox testing environment.

You can test your software by using our sandbox to ensure that its connectivity works properly with HMRC systems.

Trader Test uses the same NCTS and Guarantee Management System code as live production but populated solely with test data. This allows you to test the full journey using your software.

You must:

- Test [common scenarios](#common-scenarios) based on the reference data we provide.
- Check against our JSON schemas to ensure your requests are valid. You can download a zip file with all the CTC Guarantee balance API JSON schemas.

## Common scenarios

Use the following common scenarios to verify that your trader software functions correctly for Guarantee Balance requests. You do this by checking that for each scenario, issuing the associated sample request results in the receipt of the corresponding expected response (both expressed in JSON format).

**IMPORTANT NOTE:** Do not use these Guarantee References (GRN) when testing the CTC Traders API, because this would have a detrimental impact on other users.

These scenarios make use of the following data values for GB and XI:

### GB

- EORI: GB954131533000
- GRN: 22GB0000010000313
- Access Code: AC01
- Current balance: £50,000

### XI

- EORI: XI195624547845
- GRN: 22XI00000100002X7
- Access Code: AC01
- Current balance: £30,000

### Scenario 1: Successful balance response

This scenario verifies that when your software issues a successful balance request, you receive the expected response with the correct balance and currency.

#### Sample Request (GB):

    {
      "taxIdentifier": "GB954131533000",
      "guaranteeReference": "22GB0000010000313",
      "accessCode": "AC01"
    }


#### Expected Response (GB):

    {
      "response": {
        "balance": 50000,
        "currency": "GBP"
      }
    }


#### Sample Request (XI):

    {
      "taxIdentifier": "XI195624547845",
      "guaranteeReference": "22XI00000100002X7",
      "accessCode": "AC01"
    }


#### Expected Response (XI):

    {
      "response": {
        "balance": 30000,
        "currency": "GBP"
      }
    }


### Scenario 2: Resubmitting query within 60 seconds

This scenario verifies that when your software issues a balance request within 60 seconds of the previous one, you receive a response containing an appropriate error message.

#### Sample Request (GB):

    {
      "taxIdentifier": "GB954131533000",
      "guaranteeReference": "22GB0000010000313",
      "accessCode": "AC01"
    }


#### Expected Response (GB):

    {
        "code": "MESSAGE_THROTTLED_OUT",
        "message": "The request for the API is throttled as you have exceeded your quota."
    }


#### Sample Request (XI):

    {
      "taxIdentifier": "XI195624547845",
      "guaranteeReference": "22XI00000100002X7",
      "accessCode": "AC01"
    }


#### Expected Response (XI):

    {
        "code": "MESSAGE_THROTTLED_OUT",
        "message": "The request for the API is throttled as you have exceeded your quota."
    }


### Scenario 3: Invalid request parameters

These scenarios verify that when your software issues a balance request containing invalid request data, you receive the expected response with the relevant error information.

#### Scenario 3.1: Invalid EORI

The following GB scenario uses an invalid EORI:

##### Sample Request (GB):

    {
      "taxIdentifier": "GB000000000000",
      "guaranteeReference": "22GB0000010000313",
      "accessCode": "AC01"
    }


##### Expected Response (GB):

    {
        "code": "FUNCTIONAL_ERROR",
        "message": "The request was rejected by the guarantee management system",
        "response": {
            "errors": [
                {
                    "errorType": 12,
                    "errorPointer": "RC1.TIN"
                },
                {
                    "errorType": 12,
                    "errorPointer": "GRR(1).OTG(1).TIN"
                },
                {
                    "errorType": 26,
                    "errorPointer": "RC1.TIN"
                }
            ]
        }
    }


The following XI scenario uses an invalid EORI:

##### Sample Request (XI):

    {
      "taxIdentifier": "XI99999999999",
      "guaranteeReference": "22XI00000100002X7",
      "accessCode": "AC01"
    }


##### Expected Response (XI):

    {
        "code": "FUNCTIONAL_ERROR",
        "message": "The request was rejected by the guarantee management system",
        "response": {
            "errors": [
                {
                    "errorType": 12,
                    "errorPointer": "RC1.TIN"
                },
                {
                    "errorType": 12,
                    "errorPointer": "GRR(1).OTG(1).TIN"
                },
                {
                    "errorType": 26,
                    "errorPointer": "RC1.TIN"
                }
            ]
        }
    }


#### Scenario 3.2: Invalid GRN

The following GB scenario uses an invalid GRN:

##### Sample Request (GB):

    {
      "taxIdentifier": "GB954131533000",
      "guaranteeReference": "20GB0000000000000",
      "accessCode": "AC01"
    }


##### Expected Response (GB):

    {
        "code":"FUNCTIONAL_ERROR",
        "message":"The request was rejected by the guarantee management system",
        "response":{
            "errors":[
                {
                    "errorType":12,
                    "errorPointer":"GRR(1).Guarantee reference number (GRN)"
                },
                {
                    "errorType":12,
                    "errorPointer":"GRR(1).OTG(1).TIN"
                },
                {
                    "errorType":12,
                    "errorPointer":"GRR(1).ACC(1).Access code"
                }
            ]
        }
    }


The following XI scenario uses an invalid GRN:

##### Sample Request (XI):

    {
      "taxIdentifier": "XI195624547845",
      "guaranteeReference": "22XI0000000000000",
      "accessCode": "AC01"
    }


##### Expected Response (XI):

    {
        "code":"FUNCTIONAL_ERROR",
        "message":"The request was rejected by the guarantee management system",
        "response":{
            "errors":[
                {
                    "errorType":12,
                    "errorPointer":"GRR(1).Guarantee reference number (GRN)"
                },
                {
                    "errorType":12,
                    "errorPointer":"GRR(1).OTG(1).TIN"
                },
                {
                    "errorType":12,
                    "errorPointer":"GRR(1).ACC(1).Access code"
                }
            ]
        }
    }

#### Scenario 3.3: Invalid Access Code

The following GB scenario uses an invalid access code:

##### Sample Request (GB):

    {
      "taxIdentifier": "GB954131533000",
      "guaranteeReference": "22GB0000010000313",
      "accessCode": "AC00"
    }


##### Expected Response (GB):

    {
        "code": "FUNCTIONAL_ERROR",
        "message": "The request was rejected by the guarantee management system",
        "response": {
            "errors": [
                {
                    "errorType": 12,
                    "errorPointer": "GRR(1).ACC(1).Access code"
                }
            ]
        }
    }


The following XI scenario uses an invalid access code:

##### Sample Request (XI):

    {
      "taxIdentifier": "XI195624547845",
      "guaranteeReference": "22XI00000100002X7",
      "accessCode": "AC00"
    }


##### Expected Response (XI):

    {
        "code": "FUNCTIONAL_ERROR",
        "message": "The request was rejected by the guarantee management system",
        "response": {
            "errors": [
                {
                    "errorType": 12,
                    "errorPointer": "GRR(1).ACC(1).Access code"
                }
            ]
        }
    }

#### Scenario 3.4: Invalid Combination of Valid EORI and Valid GRN

The following GB scenario uses an XI EORI by mistake:

##### Sample Request (GB):

    {
      "taxIdentifier": "XI195624547845",
      "guaranteeReference": "22GB0000010000313",
      "accessCode": "AC01"
    }


##### Expected Response (GB):

    {
        "code":"FUNCTIONAL_ERROR",
        "message":"The request was rejected by the guarantee management system",
        "response":{
            "errors":[
                {
                    "errorType":12,
                    "errorPointer":"RC1.TIN"
                },
                {
                    "errorType":12,
                    "errorPointer":"GRR(1).OTG(1).TIN"
                },
                {
                    "errorType":26,
                    "errorPointer":"RC1.TIN"
                }
            ]
        }
    }


The following XI scenario uses a GB EORI by mistake:

##### Sample Request (XI):

    {
      "taxIdentifier": "GB954131533000",
      "guaranteeReference": "22XI00000100002X7",
      "accessCode": "AC01"
    }


##### Expected Response (XI):

    {
        "code": "FUNCTIONAL_ERROR",
        "message": "The request was rejected by the guarantee management system",
        "response": {
            "errors": [
                {
                    "errorType": 12,
                    "errorPointer": "GRR(1).OTG(1).TIN"
                }
            ]
        }
    }


## Submit your test results

Once you are satisfied with your tests and are confident that your software is fully compatible with our API:

1. [Log all your evidence and results on the checklist form (OpenOffice Document)](documentation/figures/CTCGuarantee_Balance_API_Checklist_07-02-22.odt). You must also answer all the questions at the end of the checklist.
2. When you are ready, <a rel="noreferrer noopener" href="mailto: SDSTeam@hmrc.gov.uk">email your completed form to SDSTeam@hmrc.gov.uk.</a>
3. We will check your test evidence using the information you give on this form.
4. When we are satisfied that you have done enough testing, you will be granted access to the live API system.

For further information about the process you need to follow to submit your application for production approval, see [section 4 of Using the Developer Hub](/api-documentation/docs/using-the-hub).

## Troubleshooting

### Checking API service availability

You can check planned API downtime or if there are technical issues:

- [Check HMRC API platform availability](https://api-platform-status.production.tax.service.gov.uk/)
- [Check the NCTS service availability](https://www.gov.uk/government/publications/new-computerised-transit-system-ncts-web-service-availability-and-issues/new-computerised-transit-system-ncts-web-service-availability-and-issues)

### If you need further help and support

<a rel="noreferrer noopener" href="mailto: SDSTeam@hmrc.gov.uk">Email our dedicated software developer support team at SDSTeam@hmrc.gov.uk</a> if you have any questions or difficulties or need additional clarification on this testing process.

For versioning information and a list of errors that you might receive, please refer to the [CTC Guarantee Balance API Definition](/api-documentation/docs/api/service/common-transit-convention-guarantee-balance/1.0) page.

Bookmark and save this page for future reference.
