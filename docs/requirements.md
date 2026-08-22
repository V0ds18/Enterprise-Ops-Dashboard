# Enterprise Operations Dashboard — Requirements

> **Status:** Initial Draft
> **Project Type:** Portfolio Project
> **Document:** Requirements
> **Last Updated:** 2026-08-22

---

## 1. Project Overview

The **Enterprise Operations Dashboard** is a portfolio project designed to demonstrate the development of a business-oriented enterprise application.

The application will provide a centralized operational view of equipment used in an industrial or laboratory environment, allowing users to monitor, manage, and track equipment information, maintenance, calibration, and operational status.

The project is intentionally designed to resemble a **real enterprise system**, rather than a simple CRUD application.

The system will demonstrate practices and technologies commonly found in enterprise software development, including:

* Frontend application development with Angular
* Backend API development with ASP.NET Core / C#
* Relational data management with SQL Server
* Authentication and authorization
* Role-based access control
* Operational dashboards
* Filtering and searching
* Data visualization
* Data export
* Audit history
* Bulk operations
* Docker
* Azure deployment

---

## 2. Problem Statement

Organizations operating industrial or laboratory environments may have hundreds of pieces of equipment distributed across different locations.

Without a centralized system, it can become difficult to determine:

* Which equipment exists
* Where each equipment is located
* Who is responsible for each equipment
* Whether an equipment is currently operational
* Which equipment is inactive or experiencing problems
* When an equipment was last maintained
* When an equipment was last calibrated
* Which equipment requires upcoming maintenance
* Which equipment has overdue maintenance or calibration
* What changes have been made to equipment information and by whom

The system aims to centralize this information and provide an operational view that allows users to efficiently monitor and manage the equipment inventory.

---

## 3. Project Goals

The primary goals of the project are:

1. Provide a centralized source of information about operational equipment.
2. Allow users to efficiently search, filter, and manage equipment.
3. Provide an operational dashboard with relevant information and metrics.
4. Track maintenance and calibration activities.
5. Provide historical information about relevant equipment changes.
6. Support controlled bulk updates of multiple equipment records.
7. Demonstrate authentication and authorization in an enterprise application.
8. Demonstrate data integrity and security considerations when performing bulk operations.
9. Demonstrate an architecture suitable for a real-world enterprise application.
10. Serve as a portfolio project demonstrating enterprise software engineering practices.

---

## 4. Target Users

The system will be designed for internal users responsible for monitoring and managing equipment.

The exact user profiles and permission levels have **not yet been defined**.

> **Open Question:** Which user roles will exist in the system?

> **Open Question:** What actions will each role be allowed to perform?

---

## 5. Functional Requirements

### 5.1 Dashboard

The system shall provide an operational dashboard containing information such as:

* Total number of equipment
* Number of active equipment
* Number of inactive equipment
* Upcoming maintenance
* Overdue calibration
* Equipment distribution by location
* Equipment distribution by type
* Equipment distribution by status

The exact dashboard layout and visualization types will be defined during the design phase.

> **Open Question:** Which metrics should be considered the most important operational indicators?

> **Open Question:** Should dashboard data respect the permissions of the logged-in user?

---

### 5.2 Equipment Management

Authorized users shall be able to:

* Create an equipment record
* Edit an equipment record
* View equipment details
* Change equipment status
* Associate equipment with a location
* Associate equipment with a responsible person

The exact fields belonging to an equipment record have not yet been defined.

> **Open Question:** What information is required for an equipment record?

> **Open Question:** Can an equipment have more than one responsible person?

> **Open Question:** Can an equipment belong to multiple locations?

---

### 5.3 Maintenance

The system shall allow authorized users to:

* Register a maintenance activity
* View maintenance history
* Define the next maintenance date
* Identify equipment with overdue maintenance
* Identify equipment with upcoming maintenance

The exact maintenance types and business rules have not yet been defined.

> **Open Question:** What types of maintenance will be supported?

> **Open Question:** Can a maintenance record be edited or deleted after creation?

---

