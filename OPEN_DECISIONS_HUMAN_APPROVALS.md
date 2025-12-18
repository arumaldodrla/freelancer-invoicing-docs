# Open Decisions & Human Approvals

This document lists all open decisions that require human approval before implementation. It is a living document that will be updated as new decisions arise.

## 1. Subprocessor List

- **Decision:** Final list of all subprocessors that will be used by the application.
- **Approval Required:** DPO, Legal

## 2. Data Center Regions

- **Decision:** The specific data center regions that will be used for Supabase, Vercel, and all AI providers.
- **Approval Required:** DPO, Legal

## 3. Retention Durations

- **Decision:** The exact retention durations for each data type, including audit logs, raw platform payloads, and receipts.
- **Approval Required:** DPO, Legal

## 4. AI Support Data Scope

- **Decision:** The exact scope of data that will be visible to the AI support agent.
- **Approval Required:** DPO, Product

## 5. Self-Check Thresholds

- **Decision:** The specific thresholds for the self-check alerting (e.g., when to page a human).
- **Approval Required:** Engineering, DevOps

## 6. Zoho Object Model Decisions

- **Decision:** The specific mapping rules for Zoho objects (e.g., how to handle contact vs. customer mapping).
- **Approval Required:** Engineering, Product

## 7. Tagging Taxonomy

- **Decision:** The final tagging taxonomy for Zoho CRM.
- **Approval Required:** Product, Marketing

## 8. Payment Flow Decision

- **Decision:** Whether to enable the direct Authorize.net fallback in addition to the primary Zoho Billing integration.
- **Approval Required:** Product, Engineering, Finance
