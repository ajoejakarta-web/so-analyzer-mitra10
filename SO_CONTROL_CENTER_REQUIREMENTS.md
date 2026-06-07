# SO_CONTROL_CENTER_REQUIREMENTS.md

## Project Overview

Project Name:
SO Control Center

Purpose:
Help Store Managers prepare Stock Opname by monitoring location health, identifying risky storage locations, and generating sampling recommendations before physical stock counting.

Primary Users:

* Store Manager
* Inventory Team
* DSM

Store:
MITRA10 SOLO BARU (80002)

---

# Main Workflow

User uploads:

1. ReportUpdateLocationStatus.csv
2. ReportStockWarehouseByLocation.csv

System automatically:

1. Imports data
2. Classifies locations
3. Calculates health indicators
4. Calculates risk score
5. Generates sampling recommendations
6. Displays dashboard

# IMPORTANT MVP CONSTRAINTS

This application is an internal operational tool.

Requirements:

* No Login
* No Authentication
* No User Registration
* No User Roles
* No User Management

The application is used by a single store and accessed directly by store personnel.

Focus on:

* CSV Upload
* Data Processing
* Dashboard
* Risk Analysis
* Sampling Recommendation

Do not generate authentication features.


New upload replaces previous dataset.

---

# CSV Sources

## File 1

ReportUpdateLocationStatus.csv

Contains:

* ZoneName
* StorageLocationId
* StorageLocationName
* StorageLocationActiveStatus
* StorageLocationTypeName
* CountOfItem
* SumOfStockOnHandQty
* LastModifiedDate
* AuditUserName

Ignore capacity columns.

---

## File 2

ReportStockWarehouseByLocation.csv

Contains:

* StorageLocationId
* ItemNo
* ItemDescription
* ItemCategoryDescription
* StockOnHandQty

Aggregate by:

StorageLocationId + ItemNo

Sum StockOnHandQty.

---

# Location Classification

Warehouse

StorageLocationId starts with:

W

Example:

W010010101

---

Topper

StorageLocationId starts with:

C

Example:

C010010101

---

Display

StorageLocationId starts with:

D

Example:

D010010101

---

Special Storage

StorageLocationId starts with:

X

Example:

X010010101

---

Transit

StorageLocationId starts with:

RIMPILK
RIMPILG
TRANSD

Example:

RIMPILK01
TRANSD1

---

Other

All remaining location types.

---

# Health Rules

## Active Empty

Condition:

* Active Status = Active
* Storage Location Type = RACKING
* Total Quantity = 0

Result:

Flag as Active Empty.

---

## Multi Location

Condition:

Same ItemNo exists in more than one StorageLocationId.

Result:

Flag as Multi Location.

---

## Flooring Compliance

Applicable when Zone Name contains:

* Flooring
* Wall
* Stacking

Rules:

OK

SKU Count <= 5

Warning

SKU Count between 6 and 10

Critical

SKU Count > 10

---

# Risk Engine

## Base Risk

Warehouse

+30

Topper

+20

Display

+10

---

## Flooring Risk

Warning

+30

Critical

+50

---

## Warehouse SKU Risk

Warning

+20

Critical

+40

---

## Topper SKU Risk

Warning

+20

Critical

+40

---

## Over Quantity Risk

Warning

Quantity > 100

+20

Critical

Quantity > 500

+30

---

## Multi Location Risk

+50

---

## Active Empty Risk

+20

---

# Risk Tier

Critical

Risk Score > 150

High

Risk Score 100 - 150

Medium

Risk Score 50 - 99

Low

Risk Score < 50

---

# Sampling Engine

Default Sampling:

30%

Process:

1. Sort locations by Risk Score descending
2. Prioritize Critical locations
3. Prioritize High locations
4. Prioritize Medium locations
5. Select top N percent based on configuration

Output:

Sampling Recommendation List.

---

# Configuration

Editable parameters:

FlooringMaxSKU = 5

FlooringWarningSKU = 10

WarehouseHighSKU = 20

WarehouseMaxSKU = 30

TopperHighSKU = 10

TopperMaxSKU = 15

OverQtyWarning = 100

OverQtyCritical = 500

SamplingPercent = 30

---

# Dashboard

Show KPI cards:

* Total Locations
* Warehouse Locations
* Topper Locations
* Display Locations
* Active Empty Locations
* Multi Location Items
* Flooring Compliance Issues
* Critical Risk Locations
* High Risk Locations

Show charts:

* Location Distribution
* Risk Distribution

Show tables:

* Top Risk Locations
* Active Empty Locations
* Multi Location Items
* Sampling Recommendations

---

# Pages

1. Dashboard

2. Upload Data

3. Location Health

4. Multi Location

5. Flooring Compliance

6. Sampling Result

7. Configuration

---

# Technical Requirements

* Responsive design
* Desktop and mobile friendly
* Searchable tables
* Sortable tables
* Export to Excel
* Loading indicators
* Success notifications
* Error notifications

---

# MVP Scope

Version 1:

* Retail inventory only
* Mixed Ownership module as placeholder
* Manual CSV upload
* Single store operation

Future versions may support:

* Multi-store
* Automated import
* Ownership classification
* Advanced analytics
