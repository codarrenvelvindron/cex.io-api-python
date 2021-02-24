cex.io-api-python
=================

CEX.IO API integration. Python sources.

This is a cex.io api client that works out of the box.

Original Author: https://github.com/matveyco/cex.io-api-python

Forked and modifiedby Codarren Velvindron: https://github.com/codarrenvelvindron/cex.io-api-python

## History
- The original project was last active on in 2014.
- There was a lot of functions missing so I had to add them (Maybe they didn't exist at the time)
- It was written in python 2.7.
- I added compatibility for python3. (It actually only works on python3 now)
- Added all changes to CHANGES.txt
- Trying to add more functions and make it an active project

## Introduction

1. Download lib

2. Get API key and API secret on https://cex.io/trade/profile

## How to use?

### 1. Create your python project

### 2. Add "import cexapi"

### 3. Create class 
```python
  api = cexapi.Api(username,api_key,api_secret)
```
username - your username on cex.io
api_key - your API key
api_secret - your API secret code

### 4. Methods and parameters:

#### a) API method parametrs
```
1. couple = ("GHS\BTC" | "BF1\BTC") currency pair
2. since = integer  return trades with tid >= since
3. order_id = integer 
4. ptype = ("sell" | "buy") type of order
5. amount = float 
6. price = float
```
      
#### b) API methods
```
1. ticker(couple = 'GHS/BTC') - get ticker
2. tickers(couple = 'USD') - get ALL tickers to currency
3. order_book(couple = 'GHS/BTC') - get order
4. trade_history(since = 1, couple = 'GHS/BTC') -  get all order
5. balance() - get your balance
6. current_orders(couple = 'GHS/BTC') - get open order
7. cancel_order(order_id) - cancel order №order_id
8. place_order(ptype = 'buy', amount = 1, price = 1, couple = 'GHS/BTC') - create order
9. archived_orders(couple = 'XLM/USD') - get all transactions done for pair
```
     
#### c) Full API documentation: https://cex.io/rest-api
    
### 5. Examples

#### Connect and get balance:
```python
import cexapi
api = cexapi.Api(username, api_key, api_secret)
print api.balance()
```

```
{'timestamp': '1383378763', 'BTC': {'available': '0.04722110', 'orders': '0.00170000'}, 'GHS': {'available': '0.01000000'} }
```

#### Get balance:
```python
print api.balance()
```

```
{'timestamp': '1383379054', 'BTC': {'available': '0.04614310', 'orders': '0.00170000'}, 'GHS': {'available': '0.02000000'}}
```

#### Get API ticker:
```python
print api.ticker('GHS/BTC')
```
```
{'volume': '7154.78339022', 'last': '0.1078', 'timestamp': '1383379041', 'bid': '0.10778', 'high': '0.10799999', 'low': '0.10670076', 'ask': '0.10780000000000001'}
```

#### Get order book:
```python
print api.order_book('BF1/BTC')
```

```
{'timestamp': '1383378967', 'bids': [['1.7', '0.30100000'], ['1.67', '0.00011000'], ['0.8', '0.02070000'], ['0.1002', '0.27748002'], ['0.1', '0.10000000'], ['0.011', '0.30500000'], ['0.009', '1.00000000'], ['0.00171', '0.00100000'], ['0.0012', '1.00000000'], ['0.00116819', '0.50000000'], ['0.001002', '33.00000000'], ['0.001001', '53.00000000'], ['0.001', '3.00000000'], ['0.00097626', '36.00000000'], ['0.0006', '85.00000000'], ['0.00058409', '0.50000000'], ['0.0004889', '0.06823960'], ['0.0003', '1.00000000'], ['0.00029204', '0.90000000'], ['0.0001', '101.00000000']], 'asks': []}
```

#### Get your current active orders:
```python
print api.current_orders('BF1/BTC')
```

```
[{'price': '1.7', 'amount': '0.00100000', 'time': '1383378514737', 'type': 'buy', 'id': '6219104', 'pending': '0.00100000'}]
```

#### Place new order:
```python
print api.place_order('buy', 0.001, 1.7, 'BF1/BTC')
```
```
{'price': '1.7', 'amount': '0.00100000', 'time': 1383378987622, 'type': 'buy', 'id': '6219145', 'pending': '0.00100000'}
```

#### Place another order (GHS/BTC):
```python
print api.place_order('buy', 0.01, 0.10789, 'GHS/BTC')
```
```
{'price': '0.10789', 'amount': '0.01000000', 'time': 1383379024072, 'type': 'buy', 'id': '6219150', 'pending': '0.00000000'}
```

#### Cancel order:
```python
print api.cancel_order(6219145)
```
```
True
```

