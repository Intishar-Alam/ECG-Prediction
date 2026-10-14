# ECG Heartbeat Classification with Random Forest

A machine learning project that classifies ECG heartbeats into 5 types using the MIT-BIH Arrhythmia dataset. The main challenge was **class imbalance**, so this project compares three ways to handle it.

> **Status:** Version 1 (model training). Work in progress.

---

## Project Goal

Build a model that can read a heartbeat signal and predict its type. The long-term goal is to turn this into a full edge project where a user can upload an ECG image and get a prediction.

## Dataset

- **Source:** MIT-BIH Arrhythmia Database (preprocessed CSV version from Kaggle)
- **Files used:** `mitbih_train.csv` and `mitbih_test.csv`
- **Each row:** one heartbeat signal, with the class label in the last column

### Classes

| Label | Heartbeat Type |
|---|---|
| 0 | Normal |
| 1 | Supraventricular |
| 2 | Ventricular |
| 3 | Fusion |
| 4 | Unknown |

> Please check these label names against the dataset page on Kaggle before publishing.

## The Problem: Class Imbalance

The dataset has far more **Normal** beats than the other 4 types. If this is ignored, the model learns the Normal class well but does poorly on the rare classes. In medical data, the rare classes are often the most important ones.

## Approach

I compared 3 methods using a Random Forest Classifier:

1. **Baseline:** no fix for imbalance
2. **Class weights:** give more weight to rare classes during training
3. **Oversampling:** increase the number of rare class samples in the training data

### Steps

1. Load the train and test data
2. Explore the data (class counts, one plotted beat per class, data checks)
3. Train the baseline Random Forest
4. Train with class weights
5. Train with oversampling
6. Compare F1 scores on the test set

## Results

F1 score for each class, and macro F1:

| Method | Normal | Supraventricular | Ventricular | Fusion | Unknown | Macro F1 |
|---|---|---|---|---|---|---|
| Baseline | 0.986 | 0.754 | 0.927 | 0.720 | 0.974 | 0.873 |
| Class weights | 0.986 | 0.748 | 0.933 | 0.764 | 0.977 | 0.882 |
| Oversampling | 0.988 | 0.783 | 0.941 | 0.759 | 0.981 | **0.891** |

### Key Findings

- **Oversampling** gave the best macro F1 score (0.891).
- **Macro F1** treats every class equally, so it is a fair metric for imbalanced data.
- **Supraventricular** and **Fusion** are still the weakest classes. These are the main focus for improvement.

## Tech Stack

- Python
- Pandas, NumPy
- Scikit-learn
- Matplotlib
- Google Colab

## How to Run

1. Download the dataset from Kaggle (MIT-BIH preprocessed CSV files).
2. Open the notebook in Google Colab, or run it locally.
3. Upload `mitbih_train.csv` and `mitbih_test.csv`.
4. Run the notebook cells from top to bottom.

## Roadmap

- [x] Data exploration
- [x] Random Forest baseline
- [x] Handle imbalance (class weights and oversampling)
- [ ] Improve results for Supraventricular and Fusion classes
- [ ] Image pre-processing for ECG pictures
- [ ] Build an app where users can upload an ECG image
- [ ] Deploy as a full edge project

## Limitations

- This is a learning project. It is **not** a medical tool and must not be used for real diagnosis.
- Oversampling must be applied only to the training data, never to the test data.
- Results are from one dataset and one model type.

## Author

**Md Intishar Alam**
AI/ML Engineering student

---

*I will keep updating this project as I learn more.*