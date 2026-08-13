# 💬 Jenius App Sentiment Analysis

A **Natural Language Processing (NLP) and Deep Learning project** for analyzing user reviews of the **Jenius mobile banking application**.

This project aims to identify the sentiment expressed in user reviews and classify them into three categories:

* 😊 **Positive**
* 😐 **Neutral**
* 😞 **Negative**

The project covers the complete workflow, starting from **Google Play Store review scraping**, text preprocessing, exploratory analysis, sentiment labeling, text representation, deep learning model development, and model comparison.

Three deep learning architectures are implemented and compared:

* **Convolutional Neural Network (CNN)**
* **Long Short-Term Memory (LSTM)**
* **Gated Recurrent Unit (GRU)**

Among the three models, **LSTM achieved the highest test accuracy of 92.63%**.

---

## 🎯 Project Objectives

The main objectives of this project are:

1. Collect user reviews of the Jenius application from the Google Play Store.
2. Perform text preprocessing on Indonesian-language reviews.
3. Analyze the distribution and characteristics of user sentiments.
4. Build deep learning models for sentiment classification.
5. Compare CNN, LSTM, and GRU performance.
6. Identify the best-performing model for classifying Jenius application reviews.

---

## 💡 Business Problem

User reviews provide valuable information about customers' experiences with a digital banking application.

However, manually reading thousands of reviews is inefficient. Sentiment Analysis can help transform unstructured customer feedback into structured insights by automatically identifying whether a review expresses a positive, neutral, or negative sentiment.

This analysis can potentially help identify:

* User satisfaction levels.
* Common complaints.
* Frequently discussed features.
* Areas requiring improvement.
* Overall perception of the application.

---

# 🔄 Project Workflow

```text
Google Play Store
       │
       ▼
Review Scraping
       │
       ▼
Data Collection
       │
       ▼
Data Cleaning
       │
       ▼
Text Preprocessing
       │
       ├── Cleaning
       ├── Case Folding
       ├── Slang Normalization
       ├── Tokenization
       ├── Stopword Removal
       └── Stemming
       │
       ▼
Sentiment Labeling
       │
       ├── Positive
       ├── Neutral
       └── Negative
       │
       ▼
Exploratory Data Analysis
       │
       ├── Sentiment Distribution
       └── WordCloud
       │
       ▼
Text Tokenization
       │
       ▼
Word Embedding
       │
       ├───────────────┬───────────────┐
       ▼               ▼               ▼
      CNN             LSTM            GRU
       │               │               │
       └───────────────┴───────────────┘
                       │
                       ▼
               Model Evaluation
                       │
                       ▼
               Model Comparison
```

---

# 📥 Data Collection

The review dataset was collected from the **Google Play Store** using the `google-play-scraper` library.

The scraping process is implemented in:

```text
Scrapping_Data.ipynb
```

The resulting dataset is stored as:

```text
ulasan_jenius.csv
```

The collected data contains several attributes, including:

| Column                 | Description                                 |
| ---------------------- | ------------------------------------------- |
| `reviewId`             | Unique review identifier                    |
| `userName`             | Reviewer name                               |
| `userImage`            | Reviewer profile image                      |
| `content`              | User review text                            |
| `score`                | User rating                                 |
| `thumbsUpCount`        | Number of helpful votes                     |
| `reviewCreatedVersion` | Application version when review was created |
| `at`                   | Review timestamp                            |
| `replyContent`         | Developer response                          |
| `repliedAt`            | Developer response timestamp                |
| `appVersion`           | Application version                         |

The modeling process primarily uses the **review text (`content`)** and the resulting sentiment label.

---

# 🧹 Text Preprocessing

Text preprocessing is performed to transform raw user reviews into cleaner textual representations suitable for machine learning.

The preprocessing pipeline includes:

### 1. Missing Value Removal

Reviews without content are removed.

```python
clean_data = data.dropna(subset=['content'])
```

### 2. Duplicate Removal

Duplicate reviews are removed to reduce redundant observations.

```python
clean_data = clean_data.drop_duplicates()
```

These steps are explicitly implemented in the training notebook.

### 3. Text Cleaning

Unnecessary characters and noise are removed from the reviews.

### 4. Case Folding

All text is converted into lowercase.

### 5. Slang Word Normalization

Common informal Indonesian expressions are normalized into more standardized forms.

### 6. Tokenization

Reviews are split into individual words.

### 7. Stopword Removal

