# BERT Sentiment Analysis API

This project implements a sentiment analysis API using BERT (Bidirectional Encoder Representations from Transformers) and FastAPI. It classifies text into three sentiment categories: negative, neutral, and positive.

## Features

- Sentiment analysis using a fine-tuned BERT model
- FastAPI for serving predictions
- Easy-to-use REST API

## Requirements

- Python 3.8
- Conda (for managing the virtual environment)
- Pipenv (for managing dependencies)

## Installation

1. Clone this repository:
   ```
   git clone https://github.com/your-username/bert-sentiment-api.git
   cd bert-sentiment-api
   ```

2. Create a conda environment:
   ```
   conda create -n bert-sentiment-api python=3.8
   conda activate bert-sentiment-api
   ```

3. Install Pipenv:
   ```
   pip install pipenv
   ```

4. Install the project dependencies using Pipenv:
   ```
   pipenv install
   ```

5. Install development dependencies (optional):
   ```
   pipenv install --dev
   ```

6. Download the pre-trained model:
   ```
   python bin/download_model.py
   ```
   This script will download the pre-trained model and save it in the `assets` folder.

## Usage

1. Activate the conda environment:
   ```
   conda activate bert-sentiment-api
   ```

2. Start the FastAPI server:
   ```
   pipenv run uvicorn sentiment_analyzer.api:app --reload
   ```

3. The API will be available at `http://127.0.0.1:8000`. You can use the `/predict` endpoint to get sentiment predictions:

   ```bash
   curl -X 'POST' \
     'http://127.0.0.1:8000/predict' \
     -H 'accept: application/json' \
     -H 'Content-Type: application/json' \
     -d '{
     "text": "Decent Phone. Working like a charm"
   }'
   ```

4. The API will return a JSON response with the predicted sentiment, confidence score, and probabilities for each class.

## Project Structure

- `sentiment_analyzer/`
  - `api.py`: FastAPI application and endpoint definitions
  - `classifier/`
    - `model.py`: BERT model wrapper for sentiment analysis
    - `sentiment_classifier.py`: PyTorch module for the sentiment classifier
- `bin/`
  - `download_model.py`: Script to download the pre-trained model
- `assets/`
  - `model_state_dict.bin`: Pre-trained model file (downloaded by `download_model.py`)
- `config.json`: Configuration file for the model and classes
- `.flake8`: Flake8 configuration
- `.isort.cfg`: isort configuration
- `Pipfile`: Pipenv dependencies file

## Development

This project uses `black` for code formatting, `isort` for import sorting, and `flake8` for linting. To set up the development environment:

1. Install development dependencies:
   ```
   pipenv install --dev
   ```

2. Run linting and formatting:
   ```
   pipenv run black .
   pipenv run isort .
   pipenv run flake8 .