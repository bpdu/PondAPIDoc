# Changelog

## [Release] API Documentation Structure Enhancement

*Added* - April 3, 2026 by Pond Mobile

### Two-Level Subsection Navigation
- Implemented two-level navigation structure using x-tagGroups extension
- Main sections now serve as category headers (CORE, INVENTORY, ESIM RSP, etc.)
- Subsections provide logical grouping of related endpoints:
  - **CORE**: Companies, Countries
  - **INVENTORY**: Inventories, Groups, SIM Registries, SIM Transfers, MSISDN
  - **ESIM RSP**: eUICC Profiles
  - **POLICY AND CHARGING RULES (PCR)**: Package Templates, Packages, Route Policies, SIM PCR Profiles, Traffic Policies, Wallets
  - **SESSION MANAGEMENT**: Data Sessions
  - **NETWORK ACCESS**: Whitelists, Whitelist Assigned SIMs, Location Updates
  - **A2P SMS**: A2P SMS operations
  - **WEBHOOKS**: eSIM RSP, SIM Transfer, Packages, Device Statuses, A2P SMS
- Improved navigation and user experience matching industry-standard API documentation layout
- Added tag descriptions for all subsections

## [Release] Universal eSIM Support & Webhooks Integration

*Added* - March 31, 2026 by Pond Mobile

### New Webhooks (6 endpoints)
- Introduced webhook notifications system for real-time event monitoring:
  - **ESIM Status Change Event** - Notifies on eSIM profile download progress (GSMA RSP HandleDownloadProgressInfo)
  - **SIM Transfer Callback** - Notifies on SIM transfer request completion
  - **Package Data Usage Alert Event** - Alerts when package reaches 50% or 80% data usage
  - **Package Status Change Event** - Notifies on package status modifications (ACTIVATED/TERMINATED)
  - **IMEI Change Event** - Detects IMEI changes during device location updates
  - **A2P SMS (MO) Received Event** - Notifies on Mobile Originated SMS received from devices

### Universal eSIM Support
- Introduced `sim_variance` field in List SIMs endpoint with values:
  - `CLASSIC` - Classic eSIM
  - `UNIVERSAL_DATA_ONLY` - Universal Data Only eSIM
  - `UNIVERSAL_VOICE` - Universal Voice eSIM
- Introduced `type` field in Group and Whitelist endpoints for Universal eSIM classification
  - API endpoints affected: Group Retrieval, Whitelist Retrieval

### Enhanced SIM Management
- Added `sim_type` field to SIM schema: `eSIM` | `SIM`
- Added `sim_status` enum with values:
  - `WAITING_FOR_ASSIGNMENT`
  - `PRE_SERVICE`
  - `IN_SERVICE`
  - `TERMINATED`
- Added `SIM_Detail` schema for Retrieve SIM endpoint with expanded object references

### MSISDN Self-Management APIs
- Introduced MSISDN assignment management endpoints:
  - Retrieve MSISDN assigned to an ICCID
  - Assign MSISDN to SIM (with self-service capability)
  - Unassign MSISDN from SIM
- Breaking change: Renamed `assigned_id` → `assignment_id` in MSISDN Assignment schema

