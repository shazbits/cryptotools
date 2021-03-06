cryptotools [![Maintainability Rating](https://sonarcloud.io/api/project_badges/measure?project=shazbits_cryptotools&metric=sqale_rating)](https://sonarcloud.io/dashboard?id=shazbits_cryptotools)
===========

Crypto trading command line utilities.

Currently features:
* Volatility tool


## Volatility tool

Fetches historical data from binance and inspects the volatility of symbols by looking at how many times they hit highs and lows. Highs and lows are considered when the price goes over a threshold relative to the average price over the observed time period.

To determine the number of highs and lows during the time period, candlesticks are observed from oldest to newest, and each time the closing price is over a threshold, the number of hits is incremented by one. Each subsequent tick that is continuously above the threshold isn't counted as a hit. Another hit will be counted once the closing price falls back below the threshold and crosses it again after that. This is closer to an edge detection, not the time spent above thresholds.


## Usage

```
$ python volatility.py -s APPCBTC+MTHBTC+BNBBTC -i 1m -p "2 hour"
APPCBTC volatility information
------------------------------

Price: min: 0.000117, max 0.000123, avg: 0.000120, change: 4.60%

+THRESHOLD | HITS | -THRESHOLD | HITS
-------------------------------------
+    2.00% |    3 | -    2.00% |    1
+    1.00% |    2 | -    1.00% |    2
+    0.50% |    2 | -    0.50% |    1
+    0.25% |    3 | -    0.25% |    1

MTHBTC volatility information
-----------------------------

Price: min: 0.000027, max 0.000029, avg: 0.000028, change: 5.81%

+THRESHOLD | HITS | -THRESHOLD | HITS
-------------------------------------
+    2.00% |    6 | -    2.00% |    3
+    1.00% |    9 | -    1.00% |    4
+    0.50% |   10 | -    0.50% |    9
+    0.25% |   12 | -    0.25% |    7

BNBBTC volatility information
-----------------------------

Price: min: 0.001151, max 0.001159, avg: 0.001156, change: 0.70%

+THRESHOLD | HITS | -THRESHOLD | HITS
-------------------------------------
+    0.25% |    6 | -    0.25% |    1
```

## Binance credentials

You need to have an account on Binance, create a (read-only) API key, and enter it in the credentials.secret file (see credentials.secret.example).


## Dependencies

```
$ pip install python-binance
```


## MIT License

https://github.com/shazbits/cryptotools/blob/master/LICENSE

Romain Dura
