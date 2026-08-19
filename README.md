# Calibration Cost Dashboard Study

Automated external calibration expenditure tracking and interactive executive analytics for Autoliv Hirotako.

**Public Live Dashboard:** [https://khairul6146.github.io/ExternalCalibrationCost/](https://khairul6146.github.io/ExternalCalibrationCost/)

---

## 🚀 Key Features

- **Smart Multi-Year Calibration Scheduling**: Dynamically synthesizes **`Last Cal Date` (Actual Completed)** and **`Next Cal Date` (Scheduled Due Date)** to provide an unbroken 12-month annual budget trajectory.
- **Continuous 12-Month Trajectory**: Visualizes annual cash flows without missing calendar months, distinguishing between completed calibrations and upcoming due work orders.
- **100% Unbroken Interactive Donut Chart**: Seamless circle with Spend (RM) vs Unit Volume toggle, dynamic center HUD, and instant click-to-filter cross-filtering.
- **Dual Theme System**: Professional Light Theme by default with instant 1-click Dark Theme toggle and high-contrast official brand logo container.
- **Automated Live Sync Suite**: Supports 1-Click Interactive Console Watcher (`Start-Watcher.cmd`) and background Windows Task Scheduler (`Install-AutoSync.cmd`) with desktop toast notifications.
- **Dual Client Analytics**: Feeds both the responsive HTML5/JS web dashboard (`index.html`) and Power BI semantic model (`Calibration Cost.pbix`).

---

## 🛠️ CLI & Automation Quick Reference

```powershell
# 1. Background Auto-Sync Setup Menu (Install/Uninstall Scheduled Task)
.\Install-AutoSync.cmd

# 2. 1-Click Interactive Console Watcher
.\Start-Watcher.cmd

# 3. Publish latest Excel changes to GitHub Pages manually
.\update-live.cmd

# 4. Rebuild data and preview dashboard locally (http://localhost:8765)
.\update-live.cmd -Preview

# 5. Run regression and data integrity assertions only
.\update-live.cmd -ValidateOnly
```

---

## 📂 Repository Layout

```
Calibration Cost Dashboard Study/
├── .agents/
│   └── AGENTS.md                                # Local agent router & skill rules
├── src/
│   └── scripts/
│       ├── xlsx_to_csv.py                       # Canonical Excel-to-CSV converter
│       └── validate_pipeline.py                 # Pipeline test suite
├── Icon/                                        # Dashboard icons & brand assets
├── Reference/                                   # Archived historical documents & templates
├── Autoliv Hirotako Logo Full Colour.png        # Official brand logo
├── Calibration Cost.pbix                        # Power BI report
├── Calibration_External_Distribution.xlsx       # Primary source workbook
├── data.csv                                     # Published canonical data feed
├── index.html                                   # Web dashboard application
├── Install-AutoSync.cmd                         # Auto-sync setup wizard
├── Start-Watcher.cmd                            # 1-Click interactive watcher
├── Watch-CalibrationMaster.ps1                  # Active FileSystemWatcher script
├── Register-CalibrationWatcherTask.ps1          # Task Scheduler installer
├── Sync-RemoteRepo.ps1                          # GitHub Pages asset sync script
├── update-live.cmd                              # Double-click launcher
├── update-live.ps1                              # PowerShell automation worker
├── README.md                                    # Project documentation
└── MANUAL.md                                    # Operational manual
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
