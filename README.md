````markdown
# ✈️ Airline Sentiment Analysis using BERT

A Natural Language Processing (NLP) project that uses a fine-tuned BERT (Bidirectional Encoder Representations from Transformers) model to classify airline-related tweets into three sentiment categories:

- 😠 Negative
- 😐 Neutral
- 😊 Positive

The project includes model training, evaluation, and an interactive Streamlit web application for real-time sentiment prediction.


## 📌 Project Overview

Airlines receive a large amount of feedback through social media platforms such as Twitter/X. Automatically identifying the sentiment of these messages can help organizations understand customer experiences and identify negative feedback.

This project fine-tunes the pretrained:

> `bert-base-uncased`

model for a 3-class sentiment classification task using airline-related tweets.

The trained model is then integrated into a simple Streamlit application where users can enter a tweet and receive:

- Predicted sentiment
- Prediction confidence
- Probability for each sentiment class


## 🧠 Model

### Base Model

BERT Base Uncased

```text
bert-base-uncased
````

BERT is a Transformer-based language representation model that uses bidirectional self-attention to understand contextual relationships between words.

### Classification Task

```text
Input Tweet
     │
     ▼
BERT Tokenizer
     │
     ▼
BERT Encoder
     │
     ▼
Classification Head
     │
     ▼
┌──────────┬─────────┬──────────┐
│ Negative │ Neutral │ Positive │
└──────────┴─────────┴──────────┘
```


## 📊 Dataset

The project uses the Twitter US Airline Sentiment Dataset, which contains airline-related tweets labeled according to their sentiment.

The three sentiment classes are:

| Label | Sentiment |
| ----: | --------- |
|     0 | Negative  |
|     1 | Neutral   |
|     2 | Positive  |

The dataset is divided into training and evaluation subsets.


## ⚙️ Data Preprocessing

The following preprocessing steps are performed:

1. Load the dataset using Pandas.
2. Select the tweet text and sentiment columns.
3. Encode sentiment labels using `LabelEncoder`.
4. Convert the data into a Hugging Face `Dataset`.
5. Split the dataset into training and evaluation sets.
6. Tokenize tweets using the BERT tokenizer.
7. Truncate/pad sequences to a maximum length of 128 tokens.


## 🏋️ Training

The model is fine-tuned using the Hugging Face Transformers `Trainer`.

### Main Training Parameters

| Parameter               |             Value |
| ----------------------- | ----------------: |
| Base Model              | BERT-base-uncased |
| Number of Classes       |                 3 |
| Learning Rate           |              2e-5 |
| Batch Size              |                16 |
| Evaluation Batch Size   |                16 |
| Epochs                  |                 3 |
| Weight Decay            |              0.01 |
| Maximum Sequence Length |               128 |
| Optimizer               |             AdamW |
| Evaluation Metric       |                F1 |
| Best Model Selection    |           Enabled |


## 📈 Results

The fine-tuned BERT model achieved approximately:

| Metric    |      Score |
| --------- | ---------: |
| Accuracy  | 84.95% |
| Precision | 84.90% |
| Recall    | 84.95% |
| F1 Score  | 84.92% |

### Confusion Matrix

```text
                 Predicted
              Neg   Neu   Pos

Actual Neg   1657   114    47
       Neu    127   426    60
       Pos     36    51   373
```

The model performs particularly well on negative sentiment, while neutral sentiment is comparatively more challenging to distinguish from the other classes.


## 🖥️ Streamlit Application

The project includes an interactive Streamlit interface.

Users can enter an airline-related tweet and receive the model's prediction.

### Application Features

 ✈️ Airline sentiment classification
 📝 Free-text tweet input
 🤖 Fine-tuned BERT inference
 📊 Prediction confidence
 📈 Sentiment probability distribution
 😠 Negative / 😐 Neutral / 😊 Positive classification

### Application Workflow

```text
User enters tweet
       │
       ▼
