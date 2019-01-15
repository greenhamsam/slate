# Transactions

_Update 15 Jan 2019: not yet implemented_

TRANSACTIONS ARE NOT INCLUDED IN OUR MVP

Each transaction represents the **flow** of value into and out of an account. A transaction effects the **quantity** of the asset held in an account rather than its **balance**. Where the quantity is not known on an account we do not derive the balance from the sum of transactions on that account.

Every transaction must be either a debit or a credit transaction. A transaction must, at minimum, have an **amount** of an **asset** (the same asset as the account it belongs to), a **date** and a **description**. Where a **description** does not exist in the source data, we will derive one.

A transaction belongs to a single account. Where a user transfers money between accounts, that will generate two different transactions, a debit transaction on one account, and a credit transaction on the other.

--

Transactions are created either from an instruction from a user (e.g. through contributions or withdrawals), or are incurred automatically through fees or rebalancing.

Most transactions recorded in our system are likely to be transfers between one currency type and another. More traditional send and receive transactions need to be supported too, though.

Transactions go through many states which are recorded in the Events log (see below). Only the current state of the transaction is recorded in this database.

Transactions refer to user transactions only. They change values in the ledger but do not actually move underlying assets between accounts. The movement of real assets is referred to as a Trade, in our world.
_(This assumes that we're going with an omnnibus accounts model. If we decide differently, we will need to redesign this.)_

Notes:

- accountId
- debitOrCredit
- quantityDelta
- assetId
- date
- description

## Get All Transactions

```ruby
require 'appia'

api = Appia::APIClient.authorize!('mypersonalapikey')
api.transactions.get
```

```python
import appia

api = appia.authorize('mypersonalapikey')
api.transactions.get()
```

```shell
curl "http://example.com/api/transactions"
  -H "Authorization: mypersonalapikey"
```

```javascript
const appia = require("appia");

let api = appia.authorize("mypersonalapikey");
let users = api.transactions.get();
```

> The above command returns JSON structured like this:

```json
[
  // A user buys ETH using BTC using the Lettuce iOS app
  {
    "id": 10239201,
    "user": {
      "id": 10239201,
      "name": "Chloe Coetzee"
    },
    "type": "purchase",
    "state": "processed", // Could be instructed, quoted, rejected, failed
    "dateCreated": "2012-04-23T18:25:43.511Z",
    "dateProcessed": "2012-04-23T18:25:44.511Z",
    "source": "Lettuce iOS app", // Could be Automatic rebalancing
    "fromCurrency": "BTC",
    "toCurrency": "ETH",
    "sold": {
      "debitOrCredit": "debit",
      "amount": 0.203920992,
      "denomination": "BTC"
    },
    "bought": {
      "debitOrCredit": "credit",
      "amount": 3.302992,
      "denomination": "ETH"
    },
    "fees": {
      "debitOrCredit": "debit",
      "amount": 0.0004,
      "denomination": "BTC"
    }, // Would fees not just be built into our quoted price?
    "trade": {
      "id": 10239201 // If there is a related Trade, this links to the Trade database
    }
  },
  // A user funds her account with a credit card
  {
    "id": 10239201,
    "user": {
      "id": 10239201,
      "name": "Chloe Coetzee"
    },
    "type": "card payment",
    "status": "processed",
    "dateCreated": "2012-04-23T18:25:43.511Z",
    "dateProcessed": "2012-04-23T18:25:44.511Z",
    "source": "Lettuce iOS app",
    "toCurrency": "GBP",
    "bought": {
      "debitOrCredit": "credit",
      "amount": 2000.05,
      "denomination": "GBP"
    },
    "fees": {
      "debitOrCredit": "debit",
      "amount": 0.04,
      "denomination": "GBP"
    },
    "trade": {
      "id": 10239201 // There is a related incoming GBP transaction into the Inves Revolut account
    },
    "card": {
      "id": 10239201,
      "nickname": "FNB credit card",
      "cardNumber": 33333333333333,
      "nameOnCard": "C Coetzee",
      "expiryMonth": "08",
      "expiryYear": "2020",
      "securityCode": 302,
      "issuer": "Visa" // Does this rather belong under Trades? Or in its own database?
    }
  },
  // A user withdraws GBP from her account
  {
    "id": 10239201,
    "user": {
      "id": 10239201,
      "name": "Chloe Coetzee"
    },
    "type": "withdrawal",
    "state": "processed", // Could be instructed, quoted, rejected, failed
    "dateCreated": "2012-04-23T18:25:43.511Z",
    "dateProcessed": "2012-04-23T18:25:44.511Z",
    "source": "Lettuce iOS app",
    "fromCurrency": "GBP",
    "sold": {
      "debitOrCredit": "debit",
      "amount": 20392.02,
      "denomination": "GBP"
    },
    "fees": {
      "debitOrCredit": "debit",
      "amount": 0.4,
      "denomination": "GBP"
    }, // Would fees not just be built into our quoted price?
    "trade": {
      "id": 10239201 // There is a related outgoing GBP transaction
    },
    "bankAccount": {
      // Does this rather belong under Trades? In its own database?
      "bank": "FNB",
      "branch": 2392002,
      "accountNumber": 293938393093,
      "accountHolder": "Chloe Coetzee",
      "nickname": "My favourite bank account"
    }
  }
]
```

This endpoint retrieves all transactions.

### HTTP Request

`GET http://inves.technology/api/transactions`

### Query Parameters

| Parameter      | Default | Description                                                               |
| -------------- | ------- | ------------------------------------------------------------------------- |
| only_processed | false   | If set to true, only transactions with a processed state will be returned |

## Get a Specific Transaction

```ruby
require 'appia'

api = Appia::APIClient.authorize!('mypersonalapikey')
api.transactions.get(12345678)
```

```python
import appia

api = appia.authorize('mypersonalapikey')
api.transactions.get(12345678)
```

```shell
curl "http://inves.technology/transactions/12345678"
  -H "Authorization: mypersonalapikey"
```

```javascript
const appia = require("appia");

let api = appia.authorize("mypersonalapikey");
let max = api.transactions.get(12345678);
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 12345678,
    "user": {
      "id": 10239201,
      "name": "Chloe Coetzee"
    },
    "type": "purchase",
    "state": "processed",
    "dateCreated": "2012-04-23T18:25:43.511Z",
    "dateProcessed": "2012-04-23T18:25:44.511Z",
    "source": "Automatic rebalance",
    "fromCurrency": "BTC",
    "toCurrency": "ETH",
    "sold": {
      "debitOrCredit": "debit",
      "amount": 0.203920992,
      "denomination": "BTC"
    },
    "bought": {
      "debitOrCredit": "credit",
      "amount": 3.302992,
      "denomination": "ETH"
    },
    "fees": {
      "debitOrCredit": "debit",
      "amount": 0.0004,
      "denomination": "BTC"
    }, // Would fees not just be built into our quoted price?
    "trade": {
      "id": 10239201 // If there is a related Trade, this links to the Trades database
    }
  }
]
```

This endpoint retrieves a specific transaction.

### HTTP Request

`GET http://inves.technology/trades/<ID>`

### URL Parameters

| Parameter | Description                     |
| --------- | ------------------------------- |
| ID        | The ID of the trade to retrieve |
