````markdown
<!--
  🩺 Flu Shots Dashboard — SQL + Tableau Healthcare Analytics
-->

<p align="center">
  <img src="Tableau output/Dashboard 1.png" alt="Flu Shots Dashboard Preview" width="600"/>
</p>

# 🩺 Flu Shots Dashboard

An end-to-end Healthcare Analytics project that:

- 🔍 **Analyzes 2012 flu-shot compliance** by age, race, and county  
- 📈 Builds a **running-total** chart of vaccinations over the year  
- 👥 Produces a **patient-level list** for follow-up outreach  
- 🗺️ Renders an **interactive county map** of coverage  
- 🎯 Offers **dynamic filters** for deep dives  

---

## 🚀 Features & Workflow

1. **Data Extraction & Cleaning**  
   - Identify **active patients** (alive, ≥6 mo old, had ≥1 encounter in 2012)  
   - Pull **earliest flu-shot date** per patient  
   - Flag compliance with a binary column (`1 = shot received`, `0 = no shot`)

2. **SQL Query Logic**  
   ```sql
   -- Flu-Shot Compliance for 2012
   WITH active_patients AS (
     SELECT DISTINCT patient
     FROM encounters AS e
     JOIN patients AS pat ON e.patient = pat.id
     WHERE start BETWEEN '2012-01-01 00:00'  AND '2012-12-31 11:59'
       AND pat.deathdate IS NULL
       AND EXTRACT(MONTH FROM AGE('2022-12-31', pat.birthdate)) >= 6
   ),
   flu_shot_2012 AS (
     SELECT patient,
            MIN(date) AS first_time_shot
     FROM immunizations
     WHERE code = '140'
       AND date BETWEEN '2012-01-01 00:00' AND '2012-12-31 11:59'
     GROUP BY patient
   )
   SELECT
     pat.birthdate,
     pat.race,
     pat.county,
     pat.id,
     pat.first,
     pat.last,
     flu.first_time_shot,
     CASE WHEN flu.patient IS NOT NULL THEN 1 ELSE 0 END AS flu_shot_2022
   FROM patients AS pat
   LEFT JOIN flu_shot_2012 AS flu
     ON pat.id = flu.patient
   WHERE pat.id IN (SELECT patient FROM active_patients);
````

3. **Dashboard Construction (Tableau)**

   * **Bar charts** for age & race compliance
   * **Choropleth map** of county-level percentages
   * **Dual-axis area chart** for cumulative shots
   * **Patient list** with color-coded compliance
   * **KPI badges** for overall compliance & total shots

4. **Design Assets**

   * Icons created in **Canva**
   * Consistent color palette (hex codes in Tableau format)

---

## 🗂️ Repository Structure

```
📁 input_data/  
   └── (raw CSVs for patients, encounters, immunizations)

📄 output_data.csv           # Result of the SQL query  
📄 flu_shots_query.txt       # SQL query (as above)  
📁 Tableau output/  
   └── 📄 Dashboard 1.png     # Final dashboard screenshot  

📄 README.md                 # This document  
```

---

## 🛠️ Tech Stack

| Icon | Tool           | Purpose                          |
| :--: | -------------- | -------------------------------- |
|  🐘  | PostgreSQL     | Data storage & querying          |
|  🖥️ | PGAdmin        | SQL IDE & CSV export             |
|  📊  | Tableau Public | Dashboard design & interactivity |
|  🎨  | Canva          | Icon design & branding           |

---

## 📥 Getting Started

1. **Run the SQL** in PGAdmin (or any SQL IDE) and export as `output_data.csv`.
2. **Open Tableau Public** → *Connect* → *Text File* → Select `output_data.csv`.
3. Recreate the **calculated fields** and **views** as outlined above.
4. **Publish** to Tableau Public or save locally.

---


