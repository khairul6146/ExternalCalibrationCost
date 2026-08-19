# Calibration Cost Dashboard Study

Automated external calibration expenditure tracking and interactive executive analytics for Autoliv Hirotako.

**Public Live Dashboard:** [https://khairul6146.github.io/ExternalCalibrationCost/](https://khairul6146.github.io/ExternalCalibrationCost/)

---

## 🚀 Key Features

- **One-Click Sync**: Ingests multi-sheet records (`Calibration` + `Pressure Gauge`) from Excel and publishes to GitHub Pages in seconds.
- **High Data Accuracy**: Handles Excel serial dates (`openpyxl.utils.datetime.from_excel`), standard Malaysian/UK date strings (`DD/MM/YYYY`), ISO dates, and non-breaking space trimming.
- **Automated Health Audits**: Flags missing dates, external vendor zero-cost records, and validates schema integrity automatically before publishing.
- **Local Preview Engine**: Launch an instant local web server with `.\update-live.cmd -Preview`.
- **Dual Client Analytics**: Feeds both a responsive dark-theme Vanilla JS web dashboard (`index.html`) and Power BI semantic model (`Calibration Cost.pbix`).

---

## 🛠️ CLI Quick Reference

```powershell
# 1. Publish latest Excel changes to GitHub Pages
.\update-live.cmd

# 2. Rebuild data and preview dashboard locally (http://localhost:8765)
.\update-live.cmd -Preview

# 3. Run regression and data integrity assertions only
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
├── Icon/                                        # Dashboard icons & logos
├── Reference/                                   # Archived historical documents & templates
├── Calibration Cost.pbix                        # Power BI report
├── Calibration_External_Distribution.xlsx       # Primary source workbook
├── data.csv                                     # Published canonical data feed
├── index.html                                   # Web dashboard application
├── update-live.cmd                              # Double-click launcher
├── update-live.ps1                              # PowerShell automation worker
└── MANUAL.md                                    # Operational manual
```

---

## 📊 Data Schema (`data.csv`)

| Field | Type | Description |
|---|---|---|
| `description` | String | Equipment Description (Calibration) or Machine No (Pressure Gauge) |
| `equipment_type` | String | Uppercase standardized category (CALIPER, PRESSURE, etc.) |
| `vendor` | String | Calibrated party (Sendi Mahir, Trescal, Internal, etc.) |
| `cost` | Float | Cost in RM (MYR), 2 decimal places |
| `last_cal_date` | String | ISO Date `YYYY-MM-DD` (empty if unrecorded) |
| `area` | String | Plant area / department |
| `status` | String | Item Status / Type |
| `source` | String | Origin sheet (`Calibration` or `Pressure Gauge`) |
