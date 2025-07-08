================================================================
MIMIC-IV Data Extraction and Transformation with Google BigQuery
================================================================


[ PROJECT GOAL ]

This project focuses on executing an ETL (Extract, Transform, Load) process on the large-scale MIMIC-IV clinical database hosted on Google BigQuery. The primary objective was to build a clean, analysis-ready dataset focused on predicting weaning success for ICU patients with sepsis.


[ TOOLS & TECHNOLOGIES ]

* Language: SQL
* Cloud Platform: Google Cloud Platform (GCP)
* Database: Google BigQuery


[ DETAILED PROCESS ]

The process was structured around a main SQL query that handled all three phases of the ETL pipeline:

1. Extraction:
   - [cite_start]Identified and extracted data for sepsis-3 patients during their first ICU stay. [cite: 1, 2]
   - [cite_start]Isolated the initial invasive mechanical ventilation events for this cohort. [cite: 2]

2. Transformation:
   - [cite_start]Generated the outcome variable (`weaning_success`) based on established post-weaning failure criteria, such as reintubation within 48 hours, death within 48 hours, or the need for non-invasive ventilation for more than 48 hours. [cite: 4]
   - Pre-aggregated multiple predictor variables by calculating the "worst" value (max or min) within a 24-hour window before weaning. [cite_start]This included vitals, lab results (chemistry, CBC), arterial blood gases, and ventilator settings. [cite: 6, 7, 8, 10]
   - [cite_start]Calculated complex metrics like the Rapid Shallow Breathing Index (RSBI) and Body Mass Index (BMI). [cite: 11]
   - [cite_start]Created binary flags for vasopressor use and calculated durations for antibiotic and CRRT therapies. [cite: 12, 13]

3. Load (Final Dataset Assembly):
   - [cite_start]All pre-aggregated variables and demographic data were joined into a final table. [cite: 14]
   - [cite_start]Final exclusion criteria (e.g., patients under 18) were applied to ensure the quality of the dataset. [cite: 23]


[ FINAL DATASET SCHEMA ]

The resulting dataset is a clean, modeling-ready table with one row per patient. For a complete description of all extracted variables, please refer to the `Extracted_Variables_mimiciv.pdf` file.

Key columns include:

-   Identification Vars: stay_id, subject_id
-   Outcome Var: weaning_success (1 for success, 0 for failure)
-   Demographics: age, sex, bmi
-   Comorbidities & Severity Scores: charlson_comorbidity_index, chronic_pulmonary_disease, diabetes, sapsii, first_day_sofa
-   Therapeutic Measures & Durations: imv_duration_days, vasopressor_used, antibiotic_duration_days, crrt_duration_days
-   Aggregated Labs & Vitals: highest_heart_rate, lowest_map, highest_creatinine, lowest_hemoglobin, lowest_ph, lowest_pao2fio2ratio, etc.
-   Ventilation Parameters: highest_peep, highest_fio2, rsbi