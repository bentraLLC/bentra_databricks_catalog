# bentra_databricks_catalog

Bento form and workflow prototype for a future Databricks catalog automation use case.

This repository currently contains a Bento form definition and a placeholder workflow. Today it is best understood as a prototype and syntax demo rather than a working Databricks catalog provisioning flow, with the form serving as the main demonstration of input handling, validation, conditional logic, and computed values that are useful for infrastructure automation.

## Overview

Databricks catalogs are a key part of Unity Catalog governance. A catalog typically sits near the top of the object hierarchy and helps organize schemas, tables, views, volumes, permissions, and ownership boundaries across teams and environments.

This project is intended to evolve into a workflow that can:

- collect catalog creation inputs from users
- validate required metadata before execution
- enforce environment-specific rules
- generate consistent naming and ownership conventions
- drive downstream Databricks provisioning steps

Today, the repository is a prototype rather than a complete provisioning implementation, but it already captures many of the form patterns needed for a real platform workflow.

## Repository Structure

```text
.
├── README.md
└── .bento/
    ├── form/
    │   └── form.yml
    └── workflow/
        └── workflow.yml
```

## Current Contents

### Form Definition

The form in `.bento/form/form.yml` is the most complete part of the repository. It is currently a generic Bento capability and QA fixture that exercises a broad range of input features, and it would still need to be narrowed into Databricks-specific request fields for real catalog provisioning.

Included examples cover:

- text, email, password, number, and date inputs
- plain text and markdown textareas
- single-select and multi-select dropdowns
- radio buttons and checkbox groups
- required fields and regex validation
- numeric and string length constraints
- conditional field visibility
- dynamic option maps
- auto-populated fields
- computed read-only fields
- inline custom validators
- inline JavaScript-based computed values

These patterns map well to future Databricks workflows, where requests often need strong validation and context-aware inputs.

### Workflow Definition

The workflow in `.bento/workflow/workflow.yml` is currently a placeholder example. It provides the basic Bento workflow shape but does not yet create a Databricks catalog or interact with Databricks APIs or CLI tooling.

## How This Fits a Databricks Catalog Workflow

A more complete version of this repository would typically collect inputs such as:

- catalog name
- environment
- owning team
- owner email or group
- cloud provider and region
- data classification
- storage or external location details
- approval metadata
- notification preferences

Those inputs could then be used to automate steps such as:

- creating the catalog
- assigning ownership
- creating one or more default schemas
- applying grants for groups or service principals
- attaching storage configuration
- enforcing naming and governance policies

## Example Use Cases

This kind of workflow is useful for teams that want a self-service front door for platform requests, including:

- provisioning a new catalog for a product or analytics team
- creating a sandbox catalog for experimentation
- standardizing production catalog requests
- collecting governance metadata up front
- reducing manual setup performed by platform operators

## Form Patterns Relevant to Infrastructure Automation

Even though the current form content is generic, several of the included patterns are directly useful for real infrastructure workflows.

### Validation

Provisioning forms usually need stricter validation than general application forms. Common examples include:

- naming conventions
- required owner metadata
- allowed environment values
- approval acknowledgements
- retention or cost-related numeric limits

### Dynamic Behavior

Infrastructure forms often need follow-up questions that depend on earlier answers. For example:

- region options can depend on the selected cloud provider
- production confirmations can appear only when `prod` is selected
- backup-related fields can appear only when backup is enabled
- encryption settings can be shown only for certain clouds or feature flags

### Computed Values

Computed fields are useful for generating:

- standardized resource names
- tags or labels
- estimated monthly cost hints
- derived values passed into downstream automation

## Databricks Catalog Design Notes

When extending this template into a real Databricks catalog workflow, these design areas are usually worth documenting early.

### Naming

Catalog names should be predictable and easy to govern. Common approaches include team, domain, or environment prefixes.

Examples:

- `finance_dev`
- `marketing_prod`
- `core_analytics`
- `sandbox_data_science`

### Ownership

Every catalog should have a clear owner, such as:

- a team group
- a data platform admin group
- a service principal
- a data steward or domain owner

### Access Model

A request workflow should make access expectations explicit. Common questions include:

- who can create schemas?
- who can read production data?
- who can manage grants?
- should write access be limited to service identities?

### Environment Boundaries

Many teams separate catalogs by lifecycle or sensitivity. Typical patterns include:

- separate development and production catalogs
- additional approvals for production requests
- tighter access controls for sensitive domains
- clearer auditability for regulated datasets

### Metadata and Governance

Capturing metadata during the request process makes governance easier later. Useful metadata often includes:

- owner
- purpose
- data domain
- sensitivity classification
- expected users
- retention expectations
- integration requirements

## Current Limitations

This repository is not yet a complete Databricks catalog automation solution.

Current gaps include:

- no real Databricks provisioning logic
- no Databricks API or CLI integration
- no grants or permissions automation
- no secrets or authentication setup
- no environment-specific policy enforcement
- no example request payloads tied to a real execution path

## Suggested Next Steps

Useful next steps for turning this starter into a real workflow would be:

1. replace the placeholder workflow step with actual provisioning logic
2. narrow the generic demo form into Databricks-specific inputs
3. define naming, ownership, and approval rules
4. add environment-aware validation for production requests
5. document required credentials and execution environment
6. add examples of expected inputs and resulting actions

## Summary

This repository is currently best viewed as a Bento prototype for a future Databricks catalog automation workflow. Its strongest current value is the form definition, which demonstrates many of the dynamic input and validation patterns that could later be adapted into a governed self-service infrastructure workflow.
