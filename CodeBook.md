# CodeBook – Getting and Cleaning Data Course Project

## Study Design

### Original data collection
30 volunteers (age 19–48) wore a Samsung Galaxy S II on the waist while performing six activities. The phone's accelerometer and gyroscope captured 3-axial linear acceleration and 3-axial angular velocity at 50 Hz. Sensor signals were pre-processed with noise filters and sampled in fixed-width sliding windows (2.56 s, 50 % overlap → 128 readings/window). Gravity and body-motion components were separated using a Butterworth low-pass filter (0.3 Hz cutoff).

### Transformations applied in `run_analysis.R`
1. Training set (7 352 obs.) and test set (2 947 obs.) were merged → **10 299 observations**.
2. Only the 66 features measuring **mean()** or **std()** of a signal were retained.
3. Integer activity codes were replaced with descriptive factor labels.
4. Parentheses were removed from feature names.
5. The dataset was summarised: **mean of each variable per (subject, activity) pair** → **180 rows** (30 subjects × 6 activities).

---

## Variable Descriptions

### Identifier variables

| Variable | Type | Values | Description |
|----------|------|--------|-------------|
| `SubjectNum` | Factor | 1 – 30 | Anonymous volunteer identifier |
| `Activity` | Factor | See below | Activity performed during measurement |

**Activity levels:**

| Level | Label |
|-------|-------|
| 1 | WALKING |
| 2 | WALKING_UPSTAIRS |
| 3 | WALKING_DOWNSTAIRS |
| 4 | SITTING |
| 5 | STANDING |
| 6 | LAYING |

---

### Measurement variables (columns 3 – 68)

All 66 measurement columns contain the **mean** (averaged across windows) of the named feature for a given subject and activity combination.

**Units:**
- Accelerometer-derived signals (`Acc`): standard gravity units **g**
- Gyroscope-derived signals (`Gyro`): **radians/second**
- Jerk signals (`Jerk`): **g/s** (accelerometer) or **rad/s²** (gyroscope)
- Magnitude signals (`Mag`): same unit as parent signal, computed via Euclidean norm
- Frequency-domain signals (`f` prefix): unit of the corresponding time-domain signal

**Name structure:** `<domain><Sensor><Component>-<statistic>-<axis>`

| Segment | Meaning |
|---------|---------|
| `t` prefix | Time domain |
| `f` prefix | Frequency domain (FFT applied) |
| `Body` | Body-motion component |
| `Gravity` | Gravity component |
| `Acc` | Accelerometer signal |
| `Gyro` | Gyroscope signal |
| `Jerk` | Jerk (time derivative of acceleration or angular velocity) |
| `Mag` | Magnitude of the 3-axial signal |
| `-mean` | Mean of the signal windows |
| `-std` | Standard deviation of the signal windows |
| `-X / -Y / -Z` | Axis (triaxial signals only) |

---

### Full variable list

#### Time-domain body accelerometer
| Column | Variable name |
|--------|--------------|
| 3 | `tBodyAcc-mean-X` |
| 4 | `tBodyAcc-mean-Y` |
| 5 | `tBodyAcc-mean-Z` |
| 6 | `tBodyAcc-std-X` |
| 7 | `tBodyAcc-std-Y` |
| 8 | `tBodyAcc-std-Z` |

#### Time-domain gravity accelerometer
| Column | Variable name |
|--------|--------------|
| 9 | `tGravityAcc-mean-X` |
| 10 | `tGravityAcc-mean-Y` |
| 11 | `tGravityAcc-mean-Z` |
| 12 | `tGravityAcc-std-X` |
| 13 | `tGravityAcc-std-Y` |
| 14 | `tGravityAcc-std-Z` |

#### Time-domain body accelerometer jerk
| Column | Variable name |
|--------|--------------|
| 15 | `tBodyAccJerk-mean-X` |
| 16 | `tBodyAccJerk-mean-Y` |
| 17 | `tBodyAccJerk-mean-Z` |
| 18 | `tBodyAccJerk-std-X` |
| 19 | `tBodyAccJerk-std-Y` |
| 20 | `tBodyAccJerk-std-Z` |

