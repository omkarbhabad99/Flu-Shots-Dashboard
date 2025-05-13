🩺 **Flu Shots Dashboard — SQL + Tableau Healthcare Analytics Project**

This project builds a fully interactive Tableau dashboard that visualizes flu-shot compliance across patient demographics using SQL for data extraction and transformation. The goal is to provide healthcare teams with actionable insights on vaccination coverage by age, race, and location.

---

## 📊 Dashboard Features

1. **Overall & Stratified Compliance**

   * Total % of patients receiving flu shots in 2022
   * Breakdown by:

     * **Age groups**
     * **Race**
     * **County** (on an interactive map)

2. **Time Series Analytics**

   * Running total of flu shots administered, month by month (2022)
   * Total number of flu shots given in 2022

3. **Patient Outreach List**

   * Table of every patient with a binary flag (`1` = shot received, `0` = not received)
   * Identifies those who need follow-up

4. **Active-Patient Filter**

   * Only includes patients alive and with an encounter in the specified window
   * Excludes those < 6 months old at end of 2022

---

## 🛠️ Technologies Used

* **PostgreSQL** – data cleaning, CTEs, and aggregation
* **PGAdmin** – SQL execution & CSV export
* **Tableau Public/Desktop** – interactive dashboards & visualizations
* **Canva** – custom icon design

---

## 🧮 SQL Highlights

* **CTEs** for:

  * `active_patients`: filters on encounter dates, death-date nullity, and age ≥ 6 months
  * `flu_shot_2012`: captures each patient’s first flu-shot date in 2022
* **JOIN** strategy ensures 1:1 mapping—avoids row duplication
* **CASE** expression to build a binary `flu_shot_2022` flag
* **Extract/Age** functions to compute patient age at a reference date

---

## 📂 Project Structure

```
├── input_data/                 # Raw CSVs (exported from SQL or sourced externally)
├── output_data.csv             # Aggregated results from the main query
├── flu_shots_query.txt         # Main SQL aggregation query (with CTEs)
├── Tableau output/             # Exports/screenshots of the final dashboard
│   └── Dashboard 1.png         # High-resolution dashboard image
└── README.md                   # Project overview and usage instructions
```

---

## 🧠 Key Learnings

* Designing robust SQL pipelines for healthcare data
* Avoiding one-to-many pitfalls with subqueries and CTEs
* Crafting dual-axis bar & area charts in Tableau
* Building dynamic dashboards with parameterized filters
* Translating binary flags into percentage metrics via averages

---

## 📦 Getting Started

1. **Run the SQL**

   * Execute `flu_shots_query.txt` in PostgreSQL/PGAdmin
   * Export the result to `output_data.csv`

2. **Load into Tableau**

   * **Tableau Public**: connect to `output_data.csv` as a text source
   * **Tableau Desktop**: use “Custom SQL” to plug in the query directly

3. **Open/Import**

   * Open `Dashboard 1.png` under **Tableau output** for reference
   * Recreate or tweak the visualizations in your own Tableau workbook

> For a line-by-line walkthrough, see the original [YouTube tutorial](https://www.youtube.com/watch?v=ef4CAu-OwvM).

---

