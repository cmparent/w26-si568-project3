# HRV Stress Labels — EDA & Visualizations

Exploratory data analysis (EDA) of a heart rate / HRV-related dataset with stress-condition labels. This repo/script loads an Excel workbook containing multiple sheets (participants), concatenates them into one dataframe, performs light preprocessing (timestamp parsing), and generates three core visualizations for a fictional “villainous data plan” assignment.

## Contents
- Load multi-sheet Excel label file into a single dataframe
- Basic dataset inspection (unique subjects, `.info()`, label distributions)
- Timestamp parsing + hour-of-day extraction
- Visualizations:
  1) Heart Rate by Hour of Day & Label  
  2) Heart Rate by Label & Condition  
  3) Heatmap: Share of “Stressed” Observations (Time Pressure/Interruption) by Subject & Hour

## Data Source / Location
This script expects the Excel file at:
`hrv dataset/data/raw/labels/hrv stress labels.xlsx`

It reads **all sheets** and concatenates them into one dataframe.

## Requirements
Python packages:
- pandas
- matplotlib
- seaborn

## How to Run
Confirm the Excel file path matches your local directory structure.
Run the script (or run cells in a notebook).

The script will also export a CSV: heart_rate_data_all.csv

## Dataset Schema (expected columns)
From .info() after load/concat:

- PP (object)
- C (int)
- timestamp (object → parsed to datetime)
- HR (float; has missing values)
- RMSSD (float; has missing values)
- SCL (float; partially missing)
- date (datetime)
- subject (object; ~25 unique)
- label (object; values: rest, no stress, time pressure, interruption)
- Condition (object; values: R, N, T, I)
- ElapsedTime (int)

## Preprocessing Notes
- ```timestamp``` values may be inconsistent; the script uses pd.to_datetime(..., errors="coerce").
- If timestamp cannot be parsed, it falls back to the date column.
- ```hour``` is derived from the parsed timestamp for time-of-day visualizations.

## Visualizations Produced
1) Heart Rate by Hour of Day & Label
Line plot of average HR across hours (0–23), split by label (rest, no stress, time pressure, interruption).
2) Heart Rate by Label & Condition
Box plot of HR distributions by label, grouped by Condition (R/N/T/I).
4) Heatmap: % “Stressed” Observations by Subject & Hour
Heatmap where each cell is the share of observations labeled as “stressed” for a subject-hour pair.
“Stressed” is defined as labels in: {"time pressure", "interruption"}.

