# Benchmarking Modern Tabular Deep Learning Algorithms for Multi-Class IoT Network Intrusion Detection

This repository contains the code, notebooks, and evaluation pipeline for a benchmark study of **ten modern tabular deep learning algorithms** applied to **multi-class IoT network intrusion detection**, using the **TON-IoT** dataset as the primary benchmark. Additional datasets are included for the dataset-selection phase and for a traditional machine learning prototype.

All experiments are designed to run in **Google Colab** with a **T4 GPU** runtime and use **Google Drive** for persistent storage of datasets and outputs.

---

## Table of Contents

1. [Overview](#overview)
2. [Requirements](#requirements)
3. [Datasets](#datasets)
4. [Download Options](#download-options)
5. [Runtime Requirements](#runtime-requirements)
6. [How to Run](#how-to-run)
7. [Notebooks](#notebooks)
8. [Reproducibility](#reproducibility)
9. [Troubleshooting](#troubleshooting)

---

## Overview

The goal of this project is to provide a rigorous, leakage-free evaluation of state-of-the-art tabular deep learning methods on IoT intrusion detection workloads. The main benchmark evaluates the following ten algorithms on the TON-IoT dataset:

- RealMLP
- TabM
- ExcelFormer
- AMFormer
- TabNSA
- xRFM
- GANDALF
- GRANDE
- DOFEN
- ModernNCA

A traditional machine learning prototype (Random Forest, Extra Trees, Histogram Gradient Boosting) is also included as a baseline on the ACI-IoT-2023 dataset, and three additional datasets (CICIoT2023, EdgeIIoTset, IoTID20) are used during the dataset-selection phase.

---

## Requirements

- **Google Colab** with **T4 GPU** runtime
- **Google Drive** (used for persistent storage of datasets and outputs)
- All required Python libraries are installed via `pip` at the top of each notebook

> **Important:** After running the pip installation cells, you **must restart the runtime** before continuing. This is also noted inside each notebook. Once restarted, select **Run All** to execute the full notebook.

---

## Datasets

The following datasets are used across the notebooks. Kaggle links are provided for reference.

| Dataset         | Used In                                 | Kaggle Link |
|-----------------|-----------------------------------------|-------------|
| **TON-IoT**      | Main benchmark (all 10 algorithms)      | [arnobbhowmik/ton-iot-network-dataset](https://www.kaggle.com/datasets/arnobbhowmik/ton-iot-network-dataset) |
| **CICIoT2023**   | Dataset selection phase                 | [himadri07/ciciot2023](https://www.kaggle.com/datasets/himadri07/ciciot2023) |
| **EdgeIIoTset**  | Dataset selection phase                 | [mohamedamineferrag/edgeiiotset-cyber-security-dataset-of-iot-iiot](https://www.kaggle.com/datasets/mohamedamineferrag/edgeiiotset-cyber-security-dataset-of-iot-iiot) |
| **IoTID20**      | Dataset selection phase                 | [rohulaminlabid/iotid20-dataset](https://www.kaggle.com/datasets/rohulaminlabid/iotid20-dataset) |
| **ACI-IoT-2023** | Traditional ML prototype                | [emilynack/aci-iot-network-traffic-dataset-2023](https://www.kaggle.com/datasets/emilynack/aci-iot-network-traffic-dataset-2023) |

---

## Download Options

### TON-IoT

The TON-IoT notebook includes a download option controlled by a flag at the top of the notebook, located in the **label distribution cell**:

```python
DO_DOWNLOAD = True   # Set to True to download the dataset for the first time
DO_DOWNLOAD = False  # Set to False to use the cached version from Google Drive
```

Set it to `True` on the first run and `False` on subsequent runs to avoid re-downloading.

### CICIoT2023, EdgeIIoTset, IoTID20, ACI-IoT-2023

These datasets are loaded **directly from Google Drive** and do **not** use the `DO_DOWNLOAD` flag. Ensure the dataset files are present in your Google Drive before running the corresponding notebooks.

---

## Runtime Requirements

All notebooks check for GPU availability at startup. If no GPU is detected, the notebook will raise an error and prompt you to switch to a T4 GPU runtime:

> **Runtime → Change runtime type → T4 GPU → Save**

All experiments were conducted on a **Tesla T4 GPU (15.6 GB VRAM)** via Google Colab.

---

## How to Run

1. Open the notebook in **Google Colab**.
2. Ensure the runtime is set to **T4 GPU**.
3. Run the **pip installation cells**.
4. **Restart the runtime** when prompted (also noted inside each notebook).
5. Select **Runtime → Run All** to execute the full notebook.
6. Outputs — including result CSV files and confusion matrix plots — are automatically saved to Google Drive.

---

## Notebooks

| Notebook | Description |
|---|---|
| `TraditionalML.ipynb` | Traditional ML prototype (Random Forest, Extra Trees, Histogram GB) |
| `RealMLPandTabM_TonIot.ipynb` | RealMLP and TabM on TON-IoT |
| `ExcelFormer_TONIoT.ipynb` | ExcelFormer |
| `AMFormer_TONIoT.ipynb` | AMFormer |
| `TabNSA_TONIoT.ipynb` | TabNSA |
| `xRFM_TONIoT.ipynb` | xRFM |
| `GANDALF_TONIoT.ipynb` | GANDALF |
| `GRANDE_TONIoT.ipynb` | GRANDE |
| `DOFEN_TONIoT.ipynb` | DOFEN |
| `ModernNCA_TONIoT.ipynb` | ModernNCA |
| `Model_Comparison.ipynb` | Loads all results and creates comparison table |
| `CICIoT2023_himadri_TabM_RealMLP.ipynb` | Dataset selection (CICIoT2023) |
| `TabMRealMLP_EDGE.ipynb` | Dataset selection (EdgeIIoTset) |
| `IoTID20_TabM_RealMLP_Classification.ipynb` | Dataset selection (IoTID20) |
| `ToN_IoT_Label_Distribution.ipynb` | Label distribution on TON-IoT |

> **Note:** On GitHub, if there are two files for the same algorithm, the files whose names include **`updated`** are the **final versions**. Please use these when reproducing results.

---

## Reproducibility

- A **fixed random seed of 42** is applied to all stochastic operations across every notebook to ensure full reproducibility.
- All preprocessing parameters — **median imputation** and **StandardScaler** — are fitted on the **training partition only** and applied to the validation and test sets, ensuring a **leakage-free evaluation pipeline**.

---

## Troubleshooting

### `DO_DOWNLOAD = False` raises a path or file-not-found error

In some cases, setting `DO_DOWNLOAD = False` may raise a path or file-not-found error even when the dataset has been previously downloaded. This behaviour is attributed to Google Colab clearing the session cache between runs or the Drive symlink becoming invalid.

**Fix:** Set `DO_DOWNLOAD = True` and re-execute the cell. This will re-download the dataset and reconstruct the required file path. Once the notebook completes successfully, the flag may be set back to `False` for subsequent runs to avoid unnecessary re-downloading.

---
