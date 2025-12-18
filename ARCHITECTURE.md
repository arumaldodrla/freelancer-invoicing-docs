# Architecture

This document outlines the architecture of the Freelancer Invoicing & Gig Income Tracking application. It covers the system context, components, data flows, and key design decisions.

## 1. System Context Diagram

This diagram shows the overall system landscape and how the application interacts with external systems and users.

```mermaid
graph TD
    subgraph "Freelancer App"
        A[Frontend - Vercel] --> B{Backend - Supabase};
    end

    subgraph "Users"
        C[Freelancer] --> A;
    end

    subgraph "External Services"
        B --> D[Zoho CRM];
        B --> E[Zoho Billing];
        B --> F[Zoho Books];
        B --> G[Zoho Desk];
        B --> H[Authorize.net];
        B --> I[Fiverr, Upwork, etc.];
        B --> J[Gemini Vision];
        B --> K[LLM - Gemini/Claude/OpenAI];
        B --> L[Resend/Zoho Mail];
    end
```

## 2. Component Diagram

This diagram breaks down the system into its core components and their relationships.

```mermaid
graph TD
    subgraph "Frontend (Vercel)"
        A[React App - Refine] --> B(Supabase Auth);
        A --> C{Backend API - Supabase Edge Functions};
    end

    subgraph "Backend (Supabase)"
        C --> D[PostgreSQL Database];
        C --> E[Supabase Storage];
        F[Supabase Cron] --> C;
    end

    subgraph "Integrations"
        C --> G[Zoho Services];
        C --> H[Authorize.net];
        C --> I[Gig Platforms];
        C --> J[AI Services];
    end
```

## 3. Data Flow Diagrams

These diagrams illustrate the sequence of operations for key user flows.

### a) Signup & Trial

```mermaid
sequenceDiagram
    participant User
    participant Frontend
    participant Backend
    participant ZohoCRM
    participant ZohoBilling

    User->>Frontend: Fills out signup form
    Frontend->>Backend: Creates user
    Backend->>ZohoCRM: Creates contact
    Backend->>ZohoBilling: Creates trial subscription
    Backend-->>Frontend: Signup successful
    Frontend-->>User: Navigates to dashboard
```

### b) Connect Income Source

```mermaid
sequenceDiagram
    participant User
    participant Frontend
    participant Backend

    User->>Frontend: Selects income source
    Frontend->>Backend: Initiates OAuth flow
    Backend-->>Frontend: Redirects to provider
    User->>Backend: Authorizes access
    Backend->>Backend: Stores encrypted tokens
    Backend-->>Frontend: Connection successful
```

### c) Scheduled Sync

```mermaid
sequenceDiagram
    participant CronJob
    participant Backend
    participant ZohoBooks

    CronJob->>Backend: Triggers sync
    Backend->>Backend: Fetches data from platforms
    Backend->>Backend: Normalizes and stores transactions
    Backend->>ZohoBooks: Updates accounting data
    Backend->>Backend: Recalculates tax summary
```

### d) Billing Upgrade

```mermaid
sequenceDiagram
    participant User
    participant Frontend
    participant Backend
    participant AuthorizeNet
    participant ZohoBilling

    User->>Frontend: Clicks upgrade
    Frontend->>AuthorizeNet: Displays hosted payment form
    User->>AuthorizeNet: Enters card details
    AuthorizeNet->>Backend: Returns payment token
    Backend->>ZohoBilling: Updates payment method
    Backend->>ZohoBilling: Activates subscription
    Backend-->>Frontend: Upgrade successful
```

### e) AI Support Escalation

```mermaid
sequenceDiagram
    participant User
    participant AI_Assistant
    participant ZohoDesk

    User->>AI_Assistant: "I need to talk to a human"
    AI_Assistant->>ZohoDesk: Creates ticket with context
    AI_Assistant-->>User: "A support ticket has been created."
```

## 4. Environment Separation

The application will have three environments: `dev`, `staging`, and `prod`. Each environment will have its own separate Supabase project, Vercel project, and API keys. This ensures that development and testing activities do not impact the production environment.

## 5. Key Design Decisions

- **Zoho as System of Record:** Zoho will be the single source of truth for all customer-related data, including CRM, billing, and support. However, the user interface for these functions will be built into our platform to provide a seamless user experience.
- **Authorize.net for Payments:** We will use Authorize.net for payment processing, leveraging their hosted payment forms to minimize our PCI-DSS scope. The primary integration path will be through Zoho Billing, with a direct integration as a fallback option if needed.
- **AI-First Support:** The primary support channel will be an in-app AI assistant, with human support available as an escalation path.
