# Portfolios

A user can have multiple portfolios. A portfolio is a collection of accounts. By defualt, every user has 1 portfolio called "My Moneh". 

Users can add up to 3 portfolios on the free tier, and can add up to 100 portfolios on the paid tier (TBC).

NOTE:
- Should be able to retrieve all portfolios for a single user.
- In the future, a portfolio could belong to a group.

## Get All Portfolios

```ruby
require 'appia'

api = Appia::APIClient.authorize!('mypersonalapikey')
api.portfolios.get
```

```python
import appia

api = appia.authorize('mypersonalapikey')
api.portfolios.get()
```

```shell
curl "http://example.com/api/portfolios"
  -H "Authorization: mypersonalapikey"
```

```javascript
const appia = require('appia');

let api = appia.authorize('mypersonalapikey');
let portfolios = api.portfolios.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 12345678,
    "name": "My Moneh",
    "user": 12345678,
    "accounts": [
      2392392,
      2301938,
      2938218,
    ],
    "latestBalance": {
      "amount": 2.39,
      "debitOrCredit": "debit",
      "currency": "BTC",
      "time": "2012-04-23T18:25:43.511Z",
    },
  },
  {
    "id": 12345679,
    "name": "Genesis Mining Income",
    "user": 12345678,
    "accounts": [
      2392393,
      2301938,
    ],
    "latestBalance": {
      "amount": 1.39,
      "debitOrCredit": "debit",
      "currency": "ETH",
      "time": "2012-04-23T18:25:43.511Z",
    },
  }
]
```

This endpoint retrieves all portfolios.
