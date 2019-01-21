# Prices

_Update 16 Jan 2019: implemented but not saved to a database_

Currently it calls the source(s) in real-time, but soon we will start caching the answers and do scheduled refreshes

## Default

Price data of a set of portfolio symbols (fromSymbols) in a chose currency / symbol (toSymbol), gathered through our price aggregation.

```shell
curl "http://localhost:4000/prices?toSymbol=ZAR&fromSymbols=BTC,USD,MSFT"
```

> The above command returns JSON structured like this:

```json
{
  "timestamp": "2019-01-01T00:00:01.001Z",
  "toSymbol": "ZAR",
  "fromSymbols": [
    {
      "fromSymbol":"BTC",
      "price":53676.86527106817,
      "source":"cryptocompare"
    },
    {
      "fromSymbol":"USD",
      "price":14.626298083954952,
      "source":"cryptocompare"
    },
    {
      "fromSymbol":"MSFT",
      "price":1535.9075617961096,
      "source":"alphavantage"
    }
  ],
  "errors": []
}
```

## Cryptocurrencies

Price data of a set of cryptocurrency symbols (fromSymbols) in a chosen currency symbol (toSymbol), gathered through our price aggregation.

```shell
curl "http://localhost:4000/prices/cryptocurrencies?toSymbol=ZAR&fromSymbols=BTC,ETH,XMR"
```

> The above command returns JSON structured like this:

```json
{
  "timestamp": "2019-01-01T00:00:01.001Z",
  "toSymbol": "ZAR",
  "fromSymbols": [
    {
      "fromSymbol": "BTC",
      "price": 53504.54788657036,
      "source": "cryptocompare"
    },
    {
      "fromSymbol":"ETH",
      "price":1841.2815319462345,
      "source":"cryptocompare"
    },
    {
      "fromSymbol":"XMR",
      "price":667.5567423230975,
      "source":"cryptocompare"
    }
  ],
  "errors": []
}
```

## Stocks

Price data of a set of stocks symbols (fromSymbols) in a chosen currency symbol (toSymbol), gathered through our price aggregation.

```shell
curl "http://localhost:4000/prices/stocks?toSymbol=ZAR&fromSymbols=MSFT,TWTR,VOD.JO"
```

> The above command returns JSON structured like this:

```json
{
  "timestamp": "2019-01-01T00:00:01.001Z",
  "toSymbol": "ZAR",
  "fromSymbols": [
    {
      "fromSymbol":"MSFT",
      "price":1532.7689388410452,
      "source":"alphavantage"
    },
    {
      "fromSymbol":"TWTR",
      "price":481.9734345351044,
      "source":"alphavantage"
    },
    {
      "fromSymbol":"VOD.JO",
      "price":13399.0000,
      "source":"alphavantage"
    }
  ],
  "errors": []
}
```

## Forex

Price data of a set of forex symbols (fromSymbols) in a chose currency / symbol (toSymbol), gathered through our price aggregation.

```shell
curl "http://localhost:4000/prices/forex?toSymbol=ZAR&fromSymbols=EUR,GBP,USD"
```

> The above command returns JSON structured like this:

```json
{
  "timestamp": "2019-01-01T00:00:01.001Z",
  "toSymbol": "ZAR",
  "fromSymbols": [
    {
      "fromSymbol":"EUR",
      "price":16.730801405387318,
      "source":"cryptocompare"
    },
    {
      "fromSymbol":"GBP",
      "price":18.85369532428356,
      "source":"cryptocompare"
    },
    {
      "fromSymbol":"USD",
      "price":14.63057790782736,
      "source":"cryptocompare"
    }
  ],
  "errors": []
}
```