BERT Tokenizer
       │
       ▼
Fine-tuned BERT
       │
       ▼
Softmax probabilities
       │
       ▼
Predicted sentiment
       │
       ├── Negative
       ├── Neutral
       └── Positive
```


## 📂 Project Structure

```text
airline-sentiment-analysis/
│
├── train.ipynb
│
├── app.py
│
├── requirements.txt
│
├── airline_sentiment_bert/
    ├── config.json
    ├── model.safetensors
    ├── tokenizer_config.json
    ├── special_tokens_map.json
    ├── vocab.txt
    └── label_mapping.json
```


## 🛠️ Technologies Used

### Programming Language

 Python

### Machine Learning / NLP

 PyTorch
 
 Hugging Face Transformers
 
 Hugging Face Datasets
 
 Scikit-learn

### Data Processing

 Pandas
 
 NumPy

### Visualization / Evaluation

 Matplotlib
 
 Scikit-learn

### Deployment / UI

 Streamlit

### Development Environment

 Google Colab
 
 Google Drive

---

## 📦 Installation

Clone the repository:

```bash
git clone https://github.com/Ilhamlafeer/airline-sentiment-analysis.git
```

Navigate to the project:

```bash
cd airline-sentiment-analysis
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## 📋 Requirements

Create a `requirements.txt` file:

```text
torch

transformers

datasets

scikit-learn

pandas

numpy

streamlit

safetensors
```

---

## ▶️ Running the Streamlit Application

Make sure the trained model is available in:

```text
airline_sentiment_bert/
```

Then run:

```bash
streamlit run app.py
```

The application will be available at:

```text
http://localhost:8501
```

---

## 🧪 Example Predictions

### Example 1 — Positive

```text
The flight attendant was amazing and the service was excellent!
```

Expected sentiment:

```text
😊 Positive
```

### Example 2 — Negative

```text
My flight was delayed for hours and nobody helped me.
```

Expected sentiment:

```text
😠 Negative
```

### Example 3 — Neutral

```text
My flight from New York to Chicago is scheduled for 8 PM.
```

Expected sentiment:

```text
😐 Neutral
```

> The exact prediction depends on the fine-tuned model.

---

## 🔍 Evaluation

The model is evaluated using:

 Accuracy
 
 Precision
 
 Recall
 
 F1-score
 
 Confusion Matrix

The confusion matrix provides additional insight into which sentiment classes are being confused by the model.


## 💾 Model Saving

After training, the fine-tuned model and tokenizer are saved using Hugging Face's `save_pretrained()` mechanism.

Example:

```python
trainer.save_model(
    "./airline_sentiment_bert"
)

tokenizer.save_pretrained(
    "./airline_sentiment_bert"
)
```

## ☁️ Running in Google Colab

The model can also be trained and deployed from Google Colab.

Google Drive can be mounted to store the trained model:

```python
from google.colab import drive

drive.mount("/content/drive")
```

Streamlit can be launched from Colab:

```bash
!streamlit run app.py
```

A tunneling service can then be used to access the application through a browser.


## 📚 Learning Objectives

This project demonstrates practical implementation of:

 Natural Language Processing
 
 Transformer architectures
 
 BERT fine-tuning
 
 Text classification
 
 Tokenization
 
 Transfer learning
 
 Model evaluation
 
 Confusion matrix analysis
 
 Hugging Face Transformers
 
 PyTorch
 
 Streamlit deployment



## 🚀 Future Improvements

Possible extensions include:

 Hyperparameter optimization
 
 Data augmentation
 
 Handling class imbalance
 
 Comparing BERT with other Transformer models
 
 DistilBERT-based lightweight deployment
 
 Real-time Twitter/X data collection
 
 Explainable NLP predictions
 
 Sentiment trends by airline
 
 Airline-specific sentiment analysis
 
 Deployment using Docker and cloud services



## 👨‍💻 Author

Mohamed Ilham

AI/ML Engineer
