# DS201Cap1

# Getting into Business: Real Estate Investment Data Exploration

**Authors:** John Tapia, Jacob Dudas, and James Pfaff  
**Notebook:** [DSCap1v2 (2).ipynb](DSCap1v2%20%282%29.ipynb)

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/USERNAME/REPOSITORY/blob/main/DSCap1v2%20%282%29.ipynb)

> Replace `USERNAME` and `REPOSITORY` in the Colab badge with your GitHub username and repository name after uploading the notebook. If you rename the notebook, update both links above.

## Project overview

How have U.S. house prices changed over time, and what else should someone consider before investing in a location? We explore the Federal Housing Finance Agency (FHFA) House Price Index (HPI), describe its structure and missing values, and visualize national and state level trends. We then consider natural hazard risk using FEMA's National Risk Index.

The HPI is an **index of price changes**, not the dollar price of a house. A high index value alone does not show that a state has the most expensive homes or offers the best investment.

## Data sources

| Source | Use in this project | Link |
| --- | --- | --- |
| FHFA HPI master file | Historical house price index observations for different geographies, frequencies, and index series | [FHFA HPI](https://www.fhfa.gov/data/house-price-index) · [CSV used by notebook](https://www.fhfa.gov/hpi/download/monthly/hpi_master.csv) |
| FHFA HPI data dictionary | Definitions of the HPI fields | [Excel dictionary](https://www.fhfa.gov/document/d/hpi/hpi_dictionary.xlsx) |
| FEMA National Risk Index, county table | County level natural hazard risk and expected building losses | [Dataset page](https://www.fema.gov/about/openfema/data-sets/national-risk-index-data) |

The notebook downloads the FHFA CSV and dictionary directly. It also downloads FEMA's county table, so no manual upload is needed. FHFA draws on repeat transactions involving mortgages purchased or securitized by Fannie Mae and Freddie Mac. The notebook describes data from **1975 through 2026**; because the FHFA file is updated, the last available period may differ when you run it.

## What the notebook does

1. Loads the FHFA data and dictionary and describes the columns, measurement types, time span, and geographic coverage. The data includes U.S. level, Census division, state, metropolitan area, and Puerto Rico observations.
2. Cleans tab characters and empty strings in `note`, counts missing values, and displays numerical and categorical summaries.
3. Plots the average nonseasonally adjusted HPI by year and HPI type.
4. Selects a consistent state level series, averages its periods within each year, and plots the ten states with the highest latest index values in that selected series.
5. Loads selected FEMA National Risk Index fields and discusses how hazard exposure could inform an investment decision alongside price trends.

### Main FHFA fields

| Field | Meaning |
| --- | --- |
| `hpi_type`, `hpi_flavor` | Type and variation of HPI series |
| `frequency`, `period`, `yr` | Reporting frequency, period within the year, and year |
| `level`, `place_name`, `place_id` | Geographic level, location name, and identifier |
| `index_nsa`, `index_sa` | HPI without and with seasonal adjustment |
| `rstderr` | Relative standard error, when available |
| `note` | Notes attached to particular observations, when present |

The notebook displays the complete FHFA data dictionary for additional field details.

## Initial findings and limitations

- The plotted HPI series generally rise over the long run, with variation across index types and states. The notebook notes a decline around the 2008 financial crisis.
- `index_sa`, `rstderr`, and `note` contain missing entries. A missing `note` often simply means that no special note applies. Analyses requiring another missing field should use observations where that field is available.
- The first chart averages across observations from different places and series, so it is an exploratory view rather than a national investment return. The state chart selects states by their **latest index level**, which is sensitive to index construction and does not rank states by house price, profitability, or risk.
- FEMA's county data adds information about natural hazards and expected building losses, including coastal flooding, hurricanes, and wildfires. It is explored as a complementary source; the notebook does **not** merge FEMA risk scores with the FHFA state series or calculate investment returns.

## Run the analysis

Open the notebook with the Colab badge above and choose **Runtime → Run all**, or run it in Jupyter with Python and `pandas`, `numpy`, `matplotlib`, and `openpyxl` installed. The notebook also uses `wget` to retrieve the FHFA and FEMA files and Python's built in `zipfile` module to extract the FEMA table. An internet connection is required. Outputs may change as the source files are updated.

## Assignment

Prepared for **Getting into Business: Real Estate Investment Data Exploration**. The repository includes the original Python notebook and this readable overview of its data, methods, findings, and additional source.
