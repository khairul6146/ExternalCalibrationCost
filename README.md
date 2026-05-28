# Calibration Cost Dashboard

Live dashboard for external calibration spending at Autoliv Hirotako.
**Public URL:** https://khairul6146.github.io/ExternalCalibrationCost/

---

## How it works

```
data/source.xlsx              you edit this one
        |
        v
.github/workflows/build-data.yml      runs on every push
        |
        v
data.csv                      auto-generated, do not edit by hand
        |
        v
index.html                    fetches data.csv on page load
```

You only ever touch `data/source.xlsx`. Everything else is automatic.

---

## To update the data

1. Open `data/source.xlsx` in Excel.
2. Edit either the **Calibration** sheet or the **Pressure Gauge** sheet.
3. Save and close.
4. Open PowerShell in this folder and run:

   ```powershell
   git add data/source.xlsx
   git commit -m "data update YYYY-MM-DD"
   git push
   ```

5. Wait ~30 seconds. Visit the dashboard URL above and click **Refresh**.

The GitHub Actions workflow does the XLSX-to-CSV conversion in the cloud, commits the result, and the GitHub Pages site picks it up on the next page load.

---

## To use it in Power BI

1. Open `Calibration Cost.pbix` in Power BI Desktop.
2. **Home -> Transform data -> New Source -> Web**
3. Paste: `https://khairul6146.github.io/ExternalCalibrationCost/data.csv`
4. Replace the existing local-Excel source with this Web source.
5. Publish to Power BI Service.
6. In the Service: **Dataset -> Settings -> Scheduled refresh** -> daily.

Both reports now share one source of truth.

---

## Repository layout

| Path | Purpose | Edit by hand? |
|---|---|---|
| `data/source.xlsx` | Source workbook with two sheets | YES |
| `data.csv` | Combined output, sorted by date | no — auto-generated |
| `index.html` | The dashboard | rarely |
| `scripts/xlsx_to_csv.py` | The converter the Action runs | rarely |
| `.github/workflows/build-data.yml` | The automation | rarely |

---

## Local preview

Need to test the dashboard before pushing? Open a terminal in this folder and run:

```powershell
python -m http.server 8765
```

Then open http://localhost:8765/index.html in your browser. The page fetches `./data.csv` from the same server.

If `python -m http.server` says "Python was not found", use the Microsoft Store version, or run `uv run python -m http.server 8765` if you have uv installed.

---

## Schema of `data.csv`

| Column | Type | Notes |
|---|---|---|
| description | text | Instrument name (Calibration sheet) or Machine No (Pressure Gauge sheet) |
| equipment_type | text | UPPER-cased category: CALIPER, PRESSURE, etc. |
| vendor | text | Cal-by party. "Internal" for in-house cals (cost = 0). |
| cost | number | RM, two decimals |
| last_cal_date | date | ISO YYYY-MM-DD; empty if not recorded |
| area | text | Plant area / department |
| status | text | Item Status (Calibration) or Item Type (Pressure Gauge) |
| source | text | "Calibration" or "Pressure Gauge" — which sheet the row came from |

---

## Troubleshooting

**Dashboard shows "Offline" in the corner.**
The fetch to `data.csv` failed. Common causes: the file is opened directly from disk (`file://` blocks fetch), or you are offline. Use the **Load CSV** button to drag-and-drop a file as a fallback.

**The Action runs but `data.csv` does not change.**
The XLSX content was identical after parsing. The "git diff" check at the end of the workflow short-circuits — this is correct behavior.

**The Action fails with "sheet 'Calibration' not in workbook".**
Excel renamed your tab. Either rename it back, or update the sheet names in `scripts/xlsx_to_csv.py`.

**Power BI cannot refresh the Web source on schedule.**
Power BI Service requires the data to be public OR the gateway to be configured. Since this CSV is on GitHub Pages (public), no gateway is needed — but the dataset's **Data source credentials** must be set to **Anonymous** access.
