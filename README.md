# SentimentAnalysisForFlipKart

A Flask web app that scrapes product reviews from a Flipkart product page, runs sentiment analysis on them, and visualizes the results — comparing the sentiment-predicted star rating against the actual user-given rating.

## How It Works

1. **Scraping** — Given a Flipkart product URL, the app uses [Playwright](https://playwright.dev/python/) to launch a headless Chromium browser, paginate through the review pages, and extract:
   - Product name
   - Average product rating
   - Per-review user star rating, title, and review text
2. **Sentiment Analysis** — Each review's text is scored using NLTK's VADER (`SentimentIntensityAnalyzer`), producing a compound sentiment score that is mapped to a predicted 1–5 star rating.
3. **Evaluation** — The predicted ratings are compared against the actual user ratings to compute an accuracy score and a confusion matrix.
4. **Visualization** — The app renders:
   - Pie charts of actual vs. predicted rating distribution
   - Histograms of actual vs. predicted ratings
   - A confusion matrix heatmap
   - Word clouds for negative, neutral, and positive reviews

## Tech Stack

- **Flask** — web framework / routing
- **Playwright** — headless browser scraping of Flipkart review pages
- **pandas** — data handling
- **NLTK (VADER)** — sentiment scoring
- **scikit-learn** — accuracy score and confusion matrix
- **Plotly** — interactive pie charts, histograms, and heatmap
- **WordCloud + Matplotlib** — word cloud image generation

## Project Structure

```
.
├── app.py                  # Flask app: scraping, sentiment analysis, routes
├── flipkart_reviews.csv    # Sample/output CSV of scraped reviews
├── templates/               # HTML templates (index & analysis pages)
├── static/                  # Generated word cloud images
└── .idea/                   # IDE project files
```

## Getting Started

### Prerequisites

- Python 3.8+
- pip

### Installation

```bash
git clone https://github.com/Flipkart-Sentiment-Analysis/SentimentAnalysisForFlipKart.git
cd SentimentAnalysisForFlipKart

pip install flask playwright pandas nltk scikit-learn plotly wordcloud matplotlib
playwright install chromium
```

The app also downloads the NLTK VADER lexicon automatically on first run (`nltk.download('vader_lexicon')`).

### Running the App

```bash
python app.py
```

By default, Flask runs in debug mode on `http://127.0.0.1:5000/`.

### Usage

1. Open the app in your browser.
2. Paste a Flipkart product page URL into the form.
3. Submit — the app scrapes all available reviews for that product, analyzes sentiment, and displays:
   - Actual vs. predicted rating distributions
   - A confusion matrix
   - Word clouds for negative, average, and positive reviews
   - Overall prediction accuracy

## Notes

- Scraping relies on Flipkart's current page structure (CSS class selectors). If Flipkart changes its front-end markup, the scraper's selectors in `scrape_flipkart_reviews()` may need to be updated.
- Scraped reviews are also saved locally to `flipkart_reviews.csv`.
- Generated word cloud images are saved to the `static/` folder as `neg_wc.png`, `avg_wc.png`, and `pos_wc.png`.

## Disclaimer

This project is intended for educational/research purposes. Please review Flipkart's terms of service before scraping data from the site.
