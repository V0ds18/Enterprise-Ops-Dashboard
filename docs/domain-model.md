```mermaid
%% Open Markdown Preview with Ctrl+Shift+V to visualize this diagram.

flowchart TD
    User -->|membership| Group
    Group -->|responsible| Equipment

    Location -->|current location| Equipment
    Equipment --> Type
    Equipment --> Status

    Equipment -->|history| LocationHistory
    Equipment -->|history| ResponsibleGroupHistory
    Equipment -->|history| StatusHistory
    Equipment --> Maintenance
    Equipment --> Calibration
    Equipment --> Audit
```