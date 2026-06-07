# SO Analyzer MVP

## Objective

Analyze Stock Opname preparation data from Mitra10 using two CSV files.

## Input Files

1. ReportUpdateLocationStatus.csv
2. ReportStockWarehouseByLocation.csv

## Features

### Upload

* Upload 2 CSV files
* Auto detect delimiter
* Preview rows and columns

### Dashboard KPI

* Total Location
* Warehouse
* Topper
* Display
* Active Empty
* Multi Location

### Risk Engine

Rules:

* Warehouse +30
* Topper +20
* Display +10
* Multi Location +50
* Active Empty +20
* Over Qty Warning +20
* Over Qty Critical +30

### Sampling

* Sort by Risk Score
* Take Top 30%
* Generate Recommended SO Sample

### Export Excel

Sheet 1 Dashboard Summary
Sheet 2 Sampling Result
Sheet 3 Multi Location

## Technical Stack

* Next.js
* TypeScript
* Tailwind
* Shadcn UI
* PapaParse
* SheetJS

## Deployment

* GitHub
* Vercel

## Non Scope

* Login
* User Management
* Database
* History Upload
* Role Access
* Batch Management
