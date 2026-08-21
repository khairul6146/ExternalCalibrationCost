# Calibration Cost Dashboard Study — Operations Manual

Comprehensive guide for managing the autonomous daily masterlist synchronization engine and the executive Cost Distribution Dashboard.

**Live Executive Dashboard:** [https://khairul6146.github.io/ExternalCalibrationCost/](https://khairul6146.github.io/ExternalCalibrationCost/)  
**SharePoint Online Workbook:** `https://autolivhirotako.sharepoint.com/sites/systest/Calibration/Calibration%20External%20Cost/Calibration_External_Distribution.xlsx`  
**Local Synced Path:** `C:\Users\mkakmal\Autoliv Hirotako Malaysia\System & Testing Department - Calibration\Calibration External Cost\Calibration_External_Distribution.xlsx`

---

## 1. Automated Daily Sync (100% Hands-Free)

### Scheduled Background Automation

1. The Windows Scheduled Task **`AutolivCalibrationDailySync`** runs automatically every **Weekday (Monday – Friday) at 9:00 AM**.
2. **Failure Auto-Retry**: If the corporate network or SharePoint connection is temporarily interrupted, Windows automatically retries up to **3 times (every 15 minutes)**.
3. **Missed-Run Recovery**: If your computer was asleep or turned off at 9:00 AM, the task executes immediately upon logon/wake.
4. **Execution Flow**:
   - `automation\Refresh-CalibrationMaster.ps1` opens `Calibration_External_Distribution.xlsx` headlessly via background Excel COM.
   - Synchronously executes `RefreshAll()` across all Power Query M mashups to pull the latest department masterlist records.
   - Saves the updated workbook.
   - Converts sheets into canonical `data.csv` (9-column schema).
   - Validates data health and integrity.
   - Pushes updates directly to GitHub Pages and Power BI.
   - Displays a Windows Desktop Toast notification confirming sync count and spend.

---

## 2. 1-Click Operations & Management Menu

Double-click **`Install-AutoSync.cmd`** in this folder:

- **`[1] Install Daily Auto-Sync`**: Installs/updates the Weekday 9:00 AM scheduled task with retry policy.
- **`[2] Check Scheduled Task Status`**: Displays current task state, last execution result, and next run time.
- **`[3] Run Masterlist Sync Now`**: Triggers an instant on-demand headless masterlist pull, CSV conversion, and GitHub push.
- **`[4] Uninstall Scheduled Task`**: Removes the background task.

---

## 3. Executive Dashboard Structure & Analytics

The redesigned frontend (`index.html`) is structured specifically for **Management Presentations & Financial Analysis**:

1. **Smart Multi-Year Scheduling**:
   - Synthesizes `Last Cal Date` (actual completed) and `Next Cal Date` (scheduled due dates) so that all 12 calendar months (Jan–Dec) are populated.
   - Allows switching between **🎯 Smart Unified Calendar**, **🗓️ Completed Only**, and **⏳ Scheduled Only** views.
2. **Interactive Visual Analytics**:
   - **100% Unbroken Donut Chart**: Complete circular ring with Spend (RM) vs Unit Volume toggle, dynamic center HUD, and click-to-filter capability.
   - **Continuous Monthly Combo Graph**: 12 unbroken calendar months with actual vs scheduled unit split tooltips.
   - **Dual Theme Support**: Light Theme by default with instant Dark Theme toggle and high-contrast brand logo container.
3. **Analytical Tabs**:
   - **📊 Executive Overview**: High-level spending summary, Pareto bars, vendor concentration donut, and monthly run-rate trend.
   - **📐 Equipment Pareto**: Complete category ranked breakdown with unit volume and average cost per instrument.
   - **🏢 Vendor Allocation**: Supplier concentration, core specialty mapping, and dependency risk segmentation.
   - **🏭 Department Cost Centers**: Plant area calibration cost absorption (Test Lab, Stamping, QA, Toolroom, Assembly).
   - **🏷️ Spend Tiering**: Tier 1 High-Value (>RM 1k), Tier 2 Medium (RM 200–1k), and Tier 3 Routine (<RM 200) breakdown.
   - **📈 Monthly Trajectory**: Time-series cash outflow and cumulative run-rate.
   - **💡 Strategic Recommendations**: Concrete management recommendations (Indpro Torque MSA, DTS Data Acquisition SLA, Multitech Sole-Supplier batch discount, Digital Caliper QA verification).
   - **📋 Master Audit Table**: Full register with `Last Cal Date` and `Next Due Date` columns and cycle status tags.
4. **1-Click PDF / Print Export**:
   - Click **🖨️ Export PDF** on the header to generate a clean, printout formatted for board meetings.

---

## 4. Power BI Integration

1. Open `Calibration Cost.pbix` in Power BI Desktop.
2. Web Source URL: `https://khairul6146.github.io/ExternalCalibrationCost/data.csv`
3. Authentication: **Anonymous**.
4. Set daily scheduled refresh in Power BI Service for automated reporting.
