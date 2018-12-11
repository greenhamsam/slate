# Prices

Price data of a set of assets / symbols (from_symbols) in a chose currency / symbol (to_symbol), gathered through our price aggregation.

Currently it calls the source(s) in real-time, but soon we will start caching the answers and do scheduled refreshes

```shell
curl "http://api.lettuce.money/prices?to_symbol=ZAR&from_symbols=BTC,USD,MSFT"
  -H "Authorization: mypersonalapikey"
```

> The above command returns JSON structured like this:

```json
{
  "timestamp": "2019-01-01T00:00:01.001Z",
  "toSymbol": "ZAR",
  "fromSymbols": [
    {
      "fromSymbol": "BTC",
      "lastUpdated": "2018-12-31T11:59:01.001Z",
      "price": 0.000021,
      "source": "Crypto Compare"
    },
    {
      "fromSymbol": "USD",
      "lastUpdated": "2018-12-31T11:58:01.001Z",
      "price": 0.070,
      "source": "Crypto Compare"
    },
    {
      "fromSymbol": "MSFT",
      "last_updated": "2018-12-31T11:57:01.001Z",
      "price": 1535.01,
      "source": "Alpha Vantage"
    },
  ]
}
```