Common words that provide limited information for sentiment classification are removed.

### 8. Stemming

Words are transformed into their root forms using Indonesian-language stemming.

The notebook stores the results of these preprocessing stages in columns such as:

```text
text_clean
text_casefoldingText
text_slangwords
text_tokenizingText
text_stopword
text_akhir
```

---

# 🏷️ Sentiment Labeling

The processed reviews are assigned to three sentiment categories:

```text
Positive
Neutral
Negative
```

The resulting sentiment label is stored in:

```text
polarity
```

The project also calculates a numerical sentiment score:

```text
polarity_score
```

The resulting labels are subsequently used as the target variable for the deep learning models.

---

# 📊 Exploratory Data Analysis

Before model development, exploratory analysis is performed to understand the characteristics of the reviews.

### Sentiment Distribution

The number of reviews in each sentiment category is analyzed to understand the distribution of:

* Positive reviews
* Neutral reviews
* Negative reviews

### WordCloud

WordCloud visualizations are generated to identify frequently occurring words in the reviews.

The project generates WordCloud visualizations for different sentiment categories, including neutral reviews.

This helps provide an initial understanding of the topics and words frequently discussed by Jenius users.

---

# 🤖 Deep Learning Models

Three deep learning architectures are developed and compared.

## 1. CNN

The first model uses a **Convolutional Neural Network (CNN)** for text classification.

CNN can identify local patterns and combinations of words that may be useful for distinguishing sentiment.

The CNN model achieved:

| Metric         |     Result |
| -------------- | ---------: |
| Train Accuracy |     96.80% |
| Test Accuracy  | **90.33%** |

---

## 2. LSTM

The second model uses **Long Short-Term Memory (LSTM)**.

LSTM is designed to capture sequential dependencies in text and can retain relevant information across longer sequences.

The model uses tokenized text with a vocabulary limited to **2,000 features** and padded sequences as model input.

The LSTM achieved:

| Metric         |     Result |
| -------------- | ---------: |
| Train Accuracy |     95.82% |
| Test Accuracy  | **92.63%** |

LSTM achieved the highest test accuracy among the three models.

---

## 3. GRU

The third model uses **Gated Recurrent Unit (GRU)**.

GRU is another recurrent neural network architecture designed to capture sequential information while using a simpler gating mechanism than LSTM.

The GRU model achieved:

| Metric         |     Result |
| -------------- | ---------: |
| Train Accuracy |     96.84% |
| Test Accuracy  | **92.34%** |

---

# 📈 Model Comparison

The final model comparison is:

| Model    | Feature Type   | Train Accuracy | Test Accuracy |
| -------- | -------------- | -------------: | ------------: |
| **CNN**  | Word Embedding |         96.80% |        90.33% |
| **LSTM** | Word Embedding |         95.82% |    **92.63%** |
| **GRU**  | Word Embedding |         96.84% |        92.34% |

### 🏆 Best Model: LSTM

Based on test accuracy, **LSTM achieved the best performance with 92.63% accuracy**.

Although GRU obtained slightly higher training accuracy, LSTM performed better on the test set. This indicates that LSTM generalized slightly better to unseen reviews in this experiment.

---

# 🧠 Why Compare CNN, LSTM, and GRU?

The three architectures have different strengths:

| Model | Main Strength                                                |
| ----- | ------------------------------------------------------------ |
| CNN   | Captures local word patterns                                 |
| LSTM  | Captures long-term sequential dependencies                   |
| GRU   | Captures sequential dependencies with a simpler architecture |

Comparing multiple architectures allows the project to determine which model provides the best performance for this particular sentiment classification task.

---

# 🛠️ Technologies & Libraries

The project was developed primarily using **Python** and Google Colab.

### Programming Language

* Python

### Data Processing

* Pandas
* NumPy

### NLP

* NLTK
* Sastrawi
* `google-play-scraper`

### Visualization

* Matplotlib
* Seaborn
* WordCloud

### Machine Learning

* Scikit-learn

### Deep Learning

* TensorFlow
* Keras

The repository's environment includes TensorFlow, Keras, Scikit-learn, NLTK, Sastrawi, and other NLP/ML packages.

---

# 📁 Repository Structure

```text
SentimenAnalysis/
│
├── Notebook_Pelatihan_Model.ipynb
├── Scrapping_Data.ipynb
├── ulasan_jenius.csv
├── requirements.txt
└── README.md
```

### File Description

