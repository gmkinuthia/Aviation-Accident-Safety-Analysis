
 Aviation Accidents Safety Analysis (1948–2023)

## Project Context
This project was conducted as part of a consulting-style analysis for an **airline / aircraft insurer**. The objective is to identify **aircraft makes and models** that exhibit:

- Low likelihood of **fatal or serious passenger injuries**
- Low rates of **aircraft destruction** in the event of an accident

The analysis uses U.S. aviation accident data spanning **1948–2023**, with filtering applied to reflect aircraft that are **professionally manufactured and potentially still active**.



## Data Scope and Filtering
To ensure relevance to the client’s current risk exposure:

- Only accidents from **1983 onward** were retained, assuming a maximum **40‑year operational lifespan** for aircraft makes and models.
- The dataset was reduced to variables directly related to **injury severity, aircraft damage, and operational context**.
- Aircraft makes and models with **very low sample sizes** were excluded to ensure statistical robustness.

After cleaning and filtering, the final dataset contains **~70,000 accident records** suitable for reliable comparative analysis.



## Data Cleaning and Key Assumptions

### Injury Data
- Injury count columns (fatal, serious, minor, uninjured) were converted to numeric and **missing values were imputed as zero**, assuming absent entries indicate no recorded injuries.
- **Total passengers per accident** were estimated as the sum of all injury categories.
- Two derived metrics were constructed:
  - **Serious_Fatal.Injuries** = Fatal + Serious injuries
  - **Serious_Fatal.Rate** = (Fatal + Serious) / Total.People  
- Records with **zero total occupants** were removed to avoid invalid rates.

These steps allow injury risk to be compared consistently across aircraft of different sizes.


### Aircraft Damage
- Damage categories were standardized for consistent labeling.
- A binary variable, **Destroyed.Flag**, was created:
  - `1` = Aircraft destroyed  
  - `0` = Aircraft not destroyed  

This simplifies aircraft robustness into a measurable outcome aligned with insurer priorities.



### Manufacturer (Make) Cleaning
- Manufacturer names contained case and formatting inconsistencies (e.g., “Cessna” vs “CESSNA”).
- All makes were standardized to uppercase and whitespace removed.
- Only manufacturers with **≥ 50 accident records** were retained to reduce noise and improve reliability.



### Model and Aircraft Identification
- Aircraft model names were found to be **non‑unique across manufacturers** (e.g., the same model label used by multiple makes).
- To avoid mixing different aircraft types, a unique identifier was created:
  - **Aircraft.Type = Make + Model**
- Rows missing model information were removed, as model‑level analysis is central to this study.



### Other Operational Variables
The following fields were cleaned using **standardization rather than aggressive imputation**, preserving data integrity:
- **Engine.Type**: Unified unknown/UNK/NaN into a single “unknown” category
- **Weather.Condition**: Consolidated unknown values into “UNK”
- **Purpose.of.flight**: Standardized text and unified unknown categories
- **Broad.phase.of.flight**: Consolidated missing and unknown values
- **Number.of.Engines**: Retained as numeric with missing values preserved

Columns with excessive missingness (e.g., aircraft category) were dropped.



## Aircraft Size Segmentation
Aircraft were grouped using estimated passenger count:
- **Small aircraft**: ≤ 20 passengers
- **Large aircraft**: > 20 passengers

This distinction is critical, as safety outcomes and variability differ substantially by size.


## Summary of Key Findings

- **Large aircraft models** show consistently **near‑zero fatal/serious injury rates** and very low destruction likelihood, with tight distributions indicating stable safety performance.
- **Small aircraft models** exhibit greater variability, with some models performing well but others showing higher injury dispersion.
- Manufacturer and **model selection matters far more for small aircraft** than for larger transport-category aircraft.

Visualizations (bar charts, violin plots, strip plots) and summary statistics were used throughout to support each conclusion.



## Tools Used
- Python (Pandas, NumPy)
- Matplotlib, Seaborn
- Jupyter Notebook



## Deliverables
- Cleaned dataset: `aviation_cleaned_data.csv`
- Exploratory and analytical notebook(s)
- This project documentation (README.md)
