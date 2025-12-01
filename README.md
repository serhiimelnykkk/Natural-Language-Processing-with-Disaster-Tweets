# Natural Language Processing with Disaster Tweets

This repository contains a solution for the Kaggle competition: **[Natural Language Processing with Disaster Tweets](https://www.kaggle.com/competitions/natural-language-processing-with-disaster-tweets/overview)**.

The goal of this project is to build a Machine Learning model that predicts which Tweets are about real disasters and which ones are not, using Natural Language Processing (NLP) techniques and Deep Learning.

## 📌 Project Overview

Twitter has become an important communication channel in times of emergency. The ubiquitousness of smartphones enables people to announce an emergency they’re observing in real-time. Because of this, more agencies are interested in programmatically monitoring Twitter (i.e. disaster relief organizations and news agencies).

However, it is not always clear whether a person's words are actually announcing a disaster (e.g., "The sky is **ablaze**" could be a metaphor for a sunset, or a report of a forest fire).

## 📂 Dataset

The dataset is provided by Kaggle and consists of the following files:

*   **`train.csv`**: The training set. Contains the tweet text, keyword, location, and the `target` (1 = real disaster, 0 = not a disaster).
*   **`test.csv`**: The test set. Contains the tweet text. The model must predict the target for these rows.
*   **`sample_submission.csv`**: A sample submission file in the correct format.

### Data Fields
*   `id`: A unique identifier for each tweet.
*   `text`: The text of the tweet.
*   `location`: The location the tweet was sent from (may be blank).
*   `keyword`: A particular keyword from the tweet (may be blank).
*   `target`: The label (only in `train.csv`).

## 🛠 Technologies Used

*   **Python 3**
*   **Pandas & NumPy**: For data manipulation and analysis.
*   **Matplotlib & Seaborn**: For data visualization (EDA).
*   **TensorFlow / Keras**: For building and training the Deep Learning model.
*   **Regular Expressions (re)**: For text cleaning.

## ⚙️ Methodology

### 1. Exploratory Data Analysis (EDA)
*   Analyzed the distribution of the target variable (Disaster vs. Non-Disaster).
*   Inspected missing values in `keyword` and `location` columns.
*   Visualized example tweets from both classes.

### 2. Data Preprocessing
A custom `clean_text` function was implemented to clean the raw tweet text:
*   Removed URLs and HTML tags.
*   Removed user mentions (`@user`) and hashtags (`#`).
*   Removed numbers and special punctuation.
*   Converted text to lowercase.
*   Removed extra whitespace.

### 3. Tokenization and Padding
*   Used Keras `Tokenizer` to convert text into sequences of integers.
*   Vocabulary size set to 10,000 words.
*   Sequences were padded (`pad_sequences`) to a maximum length of 50 to ensure uniform input shape for the neural network.

### 4. Model Architecture
A Deep Learning model was built using **Keras Sequential API**:
1.  **Embedding Layer**: Transforms integers into dense vectors of fixed size.
2.  **Bidirectional LSTM (32 units)**: Captures patterns from both past and future context in the text.
3.  **Bidirectional LSTM (16 units)**: A second layer for deeper learning.
4.  **Dense Layer (ReLU)**: Fully connected layer for feature interpretation.
5.  **Dropout (0.5)**: To prevent overfitting.
6.  **Output Layer (Sigmoid)**: Outputs a probability between 0 and 1.

### 5. Training
*   **Optimizer**: Adam
*   **Loss Function**: Binary Crossentropy
*   **Callbacks**: EarlyStopping (monitors validation loss to prevent overfitting and restores best weights).
## 📊 Results

The model outputs a probability of a tweet being a real disaster. The predictions on the test set are saved to `submission.csv` in the following format:

```csv
id,target
0,0
2,1
3,1
...
