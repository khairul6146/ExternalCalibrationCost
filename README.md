# Calibration Cost Dashboard Study

Automated external calibration expenditure tracking and interactive executive analytics for Autoliv Hirotako.

**Public Live Dashboard:** [https://khairul6146.github.io/ExternalCalibrationCost/](https://khairul6146.github.io/ExternalCalibrationCost/)

---

## 🚀 Key Features

- **100% Autonomous Daily Masterlist Sync**: Automatically queries the Department Masterlist via background Excel Power Query mashups every **Weekday at 9:00 AM** with failure auto-retry (3 attempts every 15 min), completely hands-free without opening Excel.
- **Smart Multi-Year Calibration Scheduling**: Dynamically synthesizes **`Last Cal Date` (Actual Completed)** and **`Next Cal Date` (Scheduled Due Date)** to provide an unbroken 12-month annual budget trajectory.
- **Continuous 12-Month Trajectory**: Visualizes annual cash flows without missing calendar months, distinguishing between completed calibrations and upcoming due work orders.
- **100% Unbroken Interactive Donut Chart**: Seamless circle with Spend (RM) vs Unit Volume toggle, dynamic center HUD, and instant click-to-filter cross-filtering.
- **Dual Theme System**: Professional Light Theme by default with instant 1-click Dark Theme toggle and high-contrast official brand logo container.
- **Dual Client Analytics**: Feeds both the responsive HTML5/JS web dashboard (`index.html`) and Power BI semantic model (`Calibration Cost.pbix`).

---

## 🛠️ CLI & Automation Quick Reference

```powershell
# 1. Daily Auto-Sync Setup Wizard (Weekdays 9:00 AM + Failure Retry)
.\Install-AutoSync.cmd

# 2. Check Daily Scheduled Task Status
pwsh .\automation\Register-DailySyncTask.ps1 -Status

# 3. Trigger On-Demand Masterlist Refresh & Push Now
pwsh .\automation\Register-DailySyncTask.ps1 -RunNow

# 4. Rebuild data and preview dashboard locally (http://localhost:8765)
.\update-live.cmd -Preview

# 5. Run regression and data integrity assertions only
.\update-live.cmd -ValidateOnly
```

---

## 📂 Streamlined Repository Architecture

```
Calibration Cost Dashboard Study/
├── 📊 CORE APPLICATIONS & DATA
│   ├── index.html                               # Executive Interactive Web Dashboard
│   ├── data.csv                                 # Canonical 9-Column Dataset Feed
│   ├── Calibration Cost.pbix                    # Executive Power BI Report Model
│   ├── Calibration_External_Distribution.xlsx   # Local Master Workbook (Power Query Synced)
│   └── Autoliv Hirotako Logo Full Colour.png   # High-Contrast Official Brand Asset
│
├── 🚀 1-CLICK LAUNCHERS (ROOT)
│   ├── Install-AutoSync.cmd                     # Daily Weekday 9AM Auto-Sync Wizard
│   └── update-live.cmd                          # 1-Click Masterlist Pull, Publish & Local Preview
│
├── 📁 automation/                               # Background Automation Engines & Workers
│   ├── Refresh-CalibrationMaster.ps1            # Headless Excel Power Query Engine & COM Handler
│   ├── Register-DailySyncTask.ps1               # Weekday 9:00 AM Scheduled Task Installer
│   ├── Sync-RemoteRepo.ps1                      # GitHub Pages Assets Synchronizer
│   └── update-live.ps1                          # Publisher & Local Preview Web Server
│
├── 📁 src/scripts/                              # Python Data Pipeline & Quality Assurance
│   ├── xlsx_to_csv.py                           # 9-Column Canonical ETL Converter
│   └── validate_pipeline.py                     # Automated Data Integrity & Schema Tests
│
├── 📁 Icon/                                     # Dashboard Vector & Raster Icons
├── 📁 logs/                                     # Automated Pipeline Execution & Sync Logs
│   └── daily_sync.log                           # Headless Daily Sync History
│
├── 📁 Reference/                                # Archived Reference Data & Historical Guides
│   ├── Calibration_External_Distribution_Legacy.csv
│   ├── Calibration_Dashboard.xlsx
│   ├── Calibration_Pressure_Combined.xlsx
│   ├── Calibration_Cost_Redesign_Guide.docx
│   └── Dashboard_Update_Guide.docx
│
└── 📖 DOCUMENTATION
    ├── README.md                                # System Overview & Developer Quick-Start
    ├── MANUAL.md                                # Executive & Operations User Manual
    └── .agents/AGENTS.md                        # Local AI Agent Routing & Architecture Specs
```

---

## 📊 Data Schema (`data.csv`)

| Field | Type | Description |
|---|---|---|
| `description` | String | Equipment Description (Calibration) or Machine No (Pressure Gauge) |
| `equipment_type` | String | Uppercase standardized category (CALIPER, PRESSURE, etc.) |
| `vendor` | String | Calibrated party (Sendi Mahir, Trescal, Multitech, DTS, Indpro, etc.) |
| `cost` | Float | Cost in RM (MYR), 2 decimal places |
| `last_cal_date` | String | ISO Date `YYYY-MM-DD` (actual completed date) |
| `next_cal_date` | String | ISO Date `YYYY-MM-DD` (scheduled due date) |
| `area` | String | Plant area / department |
| `status` | String | Item Status / Type |
| `source` | String | Origin sheet (`Calibration` or `Pressure Gauge`) |
