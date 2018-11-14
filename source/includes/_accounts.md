# Accounts

An account has a **balance**. A balance is a record of the current **state** of the account. An account can only have one type of asset inside it. That asset could be a currency, cryptocurrency, units of a fund, value of a house, or many other things. You cannot have a single account that is made up of two different currencies - as far as our system is concerned, those are two different accounts. It might, however, be helpful to sometimes group similar accounts for our users.

An account is **somewhere**, usually at an institution (e.g. Luno, Barclays) but sometimes on a paper wallet or in the deeds office (if I own a house). For consistency, our data structure will refer to all of these "wheres" as **institutions** even if it's a leather wallet in the user's backpack.

All balances are made up of a **quantity** of an **asset** that has a **current price** in the user's **base currency**. The quantity is the result of the sum of transactions that occured on an account.

Sometimes we know a lot about an account, so we can derive the **current balance** ourselves. For instance, say I have an account with Luno, and I own 10 ETH and 2 Bitcoins on that platform. I like to see everything converted back to South African Rands (this is my base currency). The price of BTC at this moment is R 90,000 and the price of ETH is R 2 000. Appia sees this as me having two accounts:
  1. A Luno (**institution**) ETH (**asset**) account with a **quantity** of 10 at a **current price** in my **base currency** of R 2 000. The **balance** of my account is therefore R 20 000. The **asset type** is "cryptocurrency".
  2. A Luno (**institution**) BTC (**asset**) account with a **quantity** of 2 at a **current price** in my **base currency** of R 90 000. The **balance** of my account is therefore R 180 000. The **asset type** is "cryptocurrency".

Say I also have an international share portfolio through EasyEquities. I own 15 shares in the S&P 500 that are worth R 100 each, and 3 shares of Netflix that are worth R 50 each. IF I am able to scrape all of this data with Appia, then Appia will see this as 2 accounts:
  1. A EasyEquities (**institution**) S&P 500 (**asset**) account with a **quantity** of 15 at a **current price** in my **base currency** of R 100. The **balance** of my account is therefore R 1 500. The **asset type** is "international equities".
  2. A EasyEquities (**institution**) Netflix (**asset**) account with a **quantity** of 3 at a **current price** in my **base currency** of R 50. The **balance** of my account is therefore R 150. The **asset type** is "cryptocurrency".

However, I may not be able to get this level of detail back from EasyEquities. In that case, Appia might see this as one account that we don't know a lot about:
  1. A EasyEquities (**institution**) account with a **balance** of R 1 650. I might know that the **asset type** is "international equities" but I may not know exactly what assets are held in that account.

Sometimes the **asset** held in a user's **account** will be identical to their **base currency**. It is still important to track the **quantity** separately to the **balance** where possible, though, because the user can change their **base currency** at any time.


```ruby
require 'appia'

api = Appia::APIClient.authorize!('mypersonalapikey')
api.accounts.get
```

```python
import appia

api = appia.authorize('mypersonalapikey')
api.accounts.get()
```

```shell
curl "http://example.com/api/accounts"
  -H "Authorization: mypersonalapikey"
```

```javascript
const appia = require('appia');

let api = appia.authorize('mypersonalapikey');
let accounts = api.accounts.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 12345678,
    "where": "Ledger Nano",
    "type": "tracked", // Can be "tracked" or "manual", in future releases, could be "linked"
    "assetSymbol": "ETH",
    "assetName": "Ethereum",
    "assetType": "cryptocurrency",
    "portfolios": [ // Optional: this account is listed in 2 portfolios
      129302,
      230199,
    ],
    "latest_balance": {
      "debitOrCredit": "debit",
      "price": 10, // In that user's base_currency
      "quantity": 2.39,
      "value": 20.9,
      "currency": "ZAR",
      "time": "2012-04-23T18:25:43.511Z",
    },
  },
  {
    "id": 12345679,
    "where": null,
    "type": "tracked", // Can be "tracked" or "manual", in future releases, could be "linked"
    "assetSymbol": "VOD.JS",
    "assetName": "Vodacom South Africa",
    "assetType": "equity",
    "latest_balance": {
      "value": 20.9, // For some accounts, we only return a value
      "currency": "ZAR",
      "time": "2012-04-23T18:25:43.511Z",
    },
  }
]
```