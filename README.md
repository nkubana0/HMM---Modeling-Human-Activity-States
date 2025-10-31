# Hidden Markov Model for Human Activity Recognition

## Project Overview

This project implements a Hidden Markov Model (HMM) to recognize human activities (standing, walking, jumping, still) from smartphone accelerometer and gyroscope sensor data. The system achieves **76.09% accuracy** on unseen test data.

##  Project Objectives

1. Collect real-world motion sensor data from smartphone
2. Extract time-domain and frequency-domain features
3. Build and train a Gaussian Hidden Markov Model
4. Implement Viterbi algorithm for activity sequence decoding
5. Evaluate model performance on unseen data

##  Dataset

### Data Collection
- **Device**: iPhone with Sensor Logger app
- **Sampling Rate**: 100 Hz
- **Sensors**: Accelerometer (x, y, z) and Gyroscope (x, y, z)
- **Total Recordings**: 15 recordings across 4 activities
- **Total Samples**: 13,000+ sensor measurements

### Activities Recorded
1. **Standing** (3 recordings) - Phone held steady at waist level
2. **Walking** (4 recordings) - Consistent pace, phone in pocket/hand
3. **Jumping** (4 recordings) - Continuous jumping motions
4. **Still** (4 recordings) - Phone on flat surface, no movement

##  Implementation

### Technologies Used
- **Python 3.8+**
- **Libraries**:
  - `hmmlearn` - Hidden Markov Model implementation
  - `scikit-learn` - Machine learning utilities
  - `numpy/scipy` - Numerical computing and signal processing
  - `pandas` - Data manipulation
  - `matplotlib/seaborn` - Data visualization

### Feature Engineering
- **83 Total Features** extracted from sliding windows (1 second, 50% overlap)
  - **54 Time-domain features**: mean, std, variance, min, max, range, median, skewness, kurtosis, RMS, SMA, correlations
  - **18 Frequency-domain features**: dominant frequency, spectral energy, spectral entropy (via FFT)

### Model Architecture
- **Hidden States**: 4 states (one per activity)
- **Emission Model**: Multivariate Gaussian with diagonal covariance
- **Training**: Baum-Welch algorithm (100 iterations)
- **Decoding**: Viterbi algorithm for optimal state sequence

##  Results

### Overall Performance
- **Overall Accuracy**: 76.09%
- **Training Samples**: 250 windows
- **Test Samples**: 92 windows

### Per-Activity Performance

| Activity | Samples | Sensitivity | Specificity | Precision |
|----------|---------|-------------|-------------|-----------|
| Standing | 21      | 1.0000      | 0.7183      | 0.5122    |
| Walking  | 21      | 0.0000      | 1.0000      | 0.0000    |
| Jumping  | 29      | 0.9655      | 0.9683      | 0.9333    |
| Still    | 21      | 1.0000      | 1.0000      | 1.0000    |

### Key Findings
- **Jumping**: Excellent recognition (96.55% sensitivity)
- **Still**: Perfect recognition (100% all metrics)
- **Walking**: Failed to recognize (0% sensitivity)
- **Standing**: High sensitivity but some confusion with other activities

##  Project Structure

```
project/
│
├── hmm_activity_recognition.ipynb    # Main Jupyter notebook
├── requirements.txt                  # Python dependencies
├── README.md                        # This file
│
├── data-recordings/                 # Raw sensor data
│   ├── standing/
│   │   ├── 1/ (Accelerometer.csv, Gyroscope.csv)
│   │   ├── 2/
│   │   └── 3/
│   ├── walking/
│   ├── jumping/
│   └── still/
│
└── outputs/                         # Generated results
    ├── raw_sensor_signals.png
    ├── feature_distributions.png
    ├── transition_matrix.png
    ├── confusion_matrix.png
    ├── decoded_sequences.png
    ├── evaluation_metrics.csv
    ├── model_summary.csv
    └── hmm_model.pkl (trained model)
```

##  Quick Start

### Installation

```bash
# Install dependencies
pip install -r requirements.txt
```

### Running the Notebook

```bash
# Start Jupyter Notebook
jupyter notebook

# Open hmm_activity_recognition.ipynb
# Run all cells
```

### Using Google Colab (Alternative)

1. Upload `hmm_activity_recognition.ipynb` to Google Colab
2. Upload `data-recordings.zip`
3. Update `DATA_DIR` path in notebook
4. Run all cells

##  Visualizations

The notebook generates several visualizations:

1. **Raw Sensor Signals** - Time-series plots of accelerometer/gyroscope data
2. **Feature Distributions** - Distribution of key features by activity
3. **Transition Matrix** - HMM state transition probabilities (heatmap)
4. **Confusion Matrix** - Model prediction accuracy
5. **Decoded Sequences** - True vs predicted activity sequences

##  Analysis & Insights

### What Worked Well
- High-amplitude, periodic activities (jumping) are easily recognizable
- No-movement states (still) are perfectly distinguishable
- Temporal modeling via HMM captures realistic activity transitions
- Feature engineering effectively captures motion characteristics

### Challenges
- Walking recognition failed completely (0% sensitivity)
- Confusion between standing and other low-motion activities
- Limited training data from single participant
- Short recording durations (10-12 seconds)

##  Recommendations for Improvement


### DATA COLLECTION:
- Collecting more samples, especially for activities with lower accuracy
- Increasing recording duration for better feature representation
- Including various participants for better generalization
- Various environmental conditions or surroundings (indoor/outdoor, different surfaces)

### FEATURE ENGINEERING:
- Include time-series features (autocorrelation, entropy measures)
- Experiment with different window sizes and overlap ratios
- Feature selection to reduce dimensionality and noise

### VALIDATION:
- Implement k-fold cross-validation
- Test on completely new participants
- Evaluate real-time performance
- Compare with other models (Random Forest, LSTM, CNN)

##  Learning Outcomes

This project demonstrates:
- Real-world data collection and preprocessing
- Time-series feature extraction techniques
- Hidden Markov Model theory and implementation
- Viterbi algorithm for sequence decoding
- Model evaluation on unseen data
- Critical analysis of results and limitations

## Authors
- Roxanne Niteka
- Ivan Shema

**Note**: The trained model and all outputs are included in the `outputs/` directory. The complete analysis and discussion are available in the written report.

[REPORT](https://docs.google.com/document/d/1oCYuhRYj1aRkStdrOxEqhYvnKWenDmzNJ3gJfk9p-9o/edit?tab=t.0)