#### Time-domain body gyroscope
| Column | Variable name |
|--------|--------------|
| 21 | `tBodyGyro-mean-X` |
| 22 | `tBodyGyro-mean-Y` |
| 23 | `tBodyGyro-mean-Z` |
| 24 | `tBodyGyro-std-X` |
| 25 | `tBodyGyro-std-Y` |
| 26 | `tBodyGyro-std-Z` |

#### Time-domain body gyroscope jerk
| Column | Variable name |
|--------|--------------|
| 27 | `tBodyGyroJerk-mean-X` |
| 28 | `tBodyGyroJerk-mean-Y` |
| 29 | `tBodyGyroJerk-mean-Z` |
| 30 | `tBodyGyroJerk-std-X` |
| 31 | `tBodyGyroJerk-std-Y` |
| 32 | `tBodyGyroJerk-std-Z` |

#### Time-domain magnitudes
| Column | Variable name |
|--------|--------------|
| 33 | `tBodyAccMag-mean` |
| 34 | `tBodyAccMag-std` |
| 35 | `tGravityAccMag-mean` |
| 36 | `tGravityAccMag-std` |
| 37 | `tBodyAccJerkMag-mean` |
| 38 | `tBodyAccJerkMag-std` |
| 39 | `tBodyGyroMag-mean` |
| 40 | `tBodyGyroMag-std` |
| 41 | `tBodyGyroJerkMag-mean` |
| 42 | `tBodyGyroJerkMag-std` |

#### Frequency-domain body accelerometer
| Column | Variable name |
|--------|--------------|
| 43 | `fBodyAcc-mean-X` |
| 44 | `fBodyAcc-mean-Y` |
| 45 | `fBodyAcc-mean-Z` |
| 46 | `fBodyAcc-std-X` |
| 47 | `fBodyAcc-std-Y` |
| 48 | `fBodyAcc-std-Z` |

#### Frequency-domain body accelerometer jerk
| Column | Variable name |
|--------|--------------|
| 49 | `fBodyAccJerk-mean-X` |
| 50 | `fBodyAccJerk-mean-Y` |
| 51 | `fBodyAccJerk-mean-Z` |
| 52 | `fBodyAccJerk-std-X` |
| 53 | `fBodyAccJerk-std-Y` |
| 54 | `fBodyAccJerk-std-Z` |

#### Frequency-domain body gyroscope
| Column | Variable name |
|--------|--------------|
| 55 | `fBodyGyro-mean-X` |
| 56 | `fBodyGyro-mean-Y` |
| 57 | `fBodyGyro-mean-Z` |
| 58 | `fBodyGyro-std-X` |
| 59 | `fBodyGyro-std-Y` |
| 60 | `fBodyGyro-std-Z` |

#### Frequency-domain magnitudes
| Column | Variable name |
|--------|--------------|
| 61 | `fBodyAccMag-mean` |
| 62 | `fBodyAccMag-std` |
| 63 | `fBodyBodyAccJerkMag-mean` |
| 64 | `fBodyBodyAccJerkMag-std` |
| 65 | `fBodyBodyGyroMag-mean` |
| 66 | `fBodyBodyGyroMag-std` |
| 67 | `fBodyBodyGyroJerkMag-mean` |
| 68 | `fBodyBodyGyroJerkMag-std` |

---

## Notes

- All measurement values in `tidyData.txt` are **averages** of the original normalised feature values (normalised to [−1, 1] in the raw dataset), so they are dimensionless ratios even though the underlying physical unit is noted above for interpretive purposes.
- `meanFreq()` variables and angle-based mean variables present in the original feature set were **excluded** because they are weighted averages of frequency components or angles between vectors, not direct means of sensor signals.
- The `fBodyBody` prefix in several frequency-domain magnitude columns appears in the original `features.txt` and is retained as-is.
