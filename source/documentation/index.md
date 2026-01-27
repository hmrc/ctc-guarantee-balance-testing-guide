---
title: CTC Guarantee Balance API testing guide
weight: 1
description: Software developers, designers, product owners or business analysts. Verify the compatibility of your software with CTC Guarantee Balance API and learn how to test your application in our sandbox environment.
---

# CTC Guarantee Balance API testing guide

Learn how to test the compatibility of your software with New Computerised Transit System and [CTC Guarantee Balance API v2.0](/api-documentation/docs/api/service/common-transit-convention-guarantee-balance/2.0).

[Learn about key NCTS5 dates](/guides/ctc-traders-phase5-tis/#ncts5-key-dates).

## Before you start

When you are ready to test your software, first read and understand the [CTC Guarantee Balance API service guide](https://developer.service.hmrc.gov.uk/guides/ctc-guarantee-balance-phase5-service-guide/).

### Scheduling your testing

Before the UK NCTS5 goes live, you will need to check that your software is compatible with both it and CTC Guarantee Balance API v2.0. This involves using test scenarios and predefined test data.

### Trader Test

Trader Test is a test environment that simulates both automated responses and real-life NCTS experience. This includes the Guarantee Management System (GMS) against which you will be able to run your tests.

For information about accessing the NCTS5 Trader Test environment, see [CTC Traders API testing guide](/guides/ctc-traders-phase5-testing-guide/#accessing-trader-test). 

### Testing prerequisites

For information about actions that must be completed before testing, see the quick start section of the [CTC Guarantee Balance API service guide](/guides/ctc-guarantee-balance-phase5-service-guide/#quick-start).

## Navigating CTC Guarantee Balance API v2.0 documentation

The following table lists the documents for CTC Guarantee Balance API v2.0 and outlines the content and intended readers of each document.

<table>
    <thead>
        <tr>
            <th>Document</th>
            <th>Content type</th>
            <th>Granularity</th>
            <th>Summary</th>
            <th>Intended readers</th>
        </tr>
    </thead>
    <tbody>
        <tr>
          <td><a href="https://developer.service.hmrc.gov.uk/roadmaps/ctc-guarantee-balance-roadmap/">CTC Guarantee Balance API roadmap</a> (covers NCTS4 onwards)</td>
            <td>Functional</td>
            <td>High level</td>
            <td><p>Outlines current status of API for each NCTS phase</p><p>Outlines any development plans for API</p></td>
            <td><p>Software developers</p> <p>Technical architects </p> <p>Product managers</p> <p>Business analysts</p></td>
        </tr>
        <tr>
            <td><a href="https://developer.service.hmrc.gov.uk/guides/ctc-traders-phase5-tis/">NCTS phase 5 technical interface specification</a> (TIS)</td>
            <td>Technical (business logic/rules)</td>
            <td>Low level</td>
            <td><p>Captures UK implementation of NCTS5</p> <p>Shows NCTS5 process flows</p> <p>Lists the message definitions and rules and conditions involved in the exchange of messages between traders and the NCTS for the departure and arrival of transit movements</p></td>
            <td><p>Software developers</p> <p>Technical architects </p> <p>Product managers</p> <p>Business analysts</p></td>
        </tr>
        <tr>
            <td><a href="https://developer.service.hmrc.gov.uk/guides/ctc-guarantee-balance-phase5-service-guide/">CTC Guarantee Balance API phase 5 service guide</a></td>
            <td>Technical</td>
            <td>High level</td>
            <td><p>How to use the API</p> <p>How to self-onboard</p></td>
            <td><p>Software developers</p> <p>Technical architects</p></td>
        </tr>
        <tr>
            <td><a href="https://developer.service.hmrc.gov.uk/api-documentation/docs/api/service/common-transit-convention-guarantee-balance/2.0/oas/page">CTC Guarantee Balance API v2.0 reference</a></td>
            <td>Technical</td>
            <td>Low level</td>
            <td>How to use each API endpoint</td>
            <td><p>Software developers</p> <p>Technical architects</p></td>
        </tr>
        <tr>
            <td>CTC Guarantee Balance API testing guide (this document)</td>
            <td>Functional</td>
            <td>Low level</td>
            <td><p>How to carry out assurance testing of your application software to ensure that it is compatible with the API</p></td>
            <td><p>Software developers</p> <p>Technical architects </p> <p>Product managers</p> <p>Business analysts</p></td>
        </tr>
    </tbody>
</table>


The order in you which you might read these documents can depend on whether you have previous NCTS experience. The following table recommends 2 possible reading orders but you can read the documents in any order you want.

| Suggested reading order | New NCTS users                    | NCTS4 users migrating to NCTS5    |
|-------------------------|-----------------------------------|-----------------------------------|
| 1                       | Roadmap                           | Service guide                     |
| 2                       | Service guide                     | Technical interface specification |
| 3                       | Technical interface specification | Reference                         |
| 4                       | Reference                         | Testing guide                     |
| 5                       | Testing guide                     | Roadmap                           |

**Note:** If you have NCTS4 experience,  it is important that you read the NCTS5 service guide and API reference carefully to understand all of the differences between NCTS4 and NCTS5. Reading only the NCTS5 technical interface specification will NOT guide you about all of the differences between the 2 NCTS phases.

## Related documentation

- [CTC Guarantee Balance API v2.0 changelog](https://github.com/hmrc/common-transit-convention-guarantee-balance/wiki/CTC-Guarantee-Balance-API-v2.0-changelog) (GitHub)

## Getting help and support

Before contacting us, find out if there is planned API downtime or a technical issue by checking [HMRC API Platform Status](https://api-platform-status.production.tax.service.gov.uk/) and [New Computerised Transit System service availability](https://www.gov.uk/guidance/new-computerised-transit-system-service-availability).

If you have specific questions about the CTC Traders API, contact our Software Developer Support (SDS) Team. You’ll get an initial response within 2 working days.

You can also email questions to [SDSTeam@hmrc.gov.uk](mailto:SDSTeam@hmrc.gov.uk). We might ask for more detailed information when we respond.

## Changelog

You can find the changelog for this document in the [ctc-guarantee-balance-testing-guide](https://github.com/hmrc/ctc-guarantee-balance-testing-guide/wiki) GitHub wiki.
