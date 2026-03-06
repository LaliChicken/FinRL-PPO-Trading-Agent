📈 FinRL Day Trading Bot - SPY
Authors: Yusuf Guler & Rahul Ghosh

Date: March 2026

A Reinforcement Learning (RL) day trading bot built with FinRL and Stable Baselines3. This agent uses a Proximal Policy Optimization (PPO) model to trade the SPY ETF, specifically optimized for navigating high-impact macroeconomic news events.

It features automated historical data extraction via the Alpaca API, advanced technical feature engineering (including VIX and Turbulence), and supports both historical backtesting and live market inference.

✨ Features
Reinforcement Learning Engine: Powered by Stable Baselines3's PPO algorithm.

Smart Data Pipeline: Custom chunked data downloader to bypass Alpaca API rate limits.

Advanced Feature Engineering: Feeds MACD, RSI, SMA, VIX (Fear Gauge), and market turbulence directly into the AI's state space.

Confidence Thresholding: Built-in signal filters to prevent the bot from over-trading during low-conviction, choppy market regimes.

Dual Execution Modes: Capable of running massive multi-year backtests or executing live market inference for real-time trade signals.

🛠️ Prerequisites
Python: 3.9+

Hardware: CUDA-enabled GPU highly recommended for training (e.g., RTX series or Cloud GPUs like H100/A100).

Brokerage: An active Alpaca account (Paper or Live) for API access.

📦 Installation
Due to version drift in the PyPI repository, FinRL must be installed directly from their master branch, and websockets must be manually upgraded to prevent yfinance crashes.

Run the following commands in your terminal or Colab environment:
Bash
Upgrade websockets to prevent yfinance streaming errors
pip install websockets>=13.0 --upgrade

Install FinRL directly from the master branch
pip install git+https://github.com/AI4Finance-Foundation/FinRL.git

Install remaining dependencies
pip uninstall -y alpaca-trade-api
pip install yfinance --upgrade --no-cache-dir
pip install stable-baselines3 alpaca-py stockstats exchange_calendars python-dotenv
🔐 Configuration (API Keys)
Never hardcode your API keys. The bot uses environment variables to keep your credentials secure.

For Local Environments (Arch Linux / VS Code):
Create a .env file in the root directory of the project:

Plaintext
ALPACA_API_KEY=your_api_key_here
ALPACA_API_SECRET=your_api_secret_here
For Google Colab:
Add your keys to the built-in Secrets tab (the key icon on the left sidebar) and name them API_KEY and API_SECRET. Grant notebook access when prompted.

🚀 Usage
Training and Backtesting
Run the standard pipeline to download historical data, engineer features, and train the PPO model. The bot will save the trained weights as ppo_spy_5m.zip and generate performance CSVs (holdout_account_value.csv, holdout_actions.csv, holdout_signals.csv).

If running headless via SSH, the script will output a performance graph as backtest_performance.png.

Live Inference
Once the model is trained (ppo_spy_5m.zip exists), you can run the live inference block. The bot will:

Ping Alpaca for the last 5 days of SPY data up to the current minute.

Calculate live technical indicators.

Feed the current state into the trained neural network.

Output a LONG, SHORT, or FLAT signal based on the AI's confidence threshold.

⚠️ Disclaimer 
For educational and research purposes only. This software is not financial advice. Algorithmic trading involves significant risk, and reinforcement learning models are highly susceptible to overfitting historical data. Always test extensively on Paper Trading accounts before committing real capital. The authors are not responsible for any financial losses incurred while using this software.
