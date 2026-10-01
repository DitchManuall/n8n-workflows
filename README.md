# DitchManual n8n Workflows

This private repository is used to store DitchManual's n8n workflow exports, example configuration files, and related documentation.

The goal is to keep automation files organized, reviewable, and protected from accidental changes.

## Repository Structure

### `workflows/production/`
Contains approved n8n workflow exports that are intended for production use.

### `workflows/testing/`
Contains workflows that are still being tested or developed.

Changes should be tested here before being treated as production-ready.

### `configs/`
Contains example configuration files showing what settings a workflow may require.

Real passwords, API keys, authentication tokens, or other secrets must never be stored in this repository.

For example, the `example.env` file only shows placeholder variable names.

### `docs/`
Contains supporting documentation, including the GitHub access policy.

## Security

This repository is private because workflow exports can contain information about how DitchManual's automation systems operate.

Sensitive credentials should be stored securely outside GitHub, such as inside n8n's credential manager or another approved secret-management system.

The `.gitignore` file also helps prevent local environment files and secrets from being committed accidentally.

## Making Changes

The recommended workflow is:

1. Create or update an n8n workflow.
2. Export the workflow as JSON.
3. Place test versions in `workflows/testing/`.
4. Review and test the workflow.
5. Create a branch and pull request for changes intended for production.
6. After approval, merge the change into `main`.

The `main` branch represents the trusted version of the repository.

## Access

Access is based on the principle of least privilege.

People should only receive the permission level required for their role.

Full details are available in:

`docs/ACCESS_POLICY.md`

## Important Rule

Never commit:

- Passwords
- API keys
- Twilio authentication tokens
- Airtable personal access tokens
- n8n credentials
- Private keys
- Production secrets

If a secret is accidentally committed, it should be revoked and replaced immediately rather than simply deleting it from the repository.
## Tiered Automation Structure

Ditch Manual now uses a client-level tier configuration in Airtable to control which n8n modules are active.

### Basic Tier
- Unified Intake Router
- No-Show & Cancellation Recovery

### Premium Tier
- Unified Intake Router
- No-Show & Cancellation Recovery
- Maintenance Rebooking Engine
- Post-Treatment Review & Retention

Each workflow checks the client configuration before running. If a module is enabled, the workflow continues. If it is disabled, the workflow stops before the existing logic runs.

This means a client can upgrade from Basic to Premium by updating the Airtable configuration only. The underlying n8n workflow does not need to be rebuilt.
## Failure-mode testing

The No-Show & Cancellation Recovery workflow was tested against a few common failure cases to see how it behaves when input or external services do not work as expected.

### 1. Missing phone number
If the incoming webhook does not contain a phone number, the Twilio `To` field now falls back to an empty value instead of returning `undefined`.

The Twilio node is also configured to continue through the error output, so a failed SMS does not stop the entire workflow.

### 2. Temporary Twilio failure
The first Twilio SMS node now has `Retry On Fail` enabled.

If the SMS request fails temporarily, n8n retries the action before passing the failure through the error output.

### 3. Invalid appointment status
The workflow only continues when the webhook status is:

- `no-show`
- `cancelled`

Any unsupported or malformed status is stopped before the SMS step.

### 4. Duplicate webhook test
I also tested sending the same webhook request twice. This created two separate workflow executions, which means duplicate requests can currently be processed more than once.

A future improvement would be to add an idempotency check using a unique event ID so repeated webhook events can be ignored safely.

### Updated workflow
The updated export is:

`02 — No-Show & Cancellation Recovery`
