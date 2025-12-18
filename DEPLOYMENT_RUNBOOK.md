# Deployment Runbook

This document provides instructions for deploying and managing the Freelancer Invoicing & Gig Income Tracking application.

## 1. Environments

The application has three environments:

- **`dev`:** For development and testing.
- **`staging`:** A mirror of the production environment for QA and pre-production testing.
- **`prod`:** The live production environment.

Each environment has its own Supabase project and Vercel project.

## 2. Environment Variables

All environment variables, including API keys and secrets, are managed in the Vercel and Supabase secret stores. A full list of environment variables is maintained in the project's internal documentation.

## 3. Setup from Zero to Production

1.  **Create Supabase and Vercel projects for each environment.**
2.  **Configure the environment variables in each project.**
3.  **Run the database migrations in the `dev` environment.**
4.  **Deploy the application to the `dev` environment.**
5.  **Test the application in the `dev` environment.**
6.  **Promote the release to the `staging` environment.**
7.  **Test the application in the `staging` environment.**
8.  **Get human approval for the production deployment.**
9.  **Deploy the application to the `prod` environment.**

## 4. CI/CD with Human Approval

The CI/CD pipeline is managed using GitHub Actions. All pull requests to the `main` branch must be reviewed and approved by a human engineer. Production deployments require an additional manual approval step in the GitHub Actions workflow.

## 5. Rollback Plan

In the event of a failed deployment, the previous version of the application can be redeployed from the Vercel dashboard. The database can be restored from a backup if necessary.

## 6. Feature Flags

Feature flags are used to enable or disable features in the application without deploying new code. This allows for a gradual rollout of new features and provides a quick way to disable a feature if it is causing problems.