| File                             | Description                                                    |
| -------------------------------- | -------------------------------------------------------------- |
| `Scrapping_Data.ipynb`           | Notebook for collecting Jenius application reviews             |
| `Notebook_Pelatihan_Model.ipynb` | Complete preprocessing, EDA, modeling, and evaluation workflow |
| `ulasan_jenius.csv`              | Collected Jenius application review dataset                    |
| `requirements.txt`               | Python package dependencies                                    |
| `README.md`                      | Project documentation                                          |

---

# 🚀 How to Run

## 1. Clone Repository

```bash
git clone https://github.com/cloudyafilia/SentimenAnalysis.git
cd SentimenAnalysis
```

## 2. Install Dependencies

```bash
pip install -r requirements.txt
```

> **Note:** The current `requirements.txt` was generated from a Google Colab environment and contains a very large number of packages. For a cleaner reproducible setup, it would be better to create a smaller `requirements.txt` containing only the packages directly required by this project.

## 3. Run Data Scraping

Open:

```text
Scrapping_Data.ipynb
```

Run the notebook sequentially to collect the Jenius application reviews.

The scraping notebook uses `google-play-scraper`.

## 4. Run Model Training

Open:

```text
Notebook_Pelatihan_Model.ipynb
```

Run the notebook sequentially to reproduce:

```text
Data Preparation
       ↓
Text Preprocessing
       ↓
Exploratory Data Analysis
       ↓
Sentiment Labeling
       ↓
Tokenization
       ↓
Word Embedding
       ↓
CNN / LSTM / GRU
       ↓
Evaluation
       ↓
Model Comparison
```

The notebook was developed in **Google Colab** with GPU acceleration available in the original environment.

---

# 📌 Key Findings

The project demonstrates that deep learning can effectively classify sentiment in Indonesian-language reviews of a mobile banking application.

The main results are:

* **CNN:** 90.33% test accuracy
* **LSTM:** **92.63% test accuracy**
* **GRU:** 92.34% test accuracy

Among the evaluated models, **LSTM achieved the best test performance**.

The results suggest that modeling sequential relationships in user reviews can be useful for sentiment classification, with LSTM providing the strongest performance among the three tested architectures in this experiment.

---

# 💼 Potential Business Applications

The sentiment analysis pipeline can be extended into a customer feedback analytics system for financial applications.

Potential applications include:

* 📊 Monitoring customer satisfaction.
* 🔎 Identifying common user complaints.
* 📱 Evaluating user perception of application updates.
* 🛠️ Identifying features that require improvement.
* 📈 Monitoring sentiment trends across application versions.
* 💬 Automatically categorizing large volumes of customer reviews.

For example, sentiment could be analyzed by application version to identify whether a new release is associated with an increase in negative reviews.

---

# 🔮 Future Improvements

Several improvements could make this project more robust:

### 1. Improve Sentiment Labeling

Use manually validated labels or human annotation to improve the reliability of the sentiment ground truth.

### 2. Address Class Imbalance

If sentiment classes are imbalanced, techniques such as class weighting or resampling can be considered.

### 3. Hyperparameter Tuning

Optimize parameters such as:

* Embedding dimension
* Number of filters
* Kernel size
* Number of LSTM/GRU units
* Dropout rate
* Batch size
* Learning rate

### 4. Evaluate with More Metrics

In addition to accuracy, evaluate:

* Precision
* Recall
* F1-Score
* Confusion Matrix

This is especially useful when the sentiment classes are not perfectly balanced.

### 5. Compare with Traditional Machine Learning

Compare deep learning models with baseline approaches such as:

* Logistic Regression
* Naive Bayes
* Support Vector Machine
* Random Forest

### 6. Experiment with Transformer Models

Future versions could compare the current deep learning models with Indonesian-language transformer models such as IndoBERT.

### 7. Build an Interactive Dashboard

The final model could be deployed using **Streamlit** to create an interactive sentiment analysis application.

---

# 👩🏻‍💻 Author

**Cloudya Filia Putri**

Statistics Student | Data Analytics & Machine Learning Enthusiast

---

## 🔗 Repository

[GitHub Repository — Jenius Sentiment Analysis](https://github.com/cloudyafilia/SentimenAnalysis)

---

## 🏷️ Topics

`Python` `NLP` `Sentiment Analysis` `Indonesian NLP` `Deep Learning` `CNN` `LSTM` `GRU` `TensorFlow` `Keras` `Machine Learning` `Data Science` `Google Play Scraping`
