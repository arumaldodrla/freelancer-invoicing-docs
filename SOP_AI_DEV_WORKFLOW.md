# SOP: AI Development Workflow for Google Antigravity

## 1. Repository Conventions

- **Monorepo:** The project will be managed in a single repository.
- **Directory Structure:**
    - `/app`: Frontend React application (Refine + Tailwind + Metronic)
    - `/supabase`: Backend Supabase project (migrations, functions, etc.)
    - `/docs`: All project documentation (this document set)

## 2. Branching & Pull Request (PR) Process

- **Branching Strategy:**
    - `main`: Production branch. All code on this branch must be deployable.
    - `develop`: Integration branch. All feature branches are merged into this branch.
    - `feature/<feature-name>`: Feature branches. Each new feature should be developed in its own branch.
- **Pull Request (PR) Process:**
    - All PRs must be reviewed and approved by at least one human engineer.
    - PRs must include a clear description of the changes and a link to the relevant user story or task.
    - All PRs must pass all automated tests before they can be merged.

## 3. AI Agent Roles

- **Architect:** Responsible for the overall system design and architecture.
- **Backend Developer:** Responsible for implementing the Supabase backend, including the database schema, API functions, and integrations.
- **Frontend Developer:** Responsible for implementing the React frontend, including the UI, components, and state management.
- **QA Engineer:** Responsible for testing the application, including writing and executing automated tests.
- **Security Engineer:** Responsible for ensuring the application is secure and compliant with all relevant regulations.
- **DevOps Engineer:** Responsible for the CI/CD pipeline, deployment, and infrastructure.

## 4. Definition of Done

A feature is considered "done" when:

- The code has been reviewed and approved.
- All automated tests have passed.
- The feature has been tested and verified by a QA engineer.
- The documentation has been updated.
- The feature has been deployed to the staging environment.

## 5. Human Approval Gates

- **Code Merges to `main`:** All PRs to the `main` branch must be reviewed and approved by a human engineer.
- **Production Deployments:** Deployments to the production environment require manual approval.
- **Schema Migrations:** Any changes to the database schema in the production environment must be manually approved.
- **Security and Compliance Changes:** Any modifications to security policies, access controls, or compliance-related logic must be reviewed and approved by a human.

## 6. Release Checklist (Staging to Prod)

1.  [ ] All automated tests have passed.
2.  [ ] The release has been tested and verified by a QA engineer in the staging environment.
3.  [ ] The documentation has been updated.
4.  [ ] The release has been approved by a human engineer.
5.  [ ] The release has been deployed to the production environment.
6.  [ ] The production environment has been monitored for any issues after the release.

## 7. Incident Response Workflow Handoff

In the event of a production incident, the on-call engineer will be notified immediately. The incident response workflow is documented in `OBSERVABILITY_INCIDENTS.md`.
