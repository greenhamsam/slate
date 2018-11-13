# User balances

The historical and current balance of each user, for each asset type that they hold with Inves. These balances are calculated at midnight for each user and stored historically. Today's balance is stored temporarily in this database if it's requested by a front-end, but it is over-written at midnight.

TODO: needs to be finalised

```ruby
require 'appia'

api = Appia::APIClient.authorize!('mypersonalapikey')
api.user_balances.get
```

```python
import appia

api = appia.authorize('mypersonalapikey')
api.user_balances.get()
```

```shell
curl "http://example.com/api/user_balances"
  -H "Authorization: mypersonalapikey"
```

```javascript
const appia = require('appia');

let api = appia.authorize('mypersonalapikey');
let users = api.user_balances.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 12345678, // Can we rather use User-Date as the primary key?
    "user": 12345678,
    "day": "20180812",
    "baseCurrency": "GBP",
    "totalBalance": {
      "amount": 39293.29,
      "currency": "GBP"
    },
    "portfolioBalances": [
      {
        "portfolio": 230293,
        "currency": "GBP",
        "value": ,
        "time": ,
      },
    ],
    "accountBalances": [
      {
        "account": 230293,
        "asset": "BTC",
        "amount": 1.30,
        "value": 29293.23 // The value on that day in the baseDenomination GBP
      },
      {
        "asset": "ETH",
        "amount": 23.23,
        "value": 3923.23
      }
    ]
  },
  {
    "id": 12345678,
    "user": {
      "id": 12345678,
      "name": "Simon Dingle"
    },
    "day": "20180812",
    "baseDenomination": "GBP",
    "total": {
      "amount": 2339293.29,
      "denomination": "GBP"
    },
    "balances": [
      {
        "asset": "BTC",
        "amount": 10.30,
        "value": 239293.23 // The value on that day in the baseDenomination GBP
      },
      {
        "asset": "ETH",
        "amount": 123.23,
        "value": 39423.23
      }
    ]
  }
]
```