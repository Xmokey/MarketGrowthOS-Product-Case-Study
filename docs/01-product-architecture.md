# MarketGrowthOS Product Architecture

## Purpose

MarketGrowthOS was designed as a multi-tenant SaaS platform in which different merchants operate independently while sharing the same platform infrastructure.

The architecture therefore needed to establish clear boundaries around:

- Tenant ownership
- Users and teams
- Customer records
- Permissions
- CRM lifecycle state
- Marketing execution
- Business workflow orchestration
- Billing state
- External integrations

The objective was not simply to create separate screens for different users, but to establish clear ownership of data and system behaviour across the platform.

---

## Three-Tier Tenant Model

The product is structured around three primary levels:

**Platform → Merchant/Tenant → Customer**

### Platform

The platform represents the overall MarketGrowthOS environment.

It is responsible for platform-level administration and controls that sit above individual merchants.

### Merchant / Tenant

A merchant represents an independent business operating within MarketGrowthOS.

Each merchant has its own:

- Users
- Teams
- Contacts/customers
- CRM records
- Business workflows
- Configuration
- Operational data

A core architectural requirement is that merchant data remains isolated.

A contact belongs to exactly one merchant, and cross-merchant access is prohibited.

### Customer

Customers are the people or organisations being managed by a merchant.

Customer records exist within the context of their merchant and participate in that merchant's CRM, consultation, project, billing and support workflows.

---

## Tenant Provisioning

Tenant provisioning is tied to merchant subscription confirmation.

A prospective merchant can exist at the platform level before subscription confirmation, but the merchant tenant is not provisioned until the subscription requirement has been satisfied.

This separates:

**Prospective Merchant**

from:

**Active Merchant Tenant**

and prevents the platform from treating an unconfirmed business as an operational tenant.

---

## Data Ownership

A central product architecture decision was establishing which system owns which type of information.

MarketGrowthOS is the authority for core business and operational state.

This includes:

- CRM records
- Lifecycle state
- Conversion logic
- Permissions
- Workflow orchestration
- Appointment booking
- Consultation booking
- Billing state

External systems are integrated around those boundaries rather than being allowed to become competing sources of truth.

---

# Integration Boundaries

## MarketGrowthOS and Mautic

Mautic is used as the marketing execution engine.

Mautic handles capabilities such as:

- Forms
- Landing pages
- Campaigns
- Nurture sequences
- Segmentation
- Tags
- Marketing behavioural signals

MarketGrowthOS owns the business state associated with those activities.

The integration therefore operates as a two-way handshake rather than a one-way data export.

### Mautic → MarketGrowthOS

Relevant marketing and activity signals can flow into GrowthOS.

Examples include:

- Form activity
- Landing-page activity
- Marketing signals
- Appointment-related activity where applicable to the integration workflow

### MarketGrowthOS → Mautic

GrowthOS can send business-state information back to Mautic for marketing execution.

Examples include:

- Contact records
- Lifecycle state
- Tags
- Conversion state

The important architectural principle is that synchronization does not transfer ownership of business state.

GrowthOS remains authoritative for the core CRM and operational lifecycle.

---

# MarketGrowthOS and Stripe

Stripe is used at multiple levels of the platform.

## Platform Billing

MarketGrowthOS uses Stripe for platform-level payment processing and subscription billing.

Stripe provides payment and subscription confirmation that GrowthOS uses as part of its own billing and tenant-management workflows.

## Merchant-Level Payments with Stripe Connect

MarketGrowthOS also uses **Stripe Connect** at the merchant level.

This supports businesses operating within GrowthOS that offer subscription-based services to their own customers.

The architecture therefore separates:

**GrowthOS Platform Billing**

from:

**Merchant Customer Billing**

GrowthOS manages the product workflow and business context, while Stripe/Stripe Connect handles the underlying payment infrastructure.

At the merchant level, Stripe Connect allows the platform to support payment relationships associated with individual businesses without treating all merchant payments as a single platform-level billing relationship.

This distinction is important because a merchant's subscription business is part of that merchant's own commercial workflow, rather than simply being a subscription to MarketGrowthOS itself.
---

# Native Consultation Capability

Appointment and consultation booking were treated as native GrowthOS capabilities.

Mautic provides marketing forms and campaign functionality, but the product required a dedicated consultation workflow capable of supporting:

- Consultation types
- Scheduling
- Time zones
- Intake information
- Qualification questions
- Consent
- Virtual or in-person meetings
- Structured submission data

This resulted in a lightweight custom consultation booking system rather than forcing consultation workflows into the marketing automation layer.

The system was also designed to support merchants and solo operators who offer consultations as a service.

---

# Architectural Principles

Several principles guided the product architecture.

### 1. Clear System Ownership

Each major type of business state should have a clear system of authority.

### 2. Tenant Isolation

Merchant data must remain isolated from other merchants.

### 3. Explicit Workflow State

Important business processes should be represented through explicit states and valid transitions rather than implicit assumptions.

### 4. Integration Rather Than Duplication

Where an external system already provides a capability, MarketGrowthOS should integrate with it rather than automatically rebuilding it.

### 5. Native Business Capabilities

Where a workflow is central to the product's own business model, the capability should be owned by GrowthOS rather than delegated to a system whose primary purpose is different.

### 6. Product Boundaries Before Screens

The architecture and ownership model were defined before treating individual interface features as isolated requirements.

---

# Product Architecture Outcome

The result is an architecture in which:

**MarketGrowthOS**
→ owns business and operational state

**Mautic**
→ executes marketing automation

**Stripe / Stripe Connect**
→ handles platform billing and merchant-level payment infrastructure

This separation gives each system a defined responsibility while allowing the overall product workflow to operate as a connected system.
