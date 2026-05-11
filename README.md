# HOA-Vehicle-Parking-Monitor
A Google AppSheet-based vehicle registry application for HOA management, enabling license plate lookup, admin-controlled vehicle records, and logging of unregistered vehicles using a Google Sheets backend.

## 📌 Overview
A "no-code application built with Google AppSheet", backed by Google Sheets, designed to:

- Search and verify vehicle registration
- Display vehicle details (read-only for general users)
- Log unregistered vehicles
- Allow administrators to manage vehicle records

---

# 🗂 Data Architecture


## Data Storage
The application is backed by Google Sheets, which serves as the primary data source for all records.

- The spreadsheet is stored in Google Drive
- AppSheet connects directly to the Google Sheets file
- All data operations (read, add, update) are performed through AppSheet
- Changes are synchronized in real time between the app and the spreadsheet

This architecture enables a no-code implementation while providing flexible and easily maintainable data storage.

## 1. Registered Table (Master Data)

"Purpose:"  
Stores all officially registered vehicles.

"Columns:"
- _RowNumber
- LicencePlate (Primary Key)
- Vehicle Model (required)
- Color
- Unit number
- Sticker Number
- Active Status (Yes / No)
- Notes

"Behavior:"
- Main lookup table
- Editable only by user
- Filtered to show only active vehicles

---

## 2. Unregistered Log Table
"Purpose:"  
Tracks vehicles not found in the registry.

"Columns:"
- _RowNumber
- LicencePlate
- Vehicle Model
- Color
- Notes
- DateTime  → default: `NOW()`
- Created by (email)
- _ComputedKey -> CONCATENATE([LicencePlate],": ",[DateTime])

"Behavior:"
- Add-only (audit log)
- No updates or deletes allowed

---

# UX
## Primary View 
### Report Vehicle
Data -> Unregistered Log Table
View Type -> Form 
layoute -> 
- Unit number
- Licence plate
- vehicle model
- Color

### Vehicle lookup
Data -> Registered Table
View Type -> Card

## Menu View 
### Manage registered vehicles
Data -> Registered Table
View Type -> table 

### Unregistered log
Data -> Unregistered Log Table

# User Flow

1. User searches licence plate in Vehicle Lookup View 
2. If found → display vehicle details
3. If not found → user can either add Vehicle in the resiter list from Vehicle View, or add vehicle to Unregistered log vis Report Vehicle View
5. User can display Registered Table details and edit values
6. User can review Unregistered log and edit details

View Type -> table 

