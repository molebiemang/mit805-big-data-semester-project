# MIT-805-Big-Data-Project
## Part 1: Data Collection and Analysis
Large-Scale Data Analysis and Distributed Processing with PySpark

### Group Members
- Buhle Ndlela (u22848322)
- Tshepo Molebiemang (u28174862)

---

## Project Overview

This project investigates the NIH ChestX-ray14 dataset as part of the MIT 805 Big Data Semester Project. The objective is to explore large-scale healthcare data, assess data quality, perform exploratory data analysis (EDA), and evaluate the dataset using the 7 Vs of Big Data.

The dataset consists of chest X-ray images and associated metadata containing patient demographics and disease labels. The project forms the foundation for subsequent distributed processing and analysis using PySpark.

---

## Dataset Information

### Dataset Name
NIH ChestX-ray14

### Source
National Institutes of Health (NIH) Clinical Center

### Dataset URL
https://nihcc.app.box.com/v/ChestXray-NIHCC

### Description

The ChestX-ray14 dataset contains:

- 112,120 frontal chest X-ray images
- 30,805 unique patients
- 14 thoracic disease labels
- Multi-label disease annotations derived from radiology reports using Natural Language Processing (NLP)

The disease categories include:

- Atelectasis
- Cardiomegaly
- Consolidation
- Edema
- Effusion
- Emphysema
- Fibrosis
- Hernia
- Infiltration
- Mass
- Nodule
- Pleural Thickening
- Pneumonia
- Pneumothorax

---

## Dataset Sizes

### Raw Dataset
- Original NIH ChestX-ray14 dataset
- Approximately 45 GB
- 112,120 images

### Working Dataset
- Downloaded subset used for analysis
- 34,999 images
- Corresponding metadata records

### Processing Dataset
- Subset to be used for PySpark processing in Part 2
- To be finalized during distributed analysis

---

## Download Instructions
1. Visit the NIH ChestX-ray14 dataset page.
2. Download the image archives.
3. Download the metadata file:
- Data_Entry_2017_v2020.csv
- Store it in folder name: Data/raw dataset
4. Extract all image archives into a single folder named:
Data/working dataset/images/

---

## Note
The image dataset is not included in this repository because of its large size and redistribution restrictions. Users should download the dataset directly from the NIH source.

## Repository Structure
```text
project/
│
├── README.md
├── requirements.txt
│
├── data/
│   ├── raw_dataset/
│   │   └── Data_Entry_2017_v2020.csv
│   │
│   ├── working_dataset/
│   │   └── images/
│   │
│   ├── processing_dataset/
│   │   └── df_subset.csv
│   │
│   ├── README.md
|   ├── README_CHESTXRAY.pdf
│
├── output/
│ └── df_subset.csv
│
├── notebooks/
│   └── MIT 805 Project.ipynb.ipynb
│
├── figures/
│   ├── sample_images.png
│   ├── age_distribution.png
│   ├── gender_distribution.png
│   ├── disease_frequency.png
│   └── disease_by_age_heatmap.png
│
└── report/
    └── MIT805_Part1_Report.pdf
```