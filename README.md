# Detecting GAN-Based Data Inversion in Collaborative Deep Learning

<p align="center">
  <b>A Machine Learning-Based Framework for Detecting Privacy Leakage Through Gradient Anomaly Detection</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-blue?logo=python" />
  <img src="https://img.shields.io/badge/PyTorch-Deep%20Learning-orange?logo=pytorch" />
  <img src="https://img.shields.io/badge/Scikit--learn-Machine%20Learning-F7931E?logo=scikitlearn" />
  <img src="https://img.shields.io/badge/Status-Research%20Prototype-success" />
</p>

---

## Overview

Collaborative Deep Learning enables multiple clients to jointly train machine learning models without directly sharing their private datasets. However, sharing model gradients and parameter updates can expose sensitive information about the underlying training data.

**Gradient Inversion Attacks** exploit this vulnerability by analyzing shared gradients to reconstruct private training samples. Generative Adversarial Networks (GANs) can be used as part of such reconstruction approaches.

This project explores a machine learning-based security framework for identifying suspicious gradient submissions in collaborative deep learning environments.

Instead of accessing or decrypting private training data, the system extracts statistical characteristics from gradient updates and applies anomaly detection techniques to identify potentially malicious behavior.

## Problem Statement

Although collaborative learning reduces the need to centralize private datasets, exchanged gradients may still leak information about the original training samples.

An adversarial participant can exploit these gradients to perform data inversion attacks, potentially compromising data confidentiality.

The objective of this project is to develop a lightweight monitoring framework that:

- Analyzes incoming gradient updates.
- Extracts statistical representations of gradient tensors.
- Identifies anomalous gradient patterns.
- Flags suspicious client submissions.
- Supports simulated client isolation and monitoring.

## System Architecture

The proposed workflow consists of the following stages:

1. **Collaborative Learning Simulation:** Multiple clients generate model updates using local training data.
2. **Gradient Generation:** A CNN processes MNIST samples and produces parameter gradients.
3. **Suspicious Gradient Simulation:** Abnormal gradient submissions are generated to simulate adversarial behavior.
4. **Feature Extraction:** Statistical characteristics are extracted from gradient tensors.
5. **Anomaly Detection:** An Isolation Forest model identifies gradient submissions that deviate from learned normal patterns.
6. **Client Monitoring:** Suspicious submissions are flagged or rejected, with simulated client isolation.
7. **Visualization and Reporting:** Detection decisions, logs, and performance metrics are presented through dashboards and reports.

## Methodology

### 1. Dataset and Model

- Dataset: MNIST handwritten digit dataset.
- Model: Custom Convolutional Neural Network (CNN).
- Framework: PyTorch.

The CNN is used to generate gradients from mini-batch training samples. These gradients provide the input for the feature extraction pipeline.

### 2. Gradient Feature Extraction

The system converts raw gradient tensors into structured numerical feature vectors.

The extracted statistical characteristics include:

- Mean and standard deviation.
- Variance and higher-order statistical moments.
- Minimum and maximum values.
- Norm-based characteristics.
- Sparsity and distribution-related statistics.
- Entropy and other aggregate properties.

The implementation extracts 19 statistical features from each of eight gradient arrays, along with three aggregate features, producing a **155-dimensional feature representation**.

### 3. Anomaly Detection

The extracted feature vectors are processed using the Isolation Forest algorithm.

Isolation Forest is an unsupervised anomaly detection technique that identifies observations that are significantly different from normal data patterns.

The detector learns the distribution of normal gradient submissions and assigns anomaly predictions and scores to incoming submissions.

An optional One-Class SVM approach is also considered for comparison.

### 4. Real-Time Monitoring Simulation

A monitoring component evaluates incoming client submissions using the trained anomaly detector.

Its responsibilities include:

- Scoring incoming gradient submissions.
- Identifying anomalous updates.
- Accepting or rejecting submissions.
- Simulating suspicious-client isolation.
- Maintaining monitoring logs.
- Generating detection reports.

### 5. Visualization and Analysis

An interactive Plotly dashboard is used to explore detection behavior and experimental results.

Additional visualizations support the analysis of model performance, anomaly distributions, and monitoring activity.

## Technology Stack

| Category | Technologies |
|---|---|
| Programming Language | Python |
| Deep Learning | PyTorch |
| Machine Learning | Scikit-learn |
| Numerical Computing | NumPy |
| Data Processing | Pandas |
| Visualization | Matplotlib, Plotly |
| Dataset | MNIST |
| Anomaly Detection | Isolation Forest, One-Class SVM |

## Repository Structure

```text
Detecting-GAN-Based-Data-Inversion/
│
├── data/
│   └── raw_gradients.pkl
│
├── logs/
│
├── models/
│
├── results/
│
├── visualizations/
│
├── detecting_GAN_based_data_inversion_in_CDL.ipynb
│
├── gan_detection_results.zip
│
├── Detecting_GAN_based_data_inversion_in_collaborative_deep_learning_Project.pdf
│
├── README.md
│
└── .gitattributes
```

*Note: The structure above highlights the main project artifacts. Some filenames may differ from the actual repository.*

## Getting Started

### Prerequisites

- Python 3.10 or later.
- Git.
- Git LFS.
- Jupyter Notebook or JupyterLab.

### 1. Clone the Repository

```bash
git clone https://github.com/Udaykaran-Singh/Detecting-GAN-Based-Data-Inversion-in-Collaborative-Deep-Learning.git

cd Detecting-GAN-Based-Data-Inversion-in-Collaborative-Deep-Learning
```

### 2. Download Large Files Using Git LFS

```bash
git lfs install
git lfs pull
```

### 3. Install Dependencies

```bash
pip install torch torchvision numpy pandas scikit-learn matplotlib plotly jupyter
```

### 4. Run the Project

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Open the project notebook and execute the cells sequentially.

## Experimental Evaluation

The prototype evaluates gradient anomaly detection using classification and anomaly-detection metrics.

The evaluation includes:

- Accuracy.
- Precision.
- Recall.
- F1-score.
- ROC-AUC.
- Confusion matrix.
- Anomaly score distributions.

The project also includes simulated client-monitoring experiments and visualization of detection decisions.

**Experimental scope:** Results obtained from the current implementation should be interpreted within its synthetic anomaly simulation setting. They do not establish effectiveness against genuine GAN-based inversion attacks in a production federated-learning environment.

## Current Limitations

The current implementation is a research prototype with the following limitations:

- Suspicious gradients are synthetically generated rather than produced by a fully implemented GAN-based inversion attack.
- The collaborative-learning workflow simulates client submissions rather than implementing a complete federated-learning server and aggregation protocol.
- Detection performance requires further validation using genuine gradient inversion attacks.
- Additional testing across independent clients, datasets, and attack scenarios is needed.

## Future Scope

Potential extensions include:

- Implementing a genuine GAN-based gradient inversion attack.
- Integrating a complete federated-learning architecture.
- Evaluating additional anomaly detection algorithms.
- Exploring advanced gradient representations and feature engineering.
- Testing on larger datasets such as CIFAR-10.
- Improving robustness against adaptive adversarial attacks.
- Evaluating computational overhead and real-time detection latency.

