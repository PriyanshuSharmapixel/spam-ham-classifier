# SMS Spam Classifier

A text classification project that takes a message, cleans it, converts it to TF-IDF features, and predicts **Spam** or **Not Spam** in a Streamlit app. The repository includes the training notebook, dataset, and serialized vectorizer and model used by the app.

## Project snapshot

| Item | Detail |
| --- | --- |
| Task | Binary classification of SMS messages (`ham = 0`, `spam = 1`) |
| Dataset | `spam.csv`, with 5,572 rows before cleaning |
| After cleaning | 5,169 unique messages: 4,516 ham and 653 spam |
| Text representation | `TfidfVectorizer(max_features=3000)` |
| App model | `MultinomialNB`, saved as `model.pkl` |
| Interface | Streamlit text input and a Spam / Not Spam prediction |

The cleaned dataset has about **12.6% spam**. A model that predicts only ham would already be correct on about **87.4%** of those messages, so accuracy alone is not enough to assess spam detection.

## What I built

The notebook in [`sms-spam-detection(FINAL).ipynb`](sms-spam-detection%28FINAL%29.ipynb) covers:

1. **Cleaning:** retain the label and message columns, encode ham/spam as 0/1, and remove 403 duplicate rows.
2. **Exploration:** compare class counts, message length, word count, and sentence count; inspect frequent words in each class.
3. **Text preprocessing:** lowercase, tokenize, remove non-alphanumeric tokens and English stop words, then apply Porter stemming.
4. **Feature extraction:** convert processed messages into TF-IDF vectors with at most 3,000 features.
5. **Model experiments:** code for three Naive Bayes variants, additional classifiers, and voting and stacking ensembles, evaluated with accuracy and spam-class precision.
6. **App artifacts:** serialize the TF-IDF vectorizer and a fitted Multinomial Naive Bayes classifier for inference.

[`app.py`](app.py) applies the same text transformation, loads `vectorizer.pkl` and `model.pkl`, and displays the predicted label. Its interface accepts free text, but the training data in this repository consists of SMS messages; performance on full email messages has not been established.

## Results and evaluation status

| Measure | Value visible in the committed notebook |
| --- | ---: |
| Original messages | 5,572 |
| Duplicate rows removed | 403 |
| Unique messages used | 5,169 |
| Ham / spam | 4,516 / 653 |
| Test split configured in code | 20%, `random_state=2` |

**Model accuracy and precision are calculated in notebook code, but their printed outputs are not saved in the committed notebook.** The repository therefore does not currently provide a verifiable numerical model score. The UI demonstrates inference with the saved artifacts; it is not a substitute for a documented holdout evaluation.

There is also an evaluation limitation to address before reporting scores: the notebook fits TF-IDF on all cleaned messages **before** splitting train and test data. That allows the test messages to influence the vocabulary and IDF weights. For a reliable result, split the messages first and fit the vectorizer only on training data, ideally inside a scikit-learn `Pipeline`. Then report the confusion matrix, spam precision, spam recall, F1, and test-set class counts alongside accuracy.

## Run the app

```bash
git clone https://github.com/PriyanshuSharmapixel/spam-ham-classifier.git
cd spam-ham-classifier
python -m venv .venv
```

Activate the environment, install the app dependencies, and start Streamlit:

```bash
# macOS / Linux
source .venv/bin/activate

# Windows PowerShell: .venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
streamlit run app.py
```

The app downloads the NLTK resources `punkt`, `punkt_tab`, and `stopwords` at startup. An internet connection may be needed on the first run. Enter a message and select **Predict**. The app reads `model.pkl` and `vectorizer.pkl` from the current directory, so launch it from the repository root.

## Reproduce the notebook

The app's `requirements.txt` contains `streamlit`, `nltk`, and `scikit-learn`. To run **all notebook experiments and plots**, install the additional libraries used there, including `numpy`, `pandas`, `matplotlib`, `seaborn`, `wordcloud`, `xgboost`, and `jupyter`.

The notebook currently reads `spam.csv` from an absolute Windows path. Change that cell to:

```python
df = pd.read_csv("spam.csv", encoding="latin1")
```

Then run the notebook from the repository root. Its model cells do not contain saved scores, and the preprocessing order noted above should be fixed before publishing new performance claims.

## Repository files

| File | Purpose |
| --- | --- |
| [`app.py`](app.py) | Streamlit prediction interface and inference preprocessing |
| [`sms-spam-detection(FINAL).ipynb`](sms-spam-detection%28FINAL%29.ipynb) | Data cleaning, exploration, model experiments, and artifact export |
| [`spam.csv`](spam.csv) | SMS messages used by the notebook |
| `vectorizer.pkl`, `model.pkl` | Serialized TF-IDF vectorizer and Multinomial Naive Bayes model used by the app |
| [`requirements.txt`](requirements.txt), [`nltk.txt`](nltk.txt) | App dependencies and NLTK resource list |

## Next improvements

- Move the train/test split ahead of vectorizer fitting and save a reproducible evaluation report.
- Compare models using spam recall and precision as well as accuracy; document the false-positive / false-negative tradeoff.
- Pin compatible dependency versions and make the notebook use relative paths so the training workflow runs on a new machine.
- Add a few representative app examples and validate empty input before predicting.