### 5.4 Calibration

The system shall allow authorized users to:

* Register a calibration activity
* View calibration history
* Define the next calibration date
* Identify equipment with overdue calibration
* Identify equipment with upcoming calibration

The exact calibration business rules have not yet been defined.

> **Open Question:** Which equipment types require calibration?

> **Open Question:** Should calibration have a mandatory frequency?

---

### 5.5 Search and Filtering

The system shall provide search and filtering capabilities for equipment.

Users shall be able to filter equipment based on information such as:

* Location
* Equipment type
* Status
* Responsible person
* Date or period
* Maintenance status
* Calibration status

The exact filtering behavior and combinations have not yet been defined.

> **Open Question:** Should filters be combinable?

> **Open Question:** Should filter state be preserved when navigating between pages?

---

### 5.6 Data Export

The system shall provide a mechanism for exporting equipment data.

The exact export format and permission requirements have not yet been defined.

> **Open Question:** Which export formats should be supported?

> **Open Question:** Should exported data respect the currently applied filters?

> **Open Question:** Which user roles can export data?

---

### 5.7 Audit History

The system shall maintain an audit history of relevant changes made to the system.

Audit information should include, at minimum:

* Who performed the action
* What was changed
* When the change occurred

The exact events that require auditing have not yet been defined.

> **Open Question:** Which operations must generate audit records?

> **Open Question:** Should audit records be immutable?

> **Open Question:** Should users be able to view the audit history directly through the application?

---

### 5.8 Bulk Operations

The system shall support bulk updates of equipment.

A user shall be able to:

1. Apply filters to the equipment list.
2. Select specific equipment records.
3. Perform an operation on the selected records.

For example:

> Filter 300 equipment records, select 15 specific equipment, and change their location to `Laboratory B`.

The backend shall **never assume that the entire filtered result represents the intended target of a bulk operation**.

The frontend shall explicitly send the IDs of the equipment selected by the user.

The backend shall validate the received IDs and apply the operation only to the explicitly selected records.

This requirement is intended to demonstrate both **data integrity and secure handling of bulk operations**.

---

## 6. Authentication and Authorization

The system shall require authentication for access to protected functionality.

Authorization shall be used to control which actions a user is permitted to perform.

The project will include different levels of permissions.

The exact authentication mechanism, roles, and permission model have not yet been defined.

> **Open Question:** Which authentication mechanism will be used?

> **Open Question:** Which roles will exist?

> **Open Question:** Which permissions will each role have?

> **Open Question:** Will authorization be based exclusively on roles, or will individual permissions also be supported?

---

## 7. Business Rules

The following business rules have been established so far:

### BR-001 — Explicit Selection for Bulk Updates

Bulk operations must only affect equipment explicitly selected by the user.

A filter result alone must never be interpreted by the backend as the target of a bulk update.

### BR-002 — Authorization for Sensitive Operations

Operations that modify equipment information or perform bulk updates must be restricted according to the user's permissions.

### BR-003 — Auditability of Changes

Relevant changes to equipment information must be traceable to the user who performed the action and the time at which it occurred.

Additional business rules will be documented as they are defined.

---

## 8. Non-Functional Requirements

### 8.1 Security

The application should:

* Require authentication for protected resources.
* Enforce authorization on the backend.
* Validate user permissions before performing protected operations.
* Validate data received from clients.
* Prevent unauthorized bulk modifications.
* Maintain an audit trail for relevant changes.

Security requirements will be expanded as the architecture and implementation are defined.

---

### 8.2 Data Integrity

The system should maintain consistent and reliable equipment information.

Particular attention should be given to:

* Bulk operations
* Equipment status changes
* Maintenance records
* Calibration records
* Relationships between equipment and other entities
* Concurrent modifications

Detailed integrity constraints will be defined during database modeling.

---

### 8.3 Maintainability

The application should be structured to support:

* Clear separation of responsibilities
* Independent frontend and backend development
* Testability
* Future feature expansion
* Clear documentation
* Consistent coding standards

---

### 8.4 Deployment

