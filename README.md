
# MIT-805-Big-Data-Project

Large-Scale Data Analysis and Distributed Processing with PySpark

  

### Author

- Tshepo Molebiemang (u28174862)

  

---

  

## Project Overview

  

This project analyses the **NYC Taxi & Limousine Commission (TLC) High Volume For-Hire Vehicle (HVFHV) trip records**, which hold every Uber and Lyft trip in New York City, as part of the MIT 805 Big Data Semester Project.

  

-  **Part 1 – Data Collection & Analysis:** collect the data, assess its quality, clean it, run an exploratory data analysis (EDA).

-  **Part 2 – MapReduce & Visualisation:** use PySpark to answer one central question with MapReduce-style processing (map, shuffle, reduce), and show evidence of Spark's distributed execution.

  

**Central question (Part 2):** How did NYC's congestion pricing, which started on 5 January 2025, change Uber and Lyft trips that start or end in the Manhattan charging zone, compared with trips elsewhere in the city?

  

---

  

## Dataset Information

  

### Dataset Name

NYC TLC High Volume For-Hire Vehicle (HVFHV) Trip Records

  

### Source

New York City Taxi & Limousine Commission (TLC)

  

### Dataset URL

https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page

  

Data dictionary: https://www.nyc.gov/assets/tlc/downloads/pdf/data_dictionary_trip_records_hvfhs.pdf

  

### Licence / Terms of Use

The TLC trip records are public data published by the City of New York and are free to use, including for academic purposes (NYC Open Data Terms of Use). The data contains no personal information: locations are recorded only as one of 263 taxi zones, and there are no names, card details or exact addresses.

  

### Description

  

- One Parquet file per month, published monthly (records from February 2019 onwards)

- One row per trip, 25 columns

- Companies: Uber (licence `HV0003`) and Lyft (licence `HV0005`)

- A separate lookup table, `taxi_zone_lookup.csv`, maps each zone ID to its borough and zone name

  

Main columns:

  

| Column | Meaning |

|---|---|

| `hvfhs_license_num` | Company licence: HV0003 = Uber, HV0005 = Lyft |

| `request_datetime`, `pickup_datetime`, `dropoff_datetime` | When the ride was requested, started and ended |

| `PULocationID`, `DOLocationID` | Pickup and drop-off taxi zone |

| `trip_miles`, `trip_time` | Distance (miles) and duration (seconds) |

| `base_passenger_fare` | Fare before tolls, taxes, fees and tips |

| `tolls`, `bcf`, `sales_tax`, `congestion_surcharge`, `airport_fee` | Extra charges (`bcf` = Black Car Fund) |

| `cbd_congestion_fee` | Congestion pricing charge (only exists from January 2025) |

| `tips`, `driver_pay` | Tip, and what the driver was paid |

| `shared_request_flag`, `shared_match_flag`, `wav_request_flag`, `wav_match_flag` | Shared rides and wheelchair-accessible vehicle requests (Y/N) |

  

---

  

## Dataset Sizes

  

### Raw Dataset

- HVFHV trip records, ** February 2019 – June 2026**

-  **40.4 GB**

  

### Working Dataset

- 27 monthly files, January 2024 – March 2026, downloaded for Part 1

-  **13.25 GB** (printed by the download cell in `mit805_grp13_part1.ipynb`)

- 545,934,549 trips before cleaning; 545,213,799 after cleaning (0.13% removed)

  

### Processing Dataset

- 8 monthly files used in Part 2: January – April 2024 (before congestion pricing) and January – April 2025 (after)

- Raw files: **3.86 GB**

- Cleaned dataset processed by PySpark: **5.19 GB** (printed in `mit805_grp13_part2.ipynb`)

- Why this subset: the same four months in each year, so seasons don't distort the before/after comparison, and small enough to process on a free Colab runtime

  

---

  

## Data Preparation

  

The same cleaning rules are used in both notebooks. A trip is kept only if:

- distance is above 0 and below 100 miles

- duration is above 0 and below 4 hours

- base fare is above $0 and below $500

- driver pay is not negative

- drop-off is after pickup

- pickup falls inside the period being analysed

  

Missing `cbd_congestion_fee` values (all trips before 2025) are filled with 0. The notebooks also add `company`, `pickup_month`, `pickup_hour`, `pickup_day` and `trip_minutes` columns.

  

---

  

## How to Reproduce

  

Both notebooks run on **Google Colab** with a standard **CPU** runtime. Each one downloads its own data, so they can run independently, top to bottom, in a fresh session.

  

1. Open the notebook in Google Colab (**File → Upload notebook**).

2. Run all cells in order.

-  `notebooks/mit805_grp13_part1.ipynb`: downloads the 27 working months, explores and cleans the data and plots the EDA charts (Part 1).

-  `notebooks/mit805_grp13_part2.ipynb`: downloads the 8 study months, cleans them, and runs the MapReduce analysis (Part 2).

3. Part 2 saves its result tables to Google Drive (`MyDrive/mit805_results/`). Copy them into `output/` in this repository.

  

**Software:** Python 3, PySpark (Colab ships with Spark 4.0.4), pandas, matplotlib, seaborn. See `requirements.txt`.

  

**Manual download (optional):** on the TLC page above, open a year and download the **High Volume For-Hire Vehicle Trip Records** files (`fhvhv_tripdata_YYYY-MM.parquet`). The taxi zone lookup table is at https://d37ci6vzurychx.cloudfront.net/misc/taxi_zone_lookup.csv.

  

---

  

## Note

The trip data is not included in this repository because of its size (several GB per year). The notebooks download it directly from the TLC.

  

---

  

## Repository Structure

```text

project/

│

├── README.md

├── requirements.txt

│

├── data/

│ └── README.md # where to get the data (not stored in the repo)

│

├── notebooks/

│ ├── mit805_grp13_part1.ipynb # Part 1: download, quality checks, cleaning, EDA

│ └── mit805_grp13_part2.ipynb # Part 2: MapReduce analysis with PySpark

│ └── [old_dataset] MIT 805 Project.ipynb # Original Part 1 Dataset and EDA

│

├── src/ # helper scripts (all code currently lives in the notebooks)

│

├── output/

│ ├── summary_by_period_area.csv # totals and averages per period and area

│ ├── change_before_after.csv # % change 2024 → 2025, charging zone vs outside

│ ├── hourly_by_period_area.csv # trips and speed by hour of day

│ └── zone_fee_share.csv # share of trips paying the congestion fee, per pickup zone

│

├── figures/ # charts from the notebooks and Spark UI screenshots

│

└── report/

├── MIT805_Part1_Report.pdf

└── MIT805_Part2_Report.pdf

```