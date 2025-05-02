# EEG-Based Motor Movement Prediction using Supervised Learning

This repository presents a complete pipeline for classifying motor intentions (left fist vs. right fist imagery) from EEG data using both traditional machine learning and deep learning techniques. The final model—a Convolutional Neural Network (CNN) with two 1D convolutional layers—achieved robust performance, supporting the feasibility of EEG-driven Brain-Computer Interfaces (BCIs) for assistive applications.

**Status**: Completed  
**Last Updated**: May 1, 2025

---

## Project Overview

- **Objective**: Classify imagined motor movements from EEG signals (left vs. right fist).
- **Application**: Brain-computer interfaces for assistive tech and neurorehabilitation.
- **Dataset**: [PhysioNet EEG Motor Movement/Imagery Dataset](https://archive.physionet.org/pn4/eegmmidb/)
- **Subjects**: 20 individuals (runs 4, 8, and 12)
- **EEG Recording**: 64 channels, 160 Hz sampling rate

---

## Methodology

### Preprocessing

- Parsed EDF files and extracted 900 trials
- Applied 1–40 Hz bandpass filter
- Segmented trials between 1s and 4.1s post-cue (497 timepoints)
- Standardized EEG channels using z-score normalization
- **Removed Rest class (T0)** to address class imbalance and improve model focus

### Feature Engineering & Modeling

- **Traditional Models**:  
  - CSP + Logistic Regression  
  - CSP + PCA + Random Forest / SVM / Gradient Boosting

- **Deep Learning Models**:  
  - Dense EEGNet-inspired model (underperformed)  
  - CNN + Transformer Hybrid (moderate)  
  - **Final Model**: 2-layer Conv1D CNN with global average pooling and softmax output

---

## Results

| Model                      | Accuracy | Avg F1-Score | ROC-AUC |
|---------------------------|----------|--------------|---------|
| CSP + Logistic Regression | ~50%     | ~0.50        | ~0.50   |
| CSP + PCA + RF/SVM/GB     | 47–54%   | ~0.48–0.50   | ~0.50   |
| EEGNet-Inspired Dense NN  | 29%      | ~0.29        | —       |
| CNN + Transformer Hybrid  | 67.74%   | 0.65         | 0.73    |
| **Final CNN (2 Conv1D)**  | **76.61%** | **0.75**     | **0.79** |

- **Best Model**: Final CNN (2 Conv1D layers)
- **Average Precision**: 0.83
- **Subject-wise generalization**: Avg. accuracy = 51.8%

---

## Key Findings

- Deep learning models **outperformed traditional ML** by a large margin.
- Removing the rest class (T0) led to **+25% improvement in accuracy**.
- CNNs learned meaningful features directly from raw EEG data.
- Model performed well on pooled data, but subject-level variability remains a challenge.

---

## Future Work

- Explore **subject-specific fine-tuning** or **domain adaptation** techniques
- Extend model to **multi-class classification** (including rest and other tasks)
- Test model in **real-time BCI settings** using OpenBCI or Lab Streaming Layer
- Investigate **shorter/adaptive time windows** to reduce latency
- Apply **data augmentation** (e.g., noise injection, time warping)
- Evaluate **transfer learning** for better generalization across sessions

---

## Repository Contents

- `Model_V2.ipynb`: Traditional ML models (CSP, PCA, classifiers)
- `CNN_BCI_Model.ipynb`: Final deep learning model (Conv1D CNN)
- `Project Final Report - Angel Barrera.pdf`: Full technical report
- `Supervised Learning for Motor Movement Prediction.pptx`: Slide presentation

---

## Author

**Angel Barrera**  
Master’s Student, Applied Data Science  
East Tennessee State University  
Focus: Brain-Computer Interfaces, Machine Learning, and Neural Decoding

---

## References

1. Goldberger AL et al. (2000). "PhysioBank, PhysioToolkit, and PhysioNet: Components of a new research resource for complex physiologic signals." *Circulation.*
2. Lawhern et al. (2018). "EEGNet: A compact convolutional neural network for EEG-based BCIs." *Journal of Neural Engineering.*
3. Ramoser et al. (2000). "Optimal spatial filtering of single trial EEG during imagined hand movement." *IEEE Trans. on Rehabilitation Engineering.*
4. Pfurtscheller & Lopes da Silva (1999). "Event-related EEG/MEG synchronization and desynchronization." *Clinical Neurophysiology.*
5. Fahsi, R. (2020). [EEG Motor Imagery Classification GitHub Repository](https://github.com/reshalfahsi/eeg-motor-imagery-classification)

---

