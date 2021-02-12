# Installation
Use the "Quick Start" installation from Github
https://github.com/freqtrade/freqtrade

# Setup:
https://www.freqtrade.io/

# Strategies
Are in "freqtrade/user_data/strategies" and can be searched on github e.g. <br>
https://github.com/search?q=freqtrade+strategy&type=repositories <br>
https://github.com/search?o=desc&q=freqtrade+strategy&s=committer-date&type=Commits

# Testrun

## Optional: Telegram Control Bot Fiverr

botname: fiverr <br>
username: <a href="https://t.me/fuenferbot">fuenferbot</a><br>
apitoken: 1529808070:AAHpfYQV1FObixx1Gy7MXtaVEvQM2LmU51E <br>
chat-id: 1569592805 <br>

        {
            "update_id": 756134048,
            "message": {
                "message_id": 565839,
                "from": {
                    "id": 1569592805,
                    "is_bot": false,
                    "first_name": "Canlann",
                    "username": "Canlann",
                    "language_code": "de"
                },
                "chat": {
                    "id": 1569592805,
                    "first_name": "Canlann",
                    "username": "Canlann",
                    "type": "private"
                },
                "date": 1611485114,
                "text": "/start",
                "entities": [
                    {
                        "offset": 0,
                        "length": 6,
                        "type": "bot_command"
                    }
                ]
            }
        }

## Run it with

        source .env/bin/activate

New (default) configuration can be created with 

        python3 ./freqtrade/main.py new-config

Start trading with:

        python3 ./freqtrade/main.py trade


# Working example: bittrex market
This example can be used by using the config-usdt.json and coping it into the main folder, renaming it to config.json.
When selecting currency pairs, you need to select a stake (e.g. USDT or BTC...). This stake has to be in every pair you select for trading. Each market has its own pairs.<br>
Look for currency pairs on <a href="https://www.cryptometer.io/list/bittrex">Bittrex pairs</a><br>
E.g.<br>

        "MKR/USDT",
        "DFI/USDT",
        "WICC/USDT",
        "AAVE/USDT",
        "LBC/USDT",
        "XWC/USDT",
        "ADA/USDT"

I selected the pairs the following way: I filtered the Monthly %Change (top, right corner). Calculate:

        avg = (highest_% + lowest_%) / 2

Then I selected the most common Bitcoin in this area. In this case it was USDT. This is my stake.

Create a configuration file for bittrex with USDT as stake currency: <br>

        python3 ./freqtrade/main.py new-config

Insert the selected pairs into the "config.json" file: <br>

        "pair_whitelist": [
            "MKR/USDT",
            "DFI/USDT",
            "WICC/USDT",
            "AAVE/USDT",
            "LBC/USDT",
            "XWC/USDT",
            "ADA/USDT"
        ],

Download historical data from 01.01.2020 until now: <br>

        python3 ./freqtrade/main.py download-data --timerange 20200101-

Search for strategies you want to apply on github and copy them into user_data/strategies. <br>

List and select strategies with: <br>

        python3 ./freqtrade/main.py list-strategies

Backtest with the data and different strategies: <br>

        python3 ./freqtrade/main.py backtesting --timerange 20200101-20210124 --timeframe 1m --strategy-list Strategy001 Strategy002 --export trades

        
Or with one strategy: <br>

        python3 ./freqtrade/main.py backtesting --timerange 20200101-20210124 --timeframe 1m -s Strategy001 --export trades

For help use: <br>

        python3 ./freqtrade/main.py backtesting -h

## Example backtesting with current setup

        python3 ./freqtrade/main.py backtesting --timerange 20200101-20210124 --timeframe 1m --strategy-list ADXMomentum ASDTSRockwellTrading AdxSmas AverageStrategy AwesomeMacd BbandRsi BinHV27 BinHV45 CCIStrategy CMCWinner ClucMay72018 CofiBitStrategy CombinedBinHAndCluc DoesNothingStrategy DoubleEMACrossoverWithTrend EMAPriceCrossoverWithTreshold EMASkipPump Freqtrade_backtest_validation_freqtrade1 InformativeSample Low_BB MACDCrossoverWithTrend MACDStrategy MACDStrategy_crossed Quickie RSIDirectionalWithTrend RSIDirectionalWithTrendSlow ReinforcedQuickie Scalp Simple SmoothOperator SmoothScalp Strategy001 Strategy002 Strategy003 Strategy004 Strategy005 TDSequentialStrategy strato --export trades



## Rinse and repeat
Don't forget to delete user_data/data before downloading new data

## Start the trading
Take the best strategy and go: <br>

        python3 ./freqtrade/main.py trade -s Strategy

## For optimal trading speed get a vserver near bittrex market
E.g. Bittrex.com is located near Chicago and/or San Fransisco<br>
vServer near Chicago for better latency available from https://www.chicagovps.net/kvm-vps <br>
