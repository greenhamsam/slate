# Prices

_Update 16 Jan 2019: implemented but not saved to a database_

Currently it calls the source(s) in real-time, but soon we will start caching the answers and do scheduled refreshes

Price data of a single or set of symbols (fromSymbols) in a chose currency / symbol (toSymbol), gathered through our price aggregation.

```shell
curl "http://localhost:4000/prices?toSymbol=ZAR.NONE.CC&fromSymbols=BTC.NONE.CC,USD.NONE.CC,MSFT.NYSE.EOD"
```

> The above command returns JSON structured like this:

```json
{
  "timestamp": "2019-01-01T00:00:01.001Z",
  "toSymbol": "ZAR",
  "fromSymbols": [
    {
      "fromSymbol": "BTC",
      "price": 53676.86527106817,
      "source": "cryptocompare",
      "lastUpdated": "2019-01-01T00:00:02.001Z"
    },
    {
      "fromSymbol": "USD",
      "price": 14.626298083954952,
      "source": "cryptocompare",
      "lastUpdated": "2019-01-01T00:00:02.001Z"
    },
    {
      "fromSymbol": "MSFT",
      "price": 1535.9075617961096,
      "source": "EODHistorical",
      "lastUpdated": "2019-01-01T00:00:02.001Z"
    }
  ],
  "errors": []
}
```

Error response for a non-existing symbol.

```shell
curl "http://localhost:4000/prices?toSymbol=ZAR&fromSymbols=BANANA"
```
> The above command returns JSON structured like this:

```json
{
  "timestamp": "2019-01-01T00:00:01.001Z",
  "toSymbol": "ZAR",
  "fromSymbols": [],
  "errors": [
    {
      "error_at": "BANANA",
      "message": "No data found for BANANA"
    }
  ]
}
```
