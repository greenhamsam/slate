# Balances

The historical and current balance of each user for each account, portfolio, and user overall. These balances are calculated at midnight for each user and stored historically. Today's balance is stored temporarily in this database if it's requested by a front-end, but it is over-written at midnight.

```ruby
require 'appia'

api = Appia::APIClient.authorize!('mypersonalapikey')
api.balances.get
```

```python
import appia

api = appia.authorize('mypersonalapikey')
api.balances.get()
```

```shell
curl "http://example.com/api/balances"
  -H "Authorization: mypersonalapikey"
```

```javascript
const appia = require('appia');

let api = appia.authorize('mypersonalapikey');
let balances = api.balances.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 12345678, // Can we rather use User-Date as the primary key?
    "user": 12345678,
    "day": "20180812",
    "baseCurrency": "GBP", // all values below are expressed in this baseCurrency
    "totalBalance": {
      "amount": 39293.29,
      "currency": "GBP"
    },
    "portfolioBalances": [
      {
        "portfolio": 230293,
        "value": 239.23,
      },
      {
        "portfolio": 330293,
        "value": -2939.29,
      },
    ],
    "accountBalances": [
      {
        "manual": false,
        "account": 230293,
        "asset": "BTC",
        "amount": 1.30,
        "value": 29293.23,
      },
      {
        "manual": true,
        "account": 320323,
        "asset": null,
        "amount": null,
        "value": 3923.23,
      }
    ]
  },
]
```