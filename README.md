# Reddit Political Sentiment Analysis

A data analysis pipeline that performs sentiment analysis on Reddit posts and comments from political subreddits during the 2016 U.S. election period.

## Overview

This project analyzes political discourse on Reddit by extracting posts and comments from politically-oriented subreddits, performing sentiment analysis using natural language processing, and identifying mentions of politicians and political policies. The pipeline combines VADER sentiment analysis with transformer-based models to generate nuanced sentiment scores.

## Features

- **Data Extraction**: PySpark-based extraction from large Reddit datasets
- **Sentiment Analysis**: Hybrid approach using VADER and DistilBERT for sentiment scoring
- **Politician Detection**: Identifies mentions of key political figures
- **Policy Analysis**: Detects and scores mentions of political policies with party-affiliation weighting
- **Multi-processing**: Efficient parallel processing for large-scale text analysis

## Tech Stack

- **Python 3.10+**
- **PySpark 3.5+** - Large-scale data processing
- **Pandas** - Data manipulation
- **NLTK** - Natural language processing and VADER sentiment
- **Transformers (Hugging Face)** - DistilBERT sentiment analysis
- **RapidFuzz** - Fuzzy string matching for policy detection

## Project Structure

```
├── spark_extract.py          # Reddit data extraction and filtering
├── create_features.py         # Sentiment feature generation pipeline
├── sentimentmodule.py         # Sentiment analysis functions
├── requirements.txt           # Python dependencies
└── README.md
```

## Installation

### 1. Create a virtual environment

```bash
cd path/to/your/project
python3 -m venv venv
```

### 2. Activate the virtual environment

```bash
source venv/bin/activate
```

You should see `(venv)` in your terminal prompt when activated.

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

## Usage

### Data Extraction

Extract and filter Reddit data from political subreddits:

```bash
spark-submit spark_extract.py
```

This will process Reddit submissions and comments from 20+ political subreddits during 2016.

### Sentiment Analysis

Generate sentiment scores for extracted data:

```bash
python create_features.py
```

The script will output a CSV file with sentiment scores for each post/comment.

## Methodology

### Sentiment Scoring

The project uses a hybrid sentiment analysis approach:

1. **VADER**: Provides baseline sentiment polarity scores
2. **DistilBERT**: Validates sentiment direction (positive/negative)
3. **Combined Score**: Merges both approaches for more accurate results

### Policy Detection

Uses fuzzy string matching and synonym expansion to detect mentions of:
- Democrat-aligned policies (e.g., healthcare reform, climate action)
- Republican-aligned policies (e.g., border security, tax cuts)

Sentiment scores are adjusted based on the sentiment expressed toward specific policies.

## Data Sources

The project analyzes data from political and election-related subreddits including:
- r/politics, r/Conservative, r/Liberal
- r/democrats, r/Republican
- r/PoliticalDiscussion, r/NeutralPolitics
- And 13+ more politically-oriented communities

## Requirements

See `requirements.txt` for full dependency list. Key requirements:
- pandas
- pyspark
- nltk
- transformers
- rapidfuzz