# Prices

TODO

The historical price data of all assets that we store from various Institutions who supply our cryptocurrency assets, and the prices that Inves has quoted for cryptocurrencies on that day.

_I'm assuming that we will run this script at midnight every day rather than keeping up to the minute/hour prices. Or add a lastUpdated field also for quick querying of a semi-current price?_

```ruby
require 'appia'

api = Appia::APIClient.authorize!('mypersonalapikey')
api.prices.get
```

```python
import appia

api = appia.authorize('mypersonalapikey')
api.prices.get()
```

```shell
curl "http://example.com/api/prices"
  -H "Authorization: mypersonalapikey"
```

```javascript
const appia = require('appia');

let api = appia.authorize('mypersonalapikey');
let users = api.prices.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 12345678, // Can we rather use User-Date as the primary key?
    "Institution": {
      "id": 12345678,
      "name": "Binance"
    },
    "day": "20180812",
    "baseDenomination": "GBP",
    "prices": [
      {
        "asset": "BTC",
        "price": 233202.20,
      },
      {
        "asset": "ETH",
        "price": 13202.20,
      }
    ]
  },
  {
    "id": 12345678, // Can we rather use User-Date as the primary key?
    "Institution": {
      "id": 000000,
      "name": "Inves"
    },
    "day": "20180812",
    "baseDenomination": "GBP",
    "prices": [
      {
        "asset": "BTC",
        "price": 233202.20,
      },
      {
        "asset": "ETH",
        "price": 13202.20,
      }
    ]
  }
]
```