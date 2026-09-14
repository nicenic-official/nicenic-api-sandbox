# NiceNIC Domain API Sandbox

Official getting-started guide for testing a NiceNIC Domain API integration.

Building a hosting platform, reseller service or domain management application? Start with the [NiceNIC Sandbox documentation](https://nicenic.com/reseller/api-sandbox.php).

## Repository Scope

This repository provides setup instructions, a first-request example and an integration checklist for the hosted NiceNIC Sandbox.

## Requirements

* A [NiceNIC account](https://nicenic.com/user/register.php).
* A Sandbox API Secret generated in [API Settings](https://nicenic.com/user/api_setting.php).
* An HTTP client such as Postman or cURL.

## Connect to the Sandbox

**Base endpoint:** `https://sandbox-api.nicenic.net/v2/`

Send these headers with your request:

* `Authorization: username:sandbox_api_secret`
* `Content-Type: application/json`

Replace the placeholders with your NiceNIC username and Sandbox API Secret. Keep credentials in private environment variables.

## First Request: Check a Domain

In your HTTP client, select **GET** and enter:

`https://sandbox-api.nicenic.net/v2/?category=domain&action=check&domains=example.com`

Add the headers above and send the request. Inspect the returned body for the API result.

This checks connectivity, authentication and response parsing.

## Testing Checklist

Before connecting your application to production:

* Confirm valid credentials work and invalid credentials are handled clearly.
* Test missing parameters and malformed input.
* Handle unsuccessful responses without reporting success to the customer.
* Test timeouts and interrupted connections.
* Prevent repeated clicks or retries from creating duplicate orders.
* Keep credentials out of logs, screenshots and Git commits.

Sandbox activity creates no real domain orders or charges. Test data may be reset.

## Move to Production

Switch to `https://api.nicenic.net/v2/` and use production credentials.

Review current prices, available account balance and order details before submitting a live operation. Treat Sandbox results as integration tests, not guarantees of live availability.

## Troubleshooting

**Authentication fails:** Confirm the username, secret and environment match.

**Unexpected response:** Save a redacted request and response, including the request time, for investigation.

**Connection fails:** Check outbound HTTPS access from the machine running your integration.

## Documentation and Support

* [Domain API Reference](https://nicenic.com/reseller/apiv2.php)
* [WHMCS Integration](https://nicenic.com/reseller/apiv2.php?api_type=whmcs&whmcs=1)
* [Reseller Program](https://nicenic.com/reseller/)
* [Contact NiceNIC](https://nicenic.com/contact.php)

For support, include the operation, timestamp, error message and steps to reproduce. Remove secrets and customer information from public reports.

## Changelog

### Unreleased

* Prepared the initial Sandbox setup guide.
* Added a domain availability request example.
* Added testing, troubleshooting and production migration checklists.
