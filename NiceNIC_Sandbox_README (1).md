# NiceNIC Domain API Sandbox

**Test your Domain API integration before going live.**

NiceNIC API Sandbox gives developers a dedicated environment to test authentication, API requests, and application workflows without creating real domain orders or incurring real charges.

Provided by **NiceNIC, an ICANN-accredited domain registrar since 2006**.

[Create an Account](https://nicenic.com/user/register.php) · [Sandbox Documentation](https://nicenic.com/reseller/apiv2.php?api_type=sandbox&sandbox=1) · [Domain API](https://nicenic.com/reseller/apiv2.php) · [Contact Support](https://nicenic.com/ctrl_support/question.php)

## Overview

Use the Sandbox when building a hosting platform, reseller system, domain management application, or custom Domain API integration.

It helps you check:

- API authentication and connectivity.
- Request formatting and required parameters.
- Response parsing and error handling.
- Your application's workflow before production deployment.

This repository is the documentation entry point for the hosted NiceNIC API Sandbox. No local Sandbox server installation is required.

## Get Started

### 1. Create or sign in to your NiceNIC account

[Create an account](https://nicenic.com/user/register.php), or use your existing NiceNIC account.

Domain API access is available to active Market and Reseller Accounts. API access and reseller pricing are separate.

### 2. Generate your Sandbox API Secret

Open [API Settings](https://nicenic.com/user/api_setting.php) and generate a Sandbox API Secret. Use your NiceNIC account username together with this secret for Sandbox authentication.

Keep Sandbox and production credentials separate.

### 3. Connect your application

**Sandbox endpoint:**

`https://sandbox-api.nicenic.net/v2/`

Follow the [Sandbox documentation](https://nicenic.com/reseller/apiv2.php?api_type=sandbox&sandbox=1) for authentication and connection instructions. Refer to the [Domain API documentation](https://nicenic.com/reseller/apiv2.php) for operation parameters and response definitions.

### 4. Validate your workflow

Start with a domain availability query, then test the operations your application requires. Confirm their availability in the Sandbox and verify how your application handles successful requests, errors, and pending results where applicable.

## Sandbox Environment

- Sandbox operations do not create real domain orders or incur real charges.
- Sandbox data may be reset periodically.
- Sandbox credentials are separate from production credentials.
- Live availability, prices, and registry requirements must be checked in production.

## Going Live

After completing your integration tests, configure your application with the production endpoint and production API credentials described in the [Domain API documentation](https://nicenic.com/reseller/apiv2.php).

Before enabling paid operations, verify your account balance, current prices, required contact information, and the requirements of each domain extension. Production operations may incur charges.

## For Hosting Companies and Domain Resellers

Connect domain services to your existing platform through the [NiceNIC Domain API](https://nicenic.com/reseller/apiv2.php), or explore the [WHMCS integration](https://nicenic.com/reseller/whmcs.php).

For account-level reseller pricing, visit the [NiceNIC Reseller Program](https://nicenic.com/reseller/).

## Support

For authentication, account access, or integration questions, [submit a support ticket](https://nicenic.com/ctrl_support/question.php).

Include the affected operation, error message, and a sanitized request or response when relevant. Keep API secrets and private account information out of public GitHub issues.

## Official Resources

- [Sandbox Documentation](https://nicenic.com/reseller/apiv2.php?api_type=sandbox&sandbox=1)
- [API Settings](https://nicenic.com/user/api_setting.php)
- [Domain API Documentation](https://nicenic.com/reseller/apiv2.php)
- [NiceNIC MCP](https://nicenic.com/reseller/mcp.php)
- [WHMCS Integration](https://nicenic.com/reseller/whmcs.php)
- [Reseller Program](https://nicenic.com/reseller/)
- [NiceNIC Trust Center](https://nicenic.com/trust-center/)
