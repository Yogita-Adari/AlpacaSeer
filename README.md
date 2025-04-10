# AlpacaSeer
A machine learning model that analyzes real-time market data from Alpaca API to predict stock market trends.
## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Technical Details](#technical-details)
- [Configuration](#configuration)
- [Results and Visualization](#results-and-visualization)
- [Paper Trading vs. Live Trading](#paper-trading-vs-live-trading)
- [Limitations](#limitations)
- [Future Improvements](#future-improvements)
- [Contributing](#contributing)
- [License](#license)

## Overview

MarketPulse is a Python-based machine learning project that uses the Alpaca API to fetch real-time and historical stock market data, process it with various technical indicators, and make predictions about future price movements. The project is designed to run in Google Colab, making it accessible without the need for local setup or configuration.

## Features

- **Real-time Data Integration**: Connects to Alpaca API for live market data
- **Technical Analysis**: Calculates key indicators like Moving Averages, MACD, RSI
- **Machine Learning Models**: Uses Random Forest to predict market direction
- **Backtesting**: Tests prediction accuracy against historical data
- **Visualization**: Displays buy/sell signals and model performance
- **Paper Trading Mode**: Test strategies without risking real money

## Prerequisites

- Google account (for Google Colab)
- Alpaca account with API keys
- Basic understanding of Python and machine learning concepts

## Installation

This project is designed to run in Google Colab, so there's no local installation required.

1. Open the notebook in Google Colab
2. Run the first cell to install required packages:
   ```python
   !pip install alpaca-trade-api pandas numpy scikit-learn matplotlib
   ```

## Usage

1. **API Setup**:
   - Create an Alpaca account at [app.alpaca.markets](https://app.alpaca.markets)
   - Enable 2FA for your account (required for API access)
   - Generate API keys from the dashboard
   - Add your API keys to the notebook:
     ```python
     API_KEY = "YOUR_API_KEY" 
     SECRET_KEY = "YOUR_SECRET_KEY"
     BASE_URL = "https://paper-api.alpaca.markets"
     ```

2. **Data Collection**:
   ```python
   symbols = ['AAPL', 'MSFT', 'AMZN', 'GOOGL', 'TSLA']
   data_dict = get_historical_data(symbols, timeframe='1D')
   ```

3. **Train Model**:
   ```python
   features = ['return', 'range', 'daily_volatility', 
              'ma_5', 'ma_10', 'ma_20', 'ma_50', 'ma_200',
              'macd', 'macd_hist', 'rsi']
   model, X_test, y_test = train_model(data_dict['AAPL'], features)
   ```

4. **Make Predictions**:
   ```python
   predictions = predict_market_direction(model, symbols, features)
   print(predictions)
   ```

## Project Structure

- **Data Collection**: `get_historical_data()` function fetches and processes market data
- **Feature Engineering**: Technical indicators calculated from raw price data
- **Model Training**: `train_model()` function creates and evaluates the predictive model
- **Prediction**: `predict_market_direction()` generates forecasts for selected symbols
- **Visualization**: Plotting functions display model signals and performance

## Technical Details

- **Technical Indicators**: 
  - Moving Averages (5, 10, 20, 50, 200 day)
  - MACD (Moving Average Convergence Divergence)
  - RSI (Relative Strength Index)
  - Volatility metrics
  
- **Machine Learning Model**:
  - Random Forest Classifier
  - Binary classification (price up or down)
  - Feature importance analysis
  - Performance metrics (accuracy, precision, recall)

## Configuration

You can customize the model by modifying:

- **Symbols**: Change the list of stocks to analyze
- **Timeframe**: Adjust data granularity ('1D', '1H', '15Min', etc.)
- **Features**: Add or remove technical indicators
- **Model Parameters**: Tune the Random Forest hyperparameters
- **Date Range**: Set the historical data period for training

## Results and Visualization

The notebook generates:

1. **Model Performance Metrics**:
   - Accuracy score
   - Classification report (precision, recall, F1-score)
   - Feature importance ranking

2. **Visual Analysis**:
   - Price chart with buy/sell signals
   - Correct and incorrect predictions highlighted
   - Performance comparison with baseline strategies

## Paper Trading vs. Live Trading

The project uses Alpaca's paper trading environment by default:
```python
BASE_URL = "https://paper-api.alpaca.markets"
```

For live trading (use with caution):
```python
BASE_URL = "https://api.alpaca.markets"
```

## Limitations

- Market prediction is inherently difficult and uncertain
- The model does not account for fundamental factors or news events
- Performance may vary across different market conditions
- Past performance does not guarantee future results

## Future Improvements

- Add sentiment analysis from news and social media
- Implement more advanced models (LSTM, Transformer)
- Include portfolio optimization strategies
- Add risk management features
- Expand to other asset classes (options, crypto)

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
