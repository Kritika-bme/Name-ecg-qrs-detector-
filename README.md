# ECG QRS Detector and HRV Analyzer

## Overview
A signal processing pipeline that automatically detects heartbeats (R-peaks) 
from raw ECG signals and computes Heart Rate Variability (HRV) metrics used 
in clinical cardiology research.

## Results
| Metric | Value |
|--------|-------|
| Heart Rate | 74.6 BPM |
| SDNN | 81.58 ms |
| RMSSD | 141.85 ms |
| pNN50 | 40.0% |

## Pipeline
1. Load ECG data directly from PhysioNet MIT-BIH Arrhythmia Database via WFDB API
2. Apply Butterworth bandpass filter (5-15 Hz) to remove baseline wander and noise
3. Detect R-peaks using adaptive threshold (30% of maximum amplitude)
4. Calculate RR intervals and clinical HRV metrics

## HRV Metrics Explained
- SDNN: Standard deviation of RR intervals — overall HRV measure
- RMSSD: Root mean square of successive differences — short term HRV
- pNN50: Percentage of successive RR intervals differing by more than 50ms

## Dataset
- Source: PhysioNet MIT-BIH Arrhythmia Database
- Record: 100 (standard benchmark record)
- Sampling frequency: 360 Hz
- Duration: 8.33 seconds
- Link: https://physionet.org/content/mitdb/1.0.0/

## Technologies
- Python 3.13
- numpy, scipy
- wfdb (PhysioNet WFDB API)
- matplotlib

## How to Reproduce
1. Clone this repository
2. pip install -r requirements.txt
3. Run 01_ecg_detector.ipynb sequentially
   (data downloads automatically from PhysioNet)

## Author
Kritika
Biomedical Engineering, 2nd Year
