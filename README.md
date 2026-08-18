# MarketGrowthOS

## Multi-Tenant SaaS CRM & Growth Operations Platform

**Status:** Testing / Moving Toward Production  
**Role:** Sole Product Owner  
**Team:** 3-person development team

---

## Overview

MarketGrowthOS is a multi-tenant SaaS platform designed to bring CRM, marketing automation, appointments, project management, billing and operational workflows into a more unified environment for small and medium-sized businesses.

The product came from a problem we were experiencing directly inside a digital marketing agency. The workflow had become spread across CRM, project management, appointment management, marketing automation and other operational tools.

The individual tools worked, but the overall process was fragmented and heavily dependent on manual coordination.

MarketGrowthOS was designed to bring the critical commercial workflow together, from lead acquisition and qualification through conversion, onboarding and operational delivery.

The difficult part was not deciding to build another business application. It was working out what that application actually needed to do and making the model coherent enough for engineering to build.

---

## What I Built

**MarketGrowthOS is a 0→1 SaaS product I took from a fragmented business problem through product definition, architecture, engineering and QA.**

### The interesting parts

| Product problem | My product decision |
|---|---|
| Fragmented CRM and operations | Unified commercial/operations platform |
| Multiple businesses sharing one platform | Three-tier tenant model and isolation rules |
| CRM progression was ambiguous | Explicit lifecycle, qualification gates and conversion policies |
| Marketing platform already existed | Defined Mautic/GrowthOS ownership boundary |
| Consultation booking didn't fit the marketing layer | Built a lean configurable consultation system |
| No dedicated QA function | Built a 1,200+ line validation process |

---

## Product in Action

### Merchant Dashboard

![MarketGrowthOS Merchant Dashboard](assets/merchant-dashboard.png)

*Unified view across CRM, sales, operations, projects, contacts, campaigns and consultations.*

### Opportunity Pipeline

![MarketGrowthOS Opportunity Pipeline](assets/opportunity-pipeline.png)

*Explicit sales stages and controlled progression through the commercial lifecycle.*

### Consultation System

![MarketGrowthOS Consultation System](assets/consultation-system.png)

*Configurable consultation workflow supporting scheduling, meeting format, free or paid consultations, intake fields and merchant-controlled availability.*

---

## The Product Challenge

The initial product vision was broad.

The scope cut across sales, marketing, appointments, CRM, project management, automation, billing and support. With HR and Payroll lined up for a future scope.

The product work therefore became as much about deciding **what should be built and what should not be built** as it was about defining features.

Some requirements were too broad, some timelines were unrealistic, and some proposed functionality duplicated capabilities that already existed in systems we intended to use.

The challenge was to turn a broad business ambition into a product that could actually be designed, specified, built and tested.

---

## My Role

I have been the sole product owner for MarketGrowthOS.

My responsibilities have included:

- Product discovery and problem decomposition
- Product architecture
- Workflow and lifecycle design
- Multi-tenant model design
- CRM lifecycle design
- Scope and V1 decisions
- Integration boundary definition
- Detailed product specifications
- Engineering collaboration and feasibility review
- Product/system impact analysis
- QA process design and execution
- Production-readiness validation

I work directly with a three-person (initially two) development team and stay involved throughout implementation rather than treating the specification as a handoff.

---

## Product Scope

The platform covers:

- Authentication and tenant management
- Teams and permissions
- Consultations and appointments
- CRM
- Project management
- Marketing automation
- Campaigns, tags and segments
- Emails, forms and pages
- Automation
- Billing and subscriptions
- Support

The important part of the product is not simply the number of modules. It is how those modules interact.

---

# Product Architecture

## Three-Tier Tenant Model

One of the foundational product decisions was the three-tier tenant architecture.

The model establishes clear boundaries between the platform, the businesses operating within it and the customers managed by those businesses.

This required decisions around:

- Organisation boundaries
- Users
- Teams
- Roles
- Access
- Customer ownership
- Data relationships
- Product-level permissions

The architecture was designed before treating individual screens as isolated features.

---

# CRM Lifecycle

The CRM was one of the areas where the underlying product logic mattered more than the interface.

The lifecycle was designed around:

**Lead → Qualification → Prospect → Opportunity → Conversion → Onboarding**

Rather than allowing records to move freely between statuses, I designed **multiple valid state transitions**.

This made the lifecycle explicit and prevented invalid or contradictory movements through the commercial process.

### Qualification Gate

Qualification was designed as a two-step gate rather than a single status change.

The purpose was to separate the qualification decision from the downstream movement of the customer through the commercial lifecycle.

### Policy-Driven Conversion

Customer conversion was also designed around explicit policy rather than treating conversion as a simple button action.

This required defining what conditions had to exist before a record could move into the next stage and what downstream consequences that movement would create.

---

# Build vs Integrate

One of the recurring product decisions was determining what MarketGrowthOS should own and what should remain with an existing system.

The product boundary was deliberately split between **marketing execution** and **business/operational state**.

### Mautic

Mautic serves as the marketing engine for functionality such as:

- Forms
- Landing pages
- Campaigns
- Nurture sequences
- Segmentation
- Tags
- Marketing behavioural signals

### MarketGrowthOS

GrowthOS owns the core business and operational state, including:

