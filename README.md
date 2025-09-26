# Hybrid Phishing Email Detection System

A comprehensive system that protects against phishing by combining **traditional blacklist security** with **advanced Machine Learning (ML) analysis**. This hybrid approach ensures high accuracy against both known and unknown threats.

---

## Project Overview

This system uses a **Primary Defense (Blacklist)** for immediate threats, and a **Secondary Defense (ML Model)** as a fallback for unknown or suspicious emails.

### Key Detection Flow

1.  **Primary Defense:** Checks known blacklists for malicious URLs, attachments, and low sender reputation.
2.  **Secondary Defense (Fallback):** If the blacklist is inconclusive, the ML model analyzes patterns in the email.
3.  **Final Verdict:** Provides a single, confident decision on the email's safety.

---

## Key Features

### Layer 1: Blacklist Analysis
* **URL Reputation:** Real-time checking against the PhishTank API.
* **Attachment Scan:** VirusTotal integration for malware detection based on file hash.
* **Whitelisting:** Trusted domains are automatically bypassed for faster processing.

### Layer 2: Machine Learning Analysis
* **Random Forest Classifier:** Uses an ensemble learning model for robust prediction.
* **Feature Extraction:** Analyzes **Sender Patterns**, **Text Features** (TF-IDF on subject/body), and **URL Structure**.
* **Email Processing:** Handles both `.eml` files and multi-part formats (HTML/Plain Text).

---

## Installation & Running

Follow these steps to set up and run the detection system.

### 1. Setup

| Step | Command | Description |
| :--- | :--- | :--- |
| **Clone Repo** | `git clone <repository-url>` | Downloads the project to your local machine. |
| **Change Dir** | `cd CS-Phishing-Detection` | Moves into the project directory. |
| **Venv & Activate** | `python -m venv venv` <br> `venv/Scripts/activate` | Creates and activates your isolated Python environment. |
| **Install Deps** | `pip install -r requirements.txt` | Installs all necessary Python packages (Pandas, Scikit-learn, etc.). |

### 2. Configure API Keys

The system requires external API keys for its blacklist checks.

* Create a file named **`.env`** in the root directory.
* Add your **`VIRUSTOTAL_API_KEY`** (PhishTank API key is optional for basic checks).

### 3. Training and Detection

| Goal | Script to Run | Notes |
| :--- | :--- | :--- |
| **Train ML Model** | `run ml_training_script/ml_training.ipynb` | Required only if you need to retrain the model. Extract `CEAS_08.csv` from `archive.zip` first. |
| **Run Detection** | `run phishing_detection_script/phishing_detection.ipynb` | This executes the full hybrid analysis on emails in your `test_emails` directory. |

---

## System Performance Highlights

The system has been designed for maximum coverage and low false positives.

| Metric | Result | Benefit |
| :--- | :--- | :--- |
| **Overall Accuracy** | **98.0%** | High reliability on both known and unknown samples. |
| **ML Fallback Accuracy**| **97.2%** | Strong performance when blacklists are inconclusive. |
| **False Positive Rate** | **<3%** | Very few legitimate emails are incorrectly flagged. |
| **Recall (ML)** | **99.2%** | High success rate at catching actual phishing attempts. |

---

## Project Structure (Key Files)

| File / Folder | Purpose |
| :--- | :--- |
| `ml_training_script/` | Contains the **`ml_training.ipynb`** notebook to train and save the ML model (`.pkl` file). |
| `phishing_detection_script/` | Contains the **`phishing_detection.ipynb`** notebook, which is the main detection system. |
| `test_emails/` | Directory for placing sample `.eml` files to be analyzed. |
| `CEAS_08.csv` | The dataset used to train the machine learning model. |
| `phishing_email_model_fixed.pkl` | The pre-trained machine learning model file. |
| `.env` | **User-created** file to store private API keys. |