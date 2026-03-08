## Live Demo
Interactive web app: [kritika-ecg-hrv.streamlit.app](https://kritika-ecg-hrv.streamlit.app)

# ECG QRS Detector and HRV Analyzer

## Overview
A signal processing pipeline that automatically detects heartbeats (R-peaks) 
from raw ECG signals, validates against cardiologist annotations, and computes 
Heart Rate Variability (HRV) metrics used in clinical cardiology research.

## Validation Results
Validated against cardiologist annotations from MIT-BIH Arrhythmia Database.

| Metric | Value |
|--------|-------|
| Sensitivity | 91.67% |
| Precision | 100.00% |
| True Positives | 11 |
| False Positives | 0 |
| False Negatives | 1 |

Note: 1 missed beat at t=0.05s attributed to Butterworth filter 
warm-up effect — consistent with Pan-Tompkins (1985) edge effect findings.

## HRV Analysis Results
| Metric | Value | Clinical Reference |
|--------|-------|-------------------|
| Heart Rate | 74.6 BPM | Normal: 60-100 BPM |
| SDNN | 81.58 ms | Healthy: >50 ms |
| RMSSD | 141.85 ms | Higher = better autonomic function |
| pNN50 | 40.0% | Healthy: >20% |

## Pipeline
1. Load ECG data directly from PhysioNet MIT-BIH Arrhythmia Database via WFDB API
2. Apply 4th order Butterworth bandpass filter (5-15 Hz) to remove 
   baseline wander and muscle noise
3. Detect R-peaks using adaptive threshold (30% of signal maximum amplitude)
4. Validate detections against cardiologist annotations using 50-sample tolerance
5. Compute RR intervals and clinical HRV metrics

## Key Finding
Filter warm-up effect causes missed detection in first 100 samples.
This is a documented limitation of zero-phase Butterworth filters 
on signal boundaries, consistent with Pan-Tompkins (1985).

## Dataset
- Source: PhysioNet MIT-BIH Arrhythmia Database
- Accessed via: WFDB Python API (industry standard)
- Record: 100 (standard benchmark)
- Sampling frequency: 360 Hz
- Annotations: Cardiologist marked R-peaks (.atr files)
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
   (ECG data downloads automatically from PhysioNet)

## Author
Kritika
B.Tech Biomedical Engineering






