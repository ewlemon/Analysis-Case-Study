# Analysis Case Study

A multi-dataset workforce analysis completed as part of a technical interview assessment. The project involved cleaning and merging raw data, performing statistical analysis, parsing a complex Excel structure, and presenting findings through Tableau dashboards and a Prezi presentation.

Prezi presentation: https://prezi.com/view/22UxRRlGPnmYlEYpWKvC/

---

## 📁 Project Structure

```
├── AnalysisCaseStudy.ipynb       # Python notebook — all cleaning, analysis, and exports
├── Files/
│   ├── Absenteeism_at_work.csv   # Raw absenteeism dataset (740 records)
│   ├── Happiness_Index.csv       # Raw employee engagement survey (740 records)
│   ├── Consultant Utilization... # Raw consultant hours Excel file
│   ├── clean_absenteeism.csv     # Cleaned & labeled absenteeism data (exported)
│   ├── clean_survey.csv          # Cleaned & labeled survey data (exported)
│   └── consultant_summary.xlsx   # Parsed consultant utilization summary (exported)
```

---

## 🔍 What the Project Covers

### Part 1–2 · Data Loading & Exploration
Loaded both CSV datasets and confirmed they each contained 740 rows, sharing a common ID column. Ran `head()`, `dtypes`, `isnull()`, and `describe()` to understand structure and spot issues before touching anything.

### Part 3 · Cleaning Absenteeism Data
- Fixed `Transportation expense` stored as an object due to comma formatting — converted to numeric and filled one missing value with the median
- Mapped numeric categorical codes to readable labels: day of week (2–6 → Monday–Friday), season (1–4 → Spring/Summer/Autumn/Winter), education level, absence reason codes (0–28), and binary flags for smoking and drinking
- Added a `Month Name` column mapping month numbers to names

### Part 4 · Cleaning Survey Data
- Mapped Likert scale scores (1–5) to descriptive labels across four survey dimensions: work satisfaction, relationship with manager, enjoyment of colleagues, and intent to stay
- Ran final null checks on both datasets confirming clean exports

### Part 5 · Export
Exported `clean_absenteeism.csv` and `clean_survey.csv` for use in Tableau.

### Part 6 · Correlation Analysis
Used SciPy's Pearson correlation to test two continuous numeric variables against absenteeism hours:
- **Number of children** vs. absenteeism time
- **Distance from residence to work** vs. absenteeism time

Deliberately excluded categorical and ordinal variables (day of week, education, etc.) from correlation — those require different statistical approaches.

### Part 7 · Consultant Utilization Parsing
The consultant Excel file had an unconventional 3-row-per-consultant structure (actual hours / capacity hours / monthly variance). Wrote a custom loop to step through every 3 rows, extract the consultant name, and reshape the data into a clean one-row-per-consultant summary exported to `consultant_summary.xlsx`.

### Part 8–9 · Statistical Verification
- Grouped survey data by employee ID to verify whether individuals gave varying responses across records — confirming the validity of using all 740 records rather than averaging to 36 employees
- Confirmed that 35 of 36 employees have an identical distance value repeated across all their records, proving a distance correlation on 740 rows would simply repeat the same 36 data points and is not statistically meaningful

---

## 📊 Tableau Dashboards

Two Tableau dashboards were built from the cleaned exports:
- **Absenteeism Dashboard** — visualizes absence patterns by day, season, reason, education level, and employee characteristics
- **Consultant Utilization Dashboard** — visualizes actual vs. capacity hours per consultant

---

## 🎨 Presentation

Findings were compiled into a Prezi presentation covering methodology, key insights, and recommendations.

🔗 [View the Prezi Presentation](https://prezi.com/view/22UxRRlGPnmYlEYpWKvC/)

---

## 🛠 Tools Used

| Tool | Purpose |
|------|---------|
| Python (Pandas) | Data loading, cleaning, transformation, export |
| Python (SciPy) | Pearson correlation analysis |
| Python (openpyxl) | Parsing and exporting Excel files |
| Tableau | Dashboard visualization |
| Prezi | Presentation of findings |

---

## ▶️ Running the Notebook

1. Clone the repository
2. Place the raw data files in a `Files/` subfolder
3. Update the file paths in the notebook cells to match your local directory
4. Run all cells in order — each part builds on the previous exports

> **Note:** The notebook was developed locally on Windows. File paths use `r"C:\..."` syntax and will need to be updated to your own directory before running.