The application is intended to demonstrate deployment using:

* Docker
* Azure

The exact Azure services and deployment architecture have not yet been defined.

> **Open Question:** Which Azure services will be used?

> **Open Question:** Will the frontend and backend be deployed independently?

> **Open Question:** Where will the SQL Server database be hosted?

---

## 9. Technology Constraints

The initial technology stack is:

| Layer            | Technology        |
| ---------------- | ----------------- |
| Frontend         | Angular           |
| Backend          | ASP.NET Core / C# |
| Database         | SQL Server        |
| Cloud            | Azure             |
| Containerization | Docker            |

Additional technologies may be introduced if justified by project requirements.

---

## 10. Scope

### In Scope

The initial scope includes:

* Equipment management
* Equipment search and filtering
* Operational dashboard
* Maintenance tracking
* Calibration tracking
* Equipment status management
* Location and responsibility assignment
* Data export
* Audit history
* Authentication
* Authorization
* Bulk equipment updates
* Dockerization
* Azure deployment

### Out of Scope

No additional functionality has been explicitly defined as out of scope yet.

This section will be updated as the project scope becomes clearer.

---

## 11. Documentation Strategy

The Git repository will be the **single source of truth** for project documentation whenever practical.

Documentation should be stored alongside the source code rather than maintained separately.

Current documentation structure:

```text
docs/
└── requirements.md
```

Additional documentation files will be created only when they provide a clear purpose.

For example:

```text
docs/
├── requirements.md
├── architecture.md
├── database.md
├── api.md
└── decisions/
```

The project will avoid duplicating the same information across multiple documents.

The `README.md` will serve as the **entry point to the project**, providing a concise overview, setup instructions, technology stack, and links to detailed documentation.

Detailed requirements and design decisions should remain in the appropriate documents under `docs/`.

---

## 12. Open Questions

The following decisions are intentionally left unresolved.

### Domain

* [ ] What fields should an equipment record contain?
* [ ] What equipment types should exist?
* [ ] What equipment statuses should exist?
* [ ] Can equipment have multiple responsible people?
* [ ] Can equipment have multiple locations?
* [ ] Can equipment move between locations?
* [ ] What happens when equipment is retired or disposed of?

### Maintenance

* [ ] What maintenance types should exist?
* [ ] How is the next maintenance date determined?
* [ ] Can maintenance records be edited?
* [ ] Can maintenance records be deleted?

### Calibration

* [ ] Which equipment requires calibration?
* [ ] How is the next calibration date determined?
* [ ] Can calibration records be edited?
* [ ] Can calibration records be deleted?

### Users and Permissions

* [ ] Which user roles will exist?
* [ ] What permissions will each role have?
* [ ] Who can perform bulk updates?
* [ ] Who can export data?
* [ ] Who can view audit history?

### Dashboard

* [ ] Which metrics are most important?
* [ ] Which charts should be included?
* [ ] Should dashboard data be affected by user permissions?
* [ ] Should dashboard filters be global or independent per visualization?

### Export

* [ ] Which formats should be supported?
* [ ] Should exports respect active filters?
* [ ] Should exports be audited?

### Audit

* [ ] Which actions must be audited?
* [ ] How long should audit records be retained?
* [ ] Can audit records ever be modified or deleted?
* [ ] Who can view audit records?

### Architecture and Infrastructure

* [ ] Which authentication solution will be used?
* [ ] Which Azure services will be used?
* [ ] How will the database be hosted?
* [ ] How will secrets and configuration be managed?
* [ ] How will the application be deployed?
* [ ] Will CI/CD be included in the project?

---

## 13. Requirements Status

This document represents the **initial requirements baseline**.

Requirements should be updated as the project evolves.

When a significant requirement changes, the change should be documented rather than silently replacing the previous decision.

The requirements document should answer:

> **What does the system need to do?**

Architecture documentation should answer:

> **How will the system be built?**

Implementation code should answer:

> **How was that design actually implemented?**

These concerns should remain separated to keep the project understandable and maintainable.
