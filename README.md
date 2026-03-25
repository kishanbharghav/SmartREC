# SentimentRec – Smart Product Recommendation Engine

SentimentRec is a full-stack AI-powered product recommendation system. It merges standard Collaborative Filtering (predicting user ratings based on past actions) with NLP-based Sentiment Analysis (processing textual reviews) to surface items that are both statistically relevant AND genuinely well-loved.

## Tech Stack
* **UI**: Streamlit
* **ML/CF**: Surprise (SVD for collaborative filtering)
* **NLP**: HuggingFace Transformers (`distilbert-base-uncased-finetuned-sst-2-english`)
* **DB**: SQLite (Users, Products, Ratings, Reviews, Sentiment Scores)

## How It Works
1. Collaborative filtering generates top-N candidate products the user might like.
2. The NLP pipeline parses the product's community reviews mapping them to `POSITIVE` or `NEGATIVE` labels and a confidence score.
3. The Re-ranker combines the two vectors via an tunable `α` slider: `final = α * cf_score + (1-α) * sentiment_ratio`.
4. The user sees a carefully curated list. Very poorly reviewed items trigger a "Sentiment Warning".

## Setup Instructions

1. **Activate the virtual environment**:
   ```sh
   .\venv\Scripts\activate
   ```

2. **Seed the database and train the models**:
   *This initializes the database, creates synthetic data, trains the SVD model, and runs HuggingFace inference on the synthetic reviews (may take a few minutes).*
   ```sh
   python database/seed.py
   python models/cf_model.py
   python models/sentiment_model.py
   ```

3. **Run the Application**:
   ```sh
   streamlit run main.py
   ```

4. **Testing**:
   * Username: `testuser`
   * Password: `password123`
