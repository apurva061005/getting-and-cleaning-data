# Getting and Cleaning Data – Course Project

## Overview

This repository contains the deliverables for the **Getting and Cleaning Data** course project (Johns Hopkins / Coursera). The goal is to collect, work with, and clean the UCI Human Activity Recognition (HAR) dataset so that the result is a tidy dataset ready for later analysis.

---

## Repository Contents

| File | Description |
|------|-------------|
| `run_analysis.R` | Main R script that downloads, merges, cleans, and summarises the data |
| `tidyData.txt` | Output tidy dataset produced by `run_analysis.R` |
| `CodeBook.md` | Describes all variables, transformations, and the study design |
| `README.md` | This file – explains the project and how the scripts work |

---

## Raw Data Source

The raw data represent measurements collected from the accelerometer and gyroscope of a Samsung Galaxy S II smartphone worn on the waist by 30 volunteers performing six activities.

- **Full description:** http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones  
- **Download URL:** https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

`run_analysis.R` downloads and unzips this file automatically; no manual download is needed.

---

## How `run_analysis.R` Works

The script performs five sequential steps as required by the project rubric.

### Step 1 – Merge the training and test sets
The raw data are split into a **training** set (70 % of subjects) and a **test** set (30 % of subjects). The script reads both, attaches the corresponding subject identifiers and activity labels, then row-binds them into a single `combined` data table (10 299 rows × 68 columns before reshaping).

### Step 2 – Extract mean and standard deviation measurements
Using `grep("(mean|std)\\(\\)", ...)` the script selects only the 66 feature columns whose names contain `mean()` or `std()`. This intentionally excludes `meanFreq()` and angle-based mean variables, which are not direct mean/SD measurements of the sensor signals.

### Step 3 – Apply descriptive activity names
The integer activity codes (1–6) are replaced with human-readable factor labels sourced from `activity_labels.txt`:

| Code | Label |
|------|-------|
| 1 | WALKING |
| 2 | WALKING_UPSTAIRS |
| 3 | WALKING_DOWNSTAIRS |
| 4 | SITTING |
| 5 | STANDING |
| 6 | LAYING |

### Step 4 – Label the dataset with descriptive variable names
Column names are taken directly from `features.txt` for the selected features. Parentheses `()` are stripped to keep names clean (e.g. `tBodyAcc-mean-X` rather than `tBodyAcc-mean()-X`). No further abbreviation expansion is applied; the original naming convention is preserved so the CodeBook remains the authoritative reference.

### Step 5 – Create the independent tidy summary dataset
`reshape2::melt` converts the wide table to long format, then `reshape2::dcast` computes the **mean of each variable for every (SubjectNum, Activity) combination**. The result (180 rows × 68 columns) is written to `tidyData.txt` using `data.table::fwrite`.

---

## How to Run

1. Open R or RStudio.
2. Set your working directory to the folder containing `run_analysis.R`.
3. Ensure the packages `data.table` and `reshape2` are installed:
   ```r
   install.packages(c("data.table", "reshape2"))
   ```
4. Source the script:
   ```r
   source("run_analysis.R")
   ```
5. `tidyData.txt` will be written to the working directory.

To read the output back into R:
```r
tidy <- data.table::fread("tidyData.txt")
```

---

## Tidy Data Principles

The output satisfies the three tidy-data rules:

1. Each variable forms one column.  
2. Each observation (one subject + one activity combination) forms one row.  
3. Each observational unit (the summarised HAR measurements) forms one table.
