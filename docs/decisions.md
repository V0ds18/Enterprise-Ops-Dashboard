# Project Decisions

## 2026-08-22 — Development Order

We decided not to move directly from requirements to database design.

The project will follow this development order:

```text
Requirements
    ↓
Domain Modeling
    ↓
Business Rules
    ↓
Database Modeling
    ↓
Architecture
    ↓
API Design
    ↓
Implementation
```

The next step will be to create `domain-model.md`, defining the domain entities, relationships, and business rules before translating these concepts into database tables.

**Reason:** The database should be a consequence of the domain and its requirements, rather than the data model dictating how the system should work.

---

## 2026-08-22 — Equipment Identity

Equipment will have both an internal system identifier and real-world business identifiers.

The conceptual identity structure is:

```text
Equipment
├── Internal ID
├── Asset Tag
└── Serial Number
```

* The Internal ID identifies the database/application record.
* The Asset Tag identifies the equipment within the organization.
* The Serial Number identifies the physical equipment according to the manufacturer.
* Asset Tag is considered permanent during the equipment's lifecycle.
* A change of Asset Tag is treated as a new equipment rather than changing the identity of an existing equipment.
* Serial Number is not treated as the primary business identity of the equipment and may change when necessary.

**Reason:** Separating technical identity from business/manufacturer identifiers provides a clearer domain model and avoids using external identifiers as database identity.

---

## 2026-08-22 — Equipment Ownership and Retirement

The application manages equipment belonging to the organization itself.

Equipment ownership transfers to external organizations are outside the scope of the system.

Equipment should not be deleted when it is no longer operational. Instead, its lifecycle status will represent that it has been retired.

The initial lifecycle statuses are:

```text
Active
Inactive
Retired
```

`Retired` is a terminal state. A retired equipment cannot return to `Active` or `Inactive`.

**Reason:** Preserving retired equipment allows maintenance, calibration, location, responsibility, and audit history to remain available without introducing unnecessary ownership-history complexity.

---

## 2026-08-22 — Responsible Groups

Equipment is assigned to exactly one responsible group at a time.

The responsible group represents the organizational unit responsible for operating and managing the equipment, including its maintenance and other operational needs.

Groups:

* Have a name.
* May have organizational hierarchy.
* May contain multiple users.
* A user may belong to multiple groups.
* Are conceptually sourced from an external identity system such as Azure/Entra ID.
* Are not managed by this application.
* Are mandatory for every equipment.

The application will simulate the external group source for the portfolio implementation.

Responsible group assignments must be historically preserved.

**Reason:** Group-based responsibility better represents an enterprise environment than assigning a single individual to each equipment and allows responsibility to remain stable when individual team members change.

---

## 2026-08-22 — Organizational Structure vs Authorization

Organizational group hierarchy and application authorization are treated as separate concerns.

Group hierarchy represents organizational structure and does not inherently determine application permissions.

Authorization rules, roles, and permissions will be defined separately.

**Reason:** Organizational membership does not necessarily imply authorization to perform sensitive operations such as bulk updates.

---

## 2026-08-22 — Location History

Equipment may change location during its lifecycle.

Location will initially be modeled as a simple organizational location such as a laboratory or warehouse. Hierarchical physical location modeling is outside the current scope.

Equipment location must be historically preserved.

The initial location assignment is recorded when the equipment is created.

The current location is derived from the active/current location-history record rather than being duplicated as a separate attribute on Equipment.

Only one location may be current for an equipment at a given time.

**Reason:** Location is operational information that may change over time, and preserving its history provides useful historical context without duplicating the current value in multiple places.

---

## 2026-08-22 — Equipment Status

Equipment status is a fixed domain enumeration:

```text
Active
Inactive
Retired
```

The organization cannot create arbitrary equipment statuses.

Status changes must be historically preserved.

The current status is derived from the current status-history record.

`Retired` is a terminal lifecycle state.

**Reason:** These statuses represent a fixed lifecycle model rather than configurable reference data. Historical status information is required to understand the equipment's lifecycle.

---

## 2026-08-22 — Equipment Type

Equipment Type is reference data rather than a fixed enumeration.

The organization may create new equipment types.

Equipment Types:

* Have a name.
* May be deactivated.
* Should not be deleted while referenced by equipment.
* Do not require historical tracking.

Each equipment has one current Equipment Type.

**Reason:** Equipment categories may evolve as the organization introduces new types, but changing the classification does not represent a temporal state change of the equipment itself.

---

## 2026-08-22 — Maintenance Scheduling

Every equipment requires maintenance.

Maintenance frequency is defined by the Equipment Type rather than individually by each equipment.

The frequency is represented as a number of days.

The next maintenance date is derived from:

```text
Maintenance Performed Date
+
Equipment Type Maintenance Frequency
```

The next maintenance cycle starts from the actual maintenance execution date, even when maintenance is performed earlier or later than originally expected.

The next maintenance date is derived rather than stored as an independent source of truth.

**Reason:** Keeping the frequency at the Equipment Type level avoids duplicating the same rule across many equipment records, while deriving the next due date prevents inconsistent duplicated data.

---

## 2026-08-22 — Domain Discovery Still In Progress

The following concepts have been identified but are not yet fully modeled:

```text
Equipment
Location
User
Group
Maintenance
Calibration
Audit
Equipment Status
Equipment Type
```

Several decisions remain intentionally open, including:

* Maintenance record structure.
* Who can perform maintenance.
* Maintenance execution responsibility.
* Calibration rules and scheduling.
* User/role/permission model.
* Audit model.
* Bulk operation transaction and failure behavior.
* Equipment attributes not yet identified.
* Final domain relationships and cardinalities.

These should be resolved during the domain-modeling phase before database schema design begins.

**Current stopping point:** Maintenance — definition of who/what performs a maintenance record.

**Next session:** Continue the Maintenance domain decision from this point rather than restarting the discovery process.
