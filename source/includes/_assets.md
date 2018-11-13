# Assets

TODO

All of the asset types that we carry and their latest quoted best price from a Institution, and the most recently Inves quoted price for that asset.

```ruby
require 'appia'

api = Appia::APIClient.authorize!('mypersonalapikey')
api.assets.get
```

```python
import appia

api = appia.authorize('mypersonalapikey')
api.assets.get()
```

```shell
curl "http://example.com/api/assets"
  -H "Authorization: mypersonalapikey"
```

```javascript
const appia = require('appia');

let api = appia.authorize('mypersonalapikey');
let users = api.assets.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 12345678,
    "name": "Ethereum",
    "code": "ETH",
    "buy": { // The best available price we can buy this at right now (or at midnight)
      "price": 2.23,
      "denomination": "BTC",
      "Institution": {
        "id": 230302,
        "name": "Binance"
      },
      "lastUpdated": "2012-04-23T00:00:00.000Z"
    },
    "sell": { // Our current price to sell this asset
      "price": 2.3,
      "denomination": "BTC",
      "lastUpdated": "2012-04-23T00:00:00.000Z"
    }
  },
  {
    "id": 12345678,
    "name": "Bitcoin",
    "code": "BTC",
    "buy": {
      "price": 223023.23,
      "denomination": "USD",
      "Institution": {
        "id": 230302,
        "name": "Cumberland"
      },
      "lastUpdated": "2012-04-23T00:00:00.000Z"
    },
    "sell": {
      "price": 223024,
      "denomination": "GBP",
      "lastUpdated": "2012-04-23T00:00:00.000Z"
    }
  }
]
```