- CRM records
- Lifecycle state
- Conversion logic
- Permissions
- Workflow orchestration
- Appointment booking
- Consultation booking
- Billing state

Rather than rebuilding marketing functionality that already existed upstream, I defined the integration boundary between MarketGrowthOS and Mautic.

This became an important product-boundary decision rather than simply an integration task.

---

# Consultation Booking System

Mautic does not provide the appointment and consultation capability required by MarketGrowthOS.

Rather than forcing the workflow into a marketing-form model, we designed a **lean, configurable consultation booking system** as a native GrowthOS capability.

The objective was to allow merchants and administrators to create consultation experiences without requiring developer involvement.

The system supports:

- Configurable form fields
- Required and optional fields
- Field reordering
- Single-page or multi-step forms
- Consultation type selection
- Date and time selection
- Time-zone handling
- Virtual or in-person meetings
- Qualification and intake questions
- File uploads
- Consent capture
- Structured submission output
- Mobile-oriented, low-friction booking

The system supports different levels of consultation complexity, from simple booking and lead capture through more detailed assessment and intake flows.

Example consultation types include:

- General Consultation
- Strategy Session
- Product Demo
- Care Assessment

The system was also designed with **solopreneurs and service businesses that offer paid consultations as a service** in mind.

This means consultation booking can function not only as a lead-generation mechanism, but as a direct entry point into a commercial workflow.

---

# Scope and V1 Decisions

MarketGrowthOS contains a large amount of functionality, but not everything that could theoretically be built belongs in the first version.

I made V1 decisions based on:

- Business value
- Technical feasibility
- Existing platform capability
- Development capacity
- Dependency complexity
- Whether the functionality was actually necessary for the initial product

One example was deliberately avoiding the rebuild of functionality already available upstream.

The product became more manageable once the question changed from:

> "Can we build this?"

to:

> "Does this need to exist in this version, and does it belong in this product?"

---

# Product Specifications

Once the workflows and product model were sufficiently clear, I translated them into detailed specifications for engineering.

The specifications cover:

- User roles
- Permissions
- States
- Transitions
- Business rules
- Data requirements
- Workflow dependencies
- Integration behaviour
- Edge cases
- Validation requirements
- Expected system behaviour

I work with engineering during this process rather than waiting until the specification is complete.

The purpose is to find technical constraints and implementation implications while the product model can still be changed.

---

# QA

There is no separate QA function for MarketGrowthOS, so I built and run the product QA process myself.

I created a **1,200+ line QA checklist covering 15 modules** and a second-stage validation mirroring the **Given-When-Then (GWT)** approach.

The QA process is intended to validate more than whether individual screens work.

It checks whether the implemented product actually follows the intended product model.

That includes:

- Workflow behaviour
- State transitions
- Permissions
- Validation rules
- Dependencies
- Cross-module behaviour
- Exception handling
- Integration behaviour
- Data consistency
- Specification compliance

---

# Catching Problems Before Code

One of the useful parts of owning both specification and QA is being able to look for contradictions before they become implementation problems.

During specification review, I identified a contradiction in the webhook/integration specifications around bidirectional contact synchronization between MarketGrowthOS and Mautic.

The issue was caught before it became code, allowing the product behaviour to be clarified rather than leaving engineering to interpret conflicting requirements.

This is one reason I treat product specifications as a model of system behaviour rather than simply a list of features.

---

# Engineering Collaboration

MarketGrowthOS is being developed by a three-person team.

My working approach is to bring engineering into the product thinking early.

The general sequence is:

**Problem → Decomposition → Workflow → Engineering Input → Refinement → Specification → Build → QA → Iteration**

This means technical feasibility, dependencies and implementation constraints can influence the product before decisions become unnecessarily expensive to change.

---

# What I Learned

MarketGrowthOS changed how I approach scope.

Earlier in my product work, I was more willing to accept broad requirements and unrealistic timelines and then try to make everything happen.

The more useful product responsibility is sometimes to say that the requested solution or timeline does not work, explain why, and propose a smaller or more practical path.

That has become an important part of how I work with stakeholders and engineering.

---

# Current Status

MarketGrowthOS is currently in **testing and moving toward production**.

The strongest evidence from the project is the product work itself:

- 0→1 SaaS product definition
- Multi-tenant architecture
- CRM lifecycle design
- Workflow and state modelling
- Product boundary decisions
- Custom consultation booking capability
- Engineering specifications
- Scope control
- QA ownership
- Technical product management

---

# What This Project Demonstrates

### SaaS Product Design

Taking a broad business problem and turning it into a coherent multi-tenant product model.

### Technical Product Management

Working with engineering on architecture, dependencies, integrations and implementation constraints.

### Workflow Design

Designing states, gates, permissions, transitions and downstream consequences rather than focusing only on screens.

### Product Scope

Knowing when to build, integrate, defer or reject functionality.

### Specification

Turning product decisions into detailed, testable implementation requirements.

### QA Ownership

Validating the product against intended behaviour and identifying contradictions before they become production problems.

---

## Product Status

**Current stage:** Testing / Pre-Production

**Product ownership:** Sole Product Owner

**Development team:** 3 engineers

**QA:** Product-owned

**Primary evidence:** Architecture, product definition, specifications, implementation and QA
