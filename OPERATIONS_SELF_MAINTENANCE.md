# Operations & Self-Maintenance

This document describes the automated self-maintenance and operational procedures for the Freelancer Invoicing & Gig Income Tracking application.

## 1. Weekly Self-Check Design

A weekly self-check will be performed by a Supabase scheduled function. The self-check will run every Sunday at 02:00 UTC and will perform the following checks:

- **Infrastructure Health:** Ping all critical external services (Zoho APIs, Authorize.net, etc.) to ensure they are reachable.
- **Database Health:** Run a series of SQL queries to check for data integrity issues, such as orphan records and unexpected nulls.
- **Error Trends:** Query the logs for any spikes in API errors or failed syncs.
- **Security Signals:** Look for any suspicious activity, such as multiple failed login attempts from the same IP address.

## 2. SQL Checks

The following SQL checks will be performed as part of the weekly self-check:

- **Orphan Records:** Check for records in child tables that do not have a corresponding record in the parent table.
- **Unexpected Nulls:** Check for null values in columns that are not expected to be null.
- **Index Usage:** Check for any unused or inefficient indexes.
- **Table Size:** Monitor the size of the tables to identify any unexpected growth.

## 3. External Service Health Checks

The self-check will ping the following external services to ensure they are reachable:

- Zoho CRM API
- Zoho Billing API
- Zoho Books API
- Zoho Desk API
- Authorize.net API

## 4. Automated Actions

The following automated actions are allowed:

- Retry failed platform syncs.
- Restart idempotent background jobs.
- Mark an unhealthy integration as `ERROR` and notify the user.

The following automated actions are forbidden and require human supervision:

- Deploying new code or schema.
- Changing tax calculation formulas.
- Altering security or access control logic.

## 5. Ticketing Rules

If the self-check detects a major anomaly, it will automatically create a Zoho Desk ticket with the appropriate severity level (`P1`, `P2`, etc.).

## 6. Reporting Format

After each self-check, a summary report will be emailed to the internal operations and security mailing list. The report will include a summary of the checks performed, any issues found, and any actions taken.
