# NiceNIC WHMCS Domain Registrar Module

**Official ICANN Registrar Module for WHMCS with 0% Fee Crypto Billing**

Connect your WHMCS store to NiceNIC to register, renew, transfer and manage customer domains through the NiceNIC Domain API.

NiceNIC is an ICANN-accredited domain registrar serving customers since 2006, IANA ID 3765.

[Create a NiceNIC Account](https://nicenic.com/user/register.php) · [Module Downloads](https://nicenic.com/reseller/apiv2.php?api_type=whmcs&whmcs=1) · [Reseller Program](https://nicenic.com/reseller/) · [Domain API](https://nicenic.com/reseller/apiv2.php)

**About crypto billing:** The 0% fee refers to NiceNIC’s own crypto processing fee when funding your NiceNIC account. Payment-provider, wallet and network fees may apply. Your WHMCS customer checkout uses the payment gateways you configure separately. See [Payment Options](https://nicenic.com/payment-options.php) for current costs.

## Contents

* [Overview](#overview)
* [Compatibility and Requirements](#compatibility-and-requirements)
* [Installation](#installation)
* [Account and Module Configuration](#account-and-module-configuration)
* [Domain Pricing and Order Settings](#domain-pricing-and-order-settings)
* [Sandbox Testing](#sandbox-testing)
* [Usage Walkthroughs](#usage-walkthroughs)
* [Going Live](#going-live)
* [Crypto Account Funding](#crypto-account-funding)
* [Upgrading and Rolling Back](#upgrading-and-rolling-back)
* [Troubleshooting](#troubleshooting)
* [Support and Bug Reports](#support-and-bug-reports)
* [Changelog](#changelog)

## Overview

The module connects WHMCS domain operations to your NiceNIC account.

The [NiceNIC module documentation](https://nicenic.com/reseller/apiv2.php?api_type=whmcs&whmcs=1) lists availability checks, registration, renewal, transfers, domain details, nameserver and contact updates, registrar lock management, and EPP code retrieval.

Operation availability depends on the installed module, domain extension, registry requirements and account permissions.

API access is available to active Market and Reseller Accounts. Reseller pricing is managed separately from API access.

## Compatibility and Requirements

### WHMCS 9.0

**Compatibility verification status: pending for the module package associated with this README.**

WHMCS 9.0 support must be confirmed against an identified module release. Check the release notes for the exact WHMCS and PHP versions tested before installing on a live store.

For WHMCS 9.0, prepare:

* A licensed, self-hosted WHMCS installation.
* PHP 8.2 or another PHP version supported by your WHMCS release.
* The appropriate ionCube Loader for that PHP version.
* PHP cURL and working HTTPS certificate validation.
* A database and server environment meeting WHMCS requirements.

Refer to the [WHMCS 9.0 requirements](https://docs.whmcs.com/releases/9-0/9-0-release-notes/) for the full dependency list.

### NiceNIC and Server Access

You also need:

* An active NiceNIC account and API credentials.
* WHMCS administrator access.
* SFTP, SSH or hosting file-manager access.
* Outbound HTTPS access from your WHMCS server to the required NiceNIC API endpoint.
* Available NiceNIC account credit before submitting paid production orders.

### Before Installation

Back up your WHMCS database, files and any existing NiceNIC module. Perform the initial installation on a separate WHMCS test instance.

Keep test orders, test customers and test payment settings separate from your live store.

## Installation

### 1. Obtain the Module

Open the official [NiceNIC module download page](https://nicenic.com/reseller/apiv2.php?api_type=whmcs&whmcs=1).

Select a package appropriate for your WHMCS and PHP versions. If the package does not explicitly identify WHMCS 9.0 compatibility, confirm the correct package with NiceNIC support before proceeding.

Extract the archive locally and locate the `nicenic` registrar module directory.

### 2. Upload the Files

Upload the module directory to:

`<WHMCS_ROOT>/modules/registrars/nicenic/`

Preserve the package’s internal file structure. Avoid placing the module inside an extra archive-name directory.

Check that the PHP process serving WHMCS can read the files. Use your hosting environment’s normal ownership and permissions; do not make the directory world-writable.

### 3. Activate NiceNIC

In WHMCS, open:

**Configuration → System Settings → Domain Registrars**

Find **NiceNIC**, activate it and open its configuration.

If the module does not appear, check the upload location, file permissions and PHP error log.

See [WHMCS registrar setup instructions](https://docs.whmcs.com/9-0/domains/domain-registration-tutorials/set-up-a-domain-registrar/) for the administrator workflow.

## Account and Module Configuration

### 1. Prepare Your Credentials

Sign in to [NiceNIC API Settings](https://nicenic.com/user/api_setting.php).

Prepare credentials for the environment you intend to use. Store secrets privately and keep a record of which application uses each credential.

### 2. Configure the Module

The public NiceNIC installation guide describes these settings:

| Setting    | What to enter                                                                                     |
| ---------- | ------------------------------------------------------------------------------------------------- |
| Username   | Your NiceNIC account username                                                                     |
| API Secret | The API secret for the selected environment                                                       |
| Test Mode  | Enable only after confirming the installed package routes test requests to the documented Sandbox |

Save your settings.

If the installed package presents different fields, follow its release-specific instructions or contact support. Do not substitute your account login password for an API secret.

### 3. Verify Connectivity

Start with a read-only module operation supported by your package.

Confirm that the operation reaches the intended NiceNIC environment and returns an understandable result. Saving configuration alone does not verify authentication.

## Domain Pricing and Order Settings

### Configure the Extensions You Sell

Open **Configuration → System Settings → Domain Pricing** in WHMCS.

For each extension:

1. Add the extension.
2. Set customer registration, renewal and transfer prices for the supported terms.
3. Select **NiceNIC** under **Auto Registration** when you are ready to route orders through the module.
4. Save and check the customer-facing order form.

See [WHMCS Domain Pricing](https://docs.whmcs.com/9-0/domains/pricing-and-configuration/domain-pricing/) for configuration details.

### Check Your Selling Prices

Your WHMCS retail prices and NiceNIC account costs are separate.

Before enabling an extension, review:

* Registration, renewal and transfer costs.
* Currency conversion and your margin.
* Available registration periods.
* Premium-domain handling.
* Required registration fields and eligibility information.

Only advertise optional features that have been verified in your installed module. This includes automated pricing imports, premium-domain checkout, DNS management and privacy controls.

### Review Order Automation

Choose how orders are accepted and when registrar actions are submitted. Test those settings before enabling unattended processing.

Check your WHMCS Cron configuration and renewal settings. Confirm domain-status synchronization support for the installed NiceNIC module; schedule manual checks where synchronization is unavailable.

## Sandbox Testing

The [NiceNIC Sandbox](https://nicenic.com/reseller/apiv2.php?api_type=sandbox&sandbox=1) supports integration testing without real domain orders or charges. Test data may be reset.

### Prepare the Test Environment

1. Use a separate WHMCS test installation.
2. Generate a Sandbox API Secret in NiceNIC API Settings.
3. Confirm that your module’s Test Mode uses `https://sandbox-api.nicenic.net/v2/`.
4. Enter your username and Sandbox secret, then enable the verified test setting.
5. Submit a read-only request and confirm the destination.

**If the module’s Sandbox routing has not been verified, stop before submitting registration, renewal or transfer actions.**

### Test Before Production

Run the following scenarios where supported by the Sandbox and module:

* A valid availability request.
* Invalid credentials.
* Missing or invalid contact information.
* A registration request and its resulting status.
* A pending operation.
* A nameserver update followed by a read-back.
* An interrupted or timed-out request.
* Repeated submission of the same order.

For each test, record the expected result, actual result and any follow-up action.

Use a test payment method on the test installation. Do not collect real customer payments for demonstration orders.

## Usage Walkthroughs

These walkthroughs describe the actions to perform and results to verify. They are not records of completed tests.

### Demo 1: Search for a Domain

**Goal:** Verify the customer’s domain-search experience.

1. Open your WHMCS storefront.
2. Enter a test domain under an extension you configured.
3. Run the search.
4. Check the availability message and displayed retail price.
5. Continue to the cart and verify the registration term.

**Verify:** The price matches your WHMCS configuration, and the result is suitable for checkout.

Check which lookup provider handled the search. A successful search through another provider does not confirm NiceNIC API authentication.

### Demo 2: Submit a Test Registration

**Goal:** Verify order submission and result handling.

1. Complete the Sandbox setup above.
2. Create a test customer and domain order.
3. Enter the required contact information and nameservers.
4. Open the customer’s domain record in the WHMCS Admin Area.
5. Confirm the selected registrar is NiceNIC.
6. Submit the registration once using the available registrar action.
7. Review the returned message, module log and resulting domain state.

**Verify:** The request reaches the Sandbox, and WHMCS represents the result accurately. Investigate pending or unclear results before submitting again.

For the administrator workflow, see [Manually Register a Domain](https://docs.whmcs.com/9-0/domains/domain-registration-tutorials/manually-register-a-domain/).

### Demo 3: Update Nameservers

**Goal:** Verify a management change and its saved result.

1. Select a test domain managed through the integration.
2. Record its current nameservers.
3. Enter the complete intended nameserver list.
4. Save the change.
5. Retrieve the nameservers again.

**Verify:** The returned list matches the requested configuration. A successful save message alone is insufficient.

For production changes, also allow for DNS caching and propagation.

### Demo 4: Review Renewals and Transfers

**Goal:** Verify that longer-running operations remain understandable.

For an eligible test renewal, record the current expiry date, submit once and check the resulting date or pending status.

For a supported test transfer, provide the required transfer information, submit once and follow the operation through its available status checks.

**Verify:** WHMCS distinguishes submission from completion. Record any manual follow-up required by the installed module.

## Going Live

Complete this checklist before accepting live NiceNIC orders:

* The installed module release has been verified for your WHMCS and PHP versions.
* Sandbox tests have passed.
* Production credentials are configured and Test Mode is disabled.
* Requests use the intended production endpoint.
* NiceNIC account credit is available.
* Retail prices, currencies and registration periods are correct.
* Required domain registration fields are collected.
* Payment, order acceptance and renewal settings have been reviewed.
* Failed and pending operations have a defined follow-up process.
* A current backup and previous module package are available.

Submit one deliberately approved live order first. Confirm the domain outcome and account transaction before increasing order volume.

Keep test orders out of the live processing queue.

## Crypto Account Funding

Crypto funding supplies the NiceNIC balance used for eligible registrar operations.

1. Sign in to your NiceNIC account.
2. Open **Add Funds**.
3. Select an available crypto payment route.
4. Check the currency, network, amount and payment instructions.
5. Complete payment and wait for account credit.
6. Confirm the available balance before submitting paid domain operations.

NiceNIC adds a **0% processing fee**. The online crypto provider currently charges a **1.5% service fee**, and wallet or blockchain fees may apply. Consult the [current payment information](https://nicenic.com/payment-options.php) before paying.

Payment from a customer to your WHMCS store does not automatically top up your NiceNIC account. Monitor the registrar balance as part of daily operations.

## Upgrading and Rolling Back

### Upgrade

1. Read the new module’s release notes and migration instructions.
2. Back up your files, database and current module configuration.
3. Test the upgrade on your WHMCS test installation.
4. Temporarily pause new registrar submissions and automated jobs that could call the module during replacement.
5. Replace the module files according to the package instructions.
6. Verify credentials, environment selection and domain assignments.
7. Run a read-only check, inspect logs and resume processing.

Reconcile pending operations before retrying them after the upgrade.

### Roll Back

If an upgrade introduces a problem:

1. Pause affected registrar submissions.
2. Save redacted error details.
3. Restore the previous module files and compatible configuration using the release’s rollback instructions.
4. Verify connectivity and existing domain access.
5. Reconcile operations submitted during the affected period.

Restoring local files does not reverse domain actions already accepted by NiceNIC. Review recent orders before considering a database restore, which may remove newer billing records.

## Troubleshooting

| Problem                                            | What to check                                                                                   |
| -------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| NiceNIC is missing from Domain Registrars          | Module directory location, nested folders, read permissions and PHP loading errors              |
| Authentication fails                               | Username, matching environment secret, accidental whitespace and configured access restrictions |
| A connection times out                             | Server DNS, outbound HTTPS, TLS certificate validation and upstream availability                |
| Search works but registration fails                | The actual lookup provider, registrar credentials, balance and required registration data       |
| An order remains pending                           | Registrar response and current domain state; confirm the outcome before retrying                |
| Customer payment succeeded but provisioning failed | NiceNIC balance, order automation settings and the module error                                 |
| The price shown to customers is unexpected         | WHMCS retail pricing, currency settings, registration term and premium status                   |
| A management option is missing                     | Whether the installed module and domain extension support that operation                        |
| Renewal or transfer status is stale                | Cron execution, module synchronization support and the latest registrar state                   |
| Errors appear after a WHMCS upgrade                | Module compatibility, PHP version, dependencies and third-party customizations                  |

### Collect Diagnostic Information

Open the WHMCS system logs and locate the Module Log where available.

Enable diagnostic logging only while reproducing the issue, inspect what it captures and disable it afterwards. Remove API secrets, authorization headers, EPP codes and customer information before sharing logs.

For an uncertain paid operation, confirm the registrar outcome before retrying. See [WHMCS registrar action retries](https://docs.whmcs.com/9-0/domains/domain-registration-tutorials/retry-a-module-action/).

## Support and Bug Reports

Email [support@nicenic.net](mailto:support@nicenic.net) for installation assistance or account-specific issues.

Use [GitHub Issues](https://github.com/nicenic-official/nicenic-whmcs-module/issues) for reproducible, non-sensitive technical problems.

Include:

* NiceNIC module version or package filename.
* WHMCS version.
* PHP version.
* Sandbox or production environment.
* Operation and timestamp, including timezone.
* Steps to reproduce.
* Expected and actual results.
* Redacted error output.

Send affected domain names and order references privately when they relate to customer accounts.

## Changelog

This changelog separates documentation work from verified software releases.

### Unreleased

**Documentation**

* Added installation and module configuration instructions.
* Added domain pricing and order-setting guidance.
* Added Sandbox preparation and test scenarios.
* Added usage walkthroughs with verification steps.
* Added production rollout, upgrade and rollback procedures.
* Added troubleshooting and support-report requirements.
* Clarified the scope of 0% NiceNIC crypto processing fees.

**Release verification pending**

* Identify the module version and downloadable package.
* Record the exact WHMCS 9.0.x and PHP versions tested.
* Confirm Test Mode routes requests to the documented Sandbox.
* Record results for registration, renewal, transfer and management operations.
* Document supported synchronization features and known limitations.

### Published Releases

No verified module release history has been added to this README yet.

For each published release, record the module version, release date, tested environments, added or changed features, fixes, known issues and upgrade instructions.
