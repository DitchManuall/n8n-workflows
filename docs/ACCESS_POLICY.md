# DitchManual GitHub Access Policy

## Purpose

This document explains who should get access to the DitchManual GitHub organization and what level of access they should receive.

The goal is simple: people should only have the access they actually need to do their work.

## Permission Levels

### Organization Owner
Owners have full control over the GitHub organization.

This level should only be given to trusted company leadership or the person responsible for managing GitHub.

Owners can:
- Add or remove members
- Change organization settings
- Manage repositories
- Manage permissions
- Review security settings

Only a small number of people should have Owner access.

### Repository Admin
Admin access should be given to the person responsible for managing a specific repository.

They can:
- Manage repository settings
- Configure branch protection
- Manage collaborators
- Review and merge changes

Admin access should not be given unless it is genuinely required.

### Write Access
Developers or automation engineers who actively work on n8n workflows can receive Write access.

They can:
- Add or update workflow files
- Create branches
- Open pull requests
- Contribute changes

They should normally make changes through a branch and pull request instead of changing the main branch directly.

### Read Access
Read access is appropriate for people who only need to review the repository.

For example:
- Interns reviewing workflows
- Auditors
- Temporary reviewers
- Non-technical team members

They can view the repository but cannot directly change files.

## Adding New Members

Before someone is added:

1. Confirm that they genuinely need GitHub access.
2. Decide what repository they need access to.
3. Give them the lowest permission level that still allows them to do their job.
4. Avoid giving Admin or Owner access unless absolutely necessary.
5. Record who approved the access.

This follows the principle of least privilege.

## Offboarding Process

When an employee, intern, or contractor leaves DitchManual, their GitHub access should be removed as soon as possible.

The offboarding process is:

1. Remove the person from the GitHub organization.
2. Remove them from any GitHub teams.
3. Confirm they no longer have access to private repositories.
4. Revoke any API tokens, deployment keys, or credentials associated with them.
5. Rotate shared credentials if the person previously had access to them.
6. Review recent repository activity for unexpected changes.
7. Confirm that access has been fully removed.

This is important because removing someone from a repository does not automatically make previously shared credentials safe.

## Why This Matters

The earlier access-control audit showed why offboarding is important.

A person who no longer works with DitchManual should not continue to have access to private workflow files or automation systems.

Removing GitHub access quickly and rotating exposed credentials reduces the risk of unauthorized changes or data access.
