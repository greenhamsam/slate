# Institutions

_Update 15 Jan 2019: not yet implemented_

Available in a later release, when users can link accounts.

All of the places where Inves Technology buys cryptocurrency assets from, like Binance or Cumberland.

We will maintain a list of institutions so that we can default account data. Institutions also contain information that is required by the pricing engine - i.e. need to store trading fees for specific platforms.

```ruby
require 'appia'

api = Appia::APIClient.authorize!('mypersonalapikey')
api.Institutions.get
```

```python
import appia

api = appia.authorize('mypersonalapikey')
api.Institutions.get()
```

```shell
curl "http://example.com/api/Institutions"
  -H "Authorization: mypersonalapikey"
```

```javascript
const appia = require("appia");

let api = appia.authorize("mypersonalapikey");
let users = api.Institutions.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 12345678,
    "name": "Binance",
    "address": "1BvBMSEYstWetqTFn5Au4m4GFg7xJaNVN2",
    "available": [
      {
        "sellAsset": "BTC",
        "buyAsset": "ETH",
        "feePercent": 0.05,
        "minimumTrade": 0.01
      },
      {
        "sellAsset": "BTC",
        "buyAsset": "BCH",
        "feePercent": 0.05,
        "minimumTrade": 0.01
      }
    ],
    "withdrawalFees": {
      "amount": 0.05,
      "denomination": "BTC"
    },
    "withdrawalLimit": {
      "amount": 100000,
      "denomination": "BTC",
      "hours": 24
    }
  },
  {
    // A second Institution
  }
]
```
