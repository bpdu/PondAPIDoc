# Changelog

## [Release] API Documentation Structure Enhancement

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

*Added* - 3 days ago by Pond Mobile

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

### Package Management Enhancements
- Added `status` enum to Package schema:
  - `NOT_ACTIVE`
  - `ACTIVE`
  - `TERMINATED`
- Added `activation_type` enum to Package Template:
  - `AUTO`
  - `MANUAL`
- Enhanced time allowance unit specification with enum:
  - `CALENDAR_MONTH`
  - `SECOND`

### eSIM RSP (EUICC) Improvements
- Expanded `state` enum in EUICC_profile with 12 values:
  - `AVAILABLE`, `ALLOCATED`, `LINKED`, `CONFIRMED`, `RELEASED`, `DOWNLOADED`, `INSTALLED`, `ENABLED`, `DISABLED`, `ERROR`, `UNAVAILABLE`, `DELETED`
- Added `profile_reuse_policy` with `reuse_type` enum:
  - `NEVER`, `SAME_EID_MID`, `SAME_MID`, `NEW_EID_MID`

### A2P SMS Binary Support
- Added `POST /a2p-sms/sms-requests/binary` endpoint for binary SMS messages
- Binary messages use HEX string format instead of integer arrays
- Includes dedicated operationId: `sendBinarySMS`

### Wallet Management
- Enhanced Wallet schema with `type` enum:
  - `INVENTORY`, `GROUP`, `SIM`
- Added required fields validation for wallet properties
- For supported accounts: automatic wallet generation on Inventory/Group/SIM creation

### Route Policies
- Fixed query parameter type for `inventory` (integer → string)
- Updated response descriptions for clarity

### Traffic Policies
- Retrieve endpoint: Added account manager consultation note
- List endpoint: Updated response field descriptions

### Network Access Improvements
- Fixed response descriptions in Whitelist endpoints
- Updated SIMs assignment endpoint for proper whitelist management
- Changed SIM assignment payload from array of objects to array of strings (ICCID list)

### Data Sessions
- Retrieve open data sessions: Now returns `open_data_sessions` array (was `data_sessions`)
- Added `charge_towards` enum: `PACKAGE` | `BALANCE`

### Inventory & SIM Registries
- Added `status` enum to Inventory schema
- Added `wallet_mode` clarification in Modify SIM PCR Profile endpoint

### Session Management
- Introduced Open Data Sessions endpoint with add-on service notification

For detailed information about Universal eSIM capabilities, please contact your account manager.
