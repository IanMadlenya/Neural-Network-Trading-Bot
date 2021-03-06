# Neural Network Trading Bot
## About
C++ implementation of artificial neural network that analyzes BTC-e trade data to predict future 
prices and generate trades accord to those predictions. Uses python3 to executes trades output 
by the neural network on the BTC-e exchange. 


- trade_stream.py : Sends HTTP request to BTC-e public API every 2 seconds to gather recent trade data
- trading_floor.py : Checks output.sqlite for new records inserted by neural-network-predictor and executes orders to BTC-e if various criteria are met
- neural-network-predictor : Inserts records into output.sqlite containing the current price, predicted price, and type of trade to execute 

## neural-network-predictor configuration variables:
- main.cpp     eta_ : overall net training rate of the neural network [0.0...1.0]
- main.cpp     alpha_ : momentum multiplier [0.0...n]
- main.cpp     topology :  determines the topology of each layer of the neural network
- training.h   subset_length : determines the length of each array used by the neural network for training
- training.h   input_data_file_ : set this to be your local path to neural-net-trading-bot/data/input.sqlite
	- NOTE input.sqlite is generated by neural-net-trading-bot/pyTrader/trade_stream.py
- exchange.h..output_data_file_ : set this to be your local path to neural-net-trading-bot/data/output.sqlite
	- NOTE output.sqlite is generated by neural-net-trading-bot/neural-network-predictor

## Usage:
- trade_stream.py, trading_floor.py, and neural-network-predictor all must be run in separate terminal windows
- Execute programs in following order: trade_stream.py, trading_floor.py, neural-network-predictor
- neural-network-predictor will automatically proceed with execution when subset_length * 10 records are present in input.sqlite
- trade_stream.py will automatically proceed with execution once records are present in output.sqlite
