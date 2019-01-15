# Trades

_Update 15 Jan 2019: not yet implemented_

All of the inter-asset trades that Inves makes on our Institution platforms. These change the real underlying assets in our value store accounts. Trades are also where we move money between different value store accounts. This database could also be called "Inves Transactions".

```ruby
require 'appia'

api = Appia::APIClient.authorize!('mypersonalapikey')
api.trades.get
```

```python
import appia

api = appia.authorize('mypersonalapikey')
api.trades.get()
```

```shell
curl "http://example.com/api/trades"
  -H "Authorization: mypersonalapikey"
```

```javascript
const appia = require("appia");

let api = appia.authorize("mypersonalapikey");
let users = api.trades.get();
```

> The above command returns JSON structured like this:

```json
[
  // Inves exchanges BTC for IOTA on behalf of a user on Binance
  {
    "id": 10239201,
    "type": "crypto for crypto",
    "state": "processed", // Could be instructed, quoted, rejected, failed
    "dateCreated": "2012-04-23T18:25:43.511Z",
    "dateProcessed": "2012-04-23T18:25:44.511Z",
    "Institution": {
      "id": 123423, // Links to the Institutions database
      "name": "Binance"
    },
    "fromCurrency": "BTC",
    "toCurrency": "IOT",
    "sold": {
      "debitOrCredit": "debit",
      "account": {
        "id": 230302,
        "nickname": "Binance BTC hotwallet"
      },
      "amount": 0.203920992,
      "denomination": "BTC"
    },
    "bought": {
      "debitOrCredit": "credit",
      "account": {
        "id": 230302,
        "nickname": "IOTA vault"
      },
      "amount": 3.302992,
      "denomination": "IOT"
    },
    "fees": {
      "debitOrCredit": "debit",
      "amount": 0.0004,
      "denomination": "BTC"
    }, // Would fees not just be built into our quoted price?
    "transaction": {
      "id": 10239201 // If there is a related user Transaction, this links to the Transactions database
    }
  },
  // Inves tops up our BTC float
  {
    "id": 10239201,
    "type": "inter crypto transfer",
    "state": "processed", // Could be instructed, quoted, rejected, failed
    "source": "float rules",
    "dateCreated": "2012-04-23T18:25:43.511Z",
    "dateProcessed": "2012-04-23T18:25:44.511Z",
    "fromCurrency": "BTC",
    "toCurrency": "BTC",
    "sold": {
      "debitOrCredit": "debit",
      "account": {
        "id": 230302,
        "nickname": "BTC vault"
      },
      "amount": 0.203920992,
      "denomination": "BTC"
    },
    "bought": {
      "debitOrCredit": "credit",
      "account": {
        "id": 230302,
        "nickname": "BTC hotwallet Binance"
      },
      "amount": 3.302992,
      "denomination": "BTC"
    },
    "fees": {
      "debitOrCredit": "debit",
      "amount": 0.0004,
      "denomination": "BTC"
    },
    "blockhainId": "e81b7ee809ac5319a54203c1740c686028bfa0612fa22a53c4e6c1f5e7c9e332"
  },
  // Inves buys more Bitcoin for GBP
  {
    "id": 10239201,
    "type": "fiat for crypto",
    "state": "processed", // Could be instructed, quoted, rejected, failed
    "source": "admin",
    "Institution": {
      "id": 123423, // Links to the Institutions database
      "name": "Cumberland"
    },
    "dateCreated": "2012-04-23T18:25:43.511Z",
    "dateProcessed": "2012-04-23T18:25:44.511Z",
    "fromCurrency": "GBP",
    "toCurrency": "BTC",
    "sold": {
      "debitOrCredit": "debit",
      "account": {
        "id": 230302,
        "nickname": "Revolut account"
      },
      "amount": 39292.32,
      "denomination": "GBP"
    },
    "bought": {
      "debitOrCredit": "credit",
      "account": {
        "id": 230302,
        "nickname": "BTC day to day"
      },
      "amount": 3.302992,
      "denomination": "BTC"
    }
  }
]
```
