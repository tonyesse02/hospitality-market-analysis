# 🏨 Hospitality Market Analysis

> Excel-based data cleaning, modelling and market analysis of 6,258 hospitality structures across 234 municipalities in the Marche region (Italy).

---

## 📌 Project Overview

This project was developed as part of a structured Excel exercise focused on real-world data quality issues. Starting from a raw open dataset of hospitality facilities provided by the Marche regional authority, the work covered the full data pipeline: cleaning, deduplication, enrichment, modelling and analysis.

The final deliverable is an integrated Excel model combining facility data with average pricing by city, featuring dynamic search functionality and pivot-based geographic reporting.

---

## 📊 Dataset at a Glance

| Metric | Value |
|---|---|
| Total structures | 6,258 |
| Municipalities covered | 234 |
| Average price range | €30 – €120 per night |
| Categories | 12 (B&B, Hotels, Agriturismo, Campsites…) |

### Category Breakdown

| Category | Count |
|---|---|
| Bed & Breakfast | 1,809 |
| Stabilimenti Balneari | 850 |
| Alloggi Agrituristici | 830 |
| Alberghi | 814 |
| Altri Alloggi Privati | 721 |
| Alloggi in Affitto | 541 |
| Turismo Rurale | 304 |
| Other | 389 |

---

## 🗂️ Repository Structure

```
hospitality-market-analysis-marche/
│
├── 📂 data/
│   ├── elencostrutture_AntonioSpagnuolo.xlsx   # Main dataset — cleaned & enriched
│   └── prezzimedi.xlsx                          # Average nightly price by city
│
├── 📂 model/
│   └── MODELLO_DATI_xlsx.xlsx                   # Final integrated data model
│
└── 📄 README.md
```

---

## 🔧 Work Performed

### 1. Data Cleaning
- Applied `TRIM` and `UPPER` to normalize text fields across all columns
- Detected and corrected swapped values between `Indirizzo internet` and `Indirizzo di posta elettronica` using:
```excel
=IF(ISNUMBER(SEARCH("@", Table1[@[Indirizzo internet]])),
   Table1[@[Indirizzo di posta elettronica]],
   Table1[@[Indirizzo internet]])
```

### 2. Unique Identifier
- Added an `Identificativo` field concatenating name and row number to handle duplicate entries:
```excel
=CONCATENATE([@Denominazione]," ";ROW()-1)
```

### 3. Dynamic Search Mask
- Built a `RICERCA` sheet with a dropdown menu referencing the `Identificativo` column
- Added `Città` field to the search output for richer results
- Included counters: total structures, structures per locality, structures per city

### 4. Pivot Table
- Created a pivot grouped by category with an optional city filter
- Allows quick comparison of facility types across municipalities

### 5. Data Model Integration (`MODELLO_DATI_xlsx.xlsx`)
- Merged the cleaned facility dataset with average pricing from `prezzimedi.xlsx`
- Final model contains 3 sheets: `Strutture Ricettive`, `prezzi`, `Pivot`
- `prezzi` sheet covers all 234 municipalities with average nightly rates

---

## 💡 Key Findings

- **B&B** is the dominant category with 1,809 facilities — nearly 29% of the total
- **Coastal municipalities** (Stabilimenti Balneari: 850) represent the second largest segment
- Average nightly prices range from **€30 (Urbino)** to **€120 (Carpegna)**, with inland mountain areas showing higher rates
- Several records had **swapped contact fields** (email in website column and vice versa) — corrected via formula logic

---

## 🛠️ Tech Stack

![Excel](https://img.shields.io/badge/Microsoft_Excel-217346?logo=microsoft-excel&logoColor=white)

- **Microsoft Excel** — data cleaning, formula logic, pivot tables, search mask
- **Functions used:** `TRIM`, `UPPER`, `IF`, `ISNUMBER`, `SEARCH`, `CONCATENATE`, `VLOOKUP`, `COUNTIF`

---

## 📄 License

This project was developed for academic purposes as part of the Epicode Data Analyst programme. Dataset sourced from open regional data of the Marche Region (Italy).
