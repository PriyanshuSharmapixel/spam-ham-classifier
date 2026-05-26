# spam-ham-classifier

> Streamlit application for classifying email and SMS spam using machine learning.

![GitHub stars](https://img.shields.io/github/stars/PriyanshuSharmapixel/spam-ham-classifier?style=for-the-badge&logo=github) ![GitHub forks](https://img.shields.io/github/forks/PriyanshuSharmapixel/spam-ham-classifier?style=for-the-badge&logo=github) ![GitHub issues](https://img.shields.io/github/issues/PriyanshuSharmapixel/spam-ham-classifier?style=for-the-badge&logo=github) ![Last commit](https://img.shields.io/github/last-commit/PriyanshuSharmapixel/spam-ham-classifier?style=for-the-badge&logo=github) ![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)

## 📑 Table of Contents

- [Description](#description)
- [Key Features](#key-features)
- [Use Cases](#use-cases)
- [Tech Stack](#tech-stack)
- [Quick Start](#quick-start)
- [Key Dependencies](#key-dependencies)
- [Project Structure](#project-structure)
- [Development Setup](#development-setup)
- [Contributing](#contributing)

## 📝 Description

spam-ham-classifier is a Python-based machine learning project designed to identify and filter SMS and email spam. By utilizing pre-trained classification models, the project addresses the challenge of identifying unsolicited or malicious messages. It packages both the model training methodology and an interactive application deployment into a single, accessible repository.

## ✨ Key Features

- **🎈 Streamlit Interactive UI** — Provides an interactive web interface using Streamlit to allow users to input text and view classification results in real-time.
- **✂️ NLTK Preprocessing Pipeline** — Cleans text inputs by tokenizing, removing stop words and punctuation, and applying Porter Stemming via the NLTK library.
- **📦 Serialized Model Deployment** — Loads a pre-trained vectorizer and classification model directly from pickled file inputs to process and predict input messages.
- **📓 Model Exploration Notebook** — Includes a comprehensive Jupyter Notebook detailing the data preparation, model comparison, and training workflows.

## 🎯 Use Cases

- Interactively testing and classifying suspicious SMS or email texts using a web interface.
- Demonstrating a complete machine learning pipeline from NLTK-based text preprocessing to model inference.
- Serving as a reference template for deploying pickled scikit-learn or similar classification models via Streamlit.

## 🛠️ Tech Stack

- 🐍 **Python**

## ⚡ Quick Start

```bash

# 1. Clone the repository
git clone https://github.com/PriyanshuSharmapixel/spam-ham-classifier/tree/main.git

# 2. Create & activate a virtualenv
python -m venv venv && source venv/bin/activate

# 3. Install dependencies
pip install -r requirements.txt
```

## 📦 Key Dependencies

```
streamlit: latest
nltk: latest
```

## 📁 Project Structure

```
.
├── app.py
├── model.pkl
├── requirements.txt
├── sms-spam-detection(FINAL).ipynb
└── vectorizer.pkl
```

## 🛠️ Development Setup

### Python
1. Install Python (v3.10+ recommended)
2. `python -m venv venv && source venv/bin/activate`  (Windows: `venv\Scripts\activate`)
3. `pip install -r requirements.txt`

## 👥 Contributing

Contributions are welcome! Here's the standard flow:

1. **Fork** the repository
2. **Clone** your fork: `git clone https://github.com/PriyanshuSharmapixel/spam-ham-classifier/tree/main.git`
3. **Branch**: `git checkout -b feature/your-feature`
4. **Commit**: `git commit -m 'feat: add some feature'`
5. **Push**: `git push origin feature/your-feature`
6. **Open** a pull request

Please follow the existing code style and include tests for new behavior where applicable.

---
*This README was generated with ❤️ by [ReadmeBuddy](https://readmebuddy.com)*
