                         ┌──────────────┐
                         │     User     │
                         └──────┬───────┘
                                │
                                │ membership
                                ▼
                         ┌──────────────┐
                         │    Group     │
                         └──────┬───────┘
                                │
                                │ responsible
                                ▼
┌──────────────┐          ┌──────────────┐
│   Location   │◄─────────│   Equipment  │
└──────┬───────┘          └──────┬───────┘
       │                         │
       │ history                ├── Status
       ▼                         ├── Type
Location History                 │
                                 ├── Responsible Group History
                                 │
                                 ├── Maintenance
                                 │
                                 └── Calibration


CURRENT STATE
    Equipment
    ├── current Location
    ├── current Responsible Group
    ├── current Status
    └── current Type

HISTORY
    ├── Location History
    ├── Responsible Group History
    ├── Status History
    ├── Maintenance History
    ├── Calibration History
    └── Audit History