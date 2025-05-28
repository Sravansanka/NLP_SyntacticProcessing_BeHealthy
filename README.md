
# 🩺 BeHealthy: Disease-Treatment Mapping using Custom NER

## 🧾 Overview

This project builds a custom Named Entity Recognition (NER) system for extracting **diseases** and their corresponding **treatments** from unstructured medical text. It simulates a use case for a hypothetical health tech platform called **BeHealthy**, which aims to organize and interpret doctor-patient interaction data to enhance care delivery.

---

## 📦 Dataset Details

You are provided with the following datasets:

| File Name        | Description                              |
|------------------|------------------------------------------|
| `train_sent`     | Tokenized words (train set)              |
| `train_label`    | Word-level labels: O (Other), D (Disease), T (Treatment) |
| `test_sent`      | Tokenized words (test set)               |
| `test_label`     | Labels for test set words                |

> Each blank line separates sentences. Label files follow one-to-one mapping with sentence files.

---

## 📌 Objective

To extract disease-treatment pairs using a Conditional Random Field (CRF) model and return a dictionary such as:

```python
{
    "cancer": ["chemotherapy", "radiation therapy"],
    "asthma": ["albuterol"]
}
```

---

## 🧩 Step-by-Step Tasks

### 1. Data Preprocessing
- Combine token-level data into full sentences (train and test sets).
- Reconstruct label sequences aligned with tokens.
- Validate:
  - ✅ Correct sentence reconstruction
  - ✅ Total number of sentences and label lines match

### 2. Concept Identification
- Merge both datasets (train + test) for exploratory analysis.
- Use spaCy for POS tagging.
- Extract top 25 frequently occurring **NOUN/PROPN** words as key concepts.

### 3. Define CRF Features
- Feature set includes:
  - Word itself
  - POS tag
  - Lowercase form
  - Prefixes/suffixes
  - Previous word features
  - Start/end of sentence markers

### 4. Extract Sentence Features & Labels
- Apply feature generation to each sentence.
- Extract aligned labels from processed label files.

### 5. Define Model Inputs
- `X_train`, `X_test`: Sentence-wise feature dictionaries
- `y_train`, `y_test`: Corresponding label sequences

### 6. Build CRF Model
- Use `sklearn-crfsuite`
- Train on training data
- Apply appropriate regularization and training parameters

### 7. Evaluate Model
- Predict labels on `X_test`
- Calculate F1-score and generate classification report
- Inspect predicted vs actual labels

### 8. Disease-Treatment Mapping
- For every sentence in test data:
  - If a `D` (disease) and `T` (treatment) are present, map them
- Create dictionary: `{ disease: [list of treatments] }`
- Predict treatment(s) for: **"hereditary retinoblastoma"**

---

## 🧪 Dependencies

```bash
pip install scikit-learn
pip install sklearn-crfsuite
pip install nltk
pip install pandas
pip install spacy
python -m spacy download en_core_web_sm
```

---

## ▶️ Running the Notebook

1. Open the notebook:
   ```bash
   jupyter notebook Sravana_Sanka_Syntactic_Processing_BeHealthy.ipynb
   ```
2. Run all cells in order.
3. Outputs:
   - Top concepts list
   - Evaluation metrics
   - Extracted disease-treatment dictionary

---

## 💡 Notes & Assumptions

- Each sentence is considered independently.
- If both disease and treatment appear in a sentence, they are mapped.
- Treatments can apply to multiple diseases.
- Only noun-related tokens are used to identify concepts.

---

## 📄 License

This is a capstone NLP assignment provided as part of the upGrad AI/ML learning module.

---


## 🔍 Suggested Treatment Plan
────────────────────────────
🦠 Disease: **Hereditary Retinoblastoma**

💊 Recommended Treatments:
  1. Radiotherapy

✅ Please consult a medical professional before proceeding with any treatment.

## ✍️ Author
**Sravana Sanka**
