---
title: Appia API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Appia API. You can use our API to access Appia endpoints, which can query balances and transactions and tell you which of our users are cat people.

We have language bindings in Shell, Ruby, Python, and JavaScript. BOOM. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

Oh by the way, Simon Dingle has an extremely silly face. 😜

# Important Definitions

Some important definitions that exist within our world.

## Account

An account has a balance that is the sum of transactions. A balance is a record of the current **state** of the account. An account can only have type of asset inside it. That asset could be a currency, cryptocurrency, units of a fund, value of a house, or many other things. You cannot have a single account that is made up of two different currencies - as far as our system is concerned, those are two different accounts. It might, however, be helpful to sometimes group similar accounts for our users.

All balances are made up of a **quantity** of a **type of asset** that has a **current price** in the user's **base currency**. For instance:
- I have an account with Luno, and I own 10 ETH and 2 Bitcoins on that platform. I like to see everything converted back to South African Rands (this is my base currency). The price of BTC at this moment is R 90,000 and the price of ETH is R 2 000. Appia sees this as me having two accounts:
  1. A Luno (**institution**) ETH (**asset type**) account with a **quantity** of 10 at a **current price** in my **base currency** of R 2 000. The **balance** of my account is therefore R 20 000.
  2. A Luno (**institution**) BTC (**asset type**) account with a **quantity** of 2 at a **current price** in my **base currency** of R 90 000. The **balance** of my account is therefore R 180 000.
- I also have a share portfolio through EasyEquities. I own 15 shares in the S&P 500 that are worth R 100 each, and 3 shares of Netflix that are worth R 50 each. IF I am able to scrape all of this data with Appia, then Appia will see this as 2 accounts:
  1. A EasyEquities (**institution**) S&P 500 (**asset type**) account with a **quantity** of 15 at a **current price** in my **base currency** of R 100. The **balance** of my account is therefore R 1 500.
  2. A EasyEquities (**institution**) Netflix (**asset type**) account with a **quantity** of 3 at a **current price** in my **base currency** of R 50. The **balance** of my account is therefore R 150.

However, I may not be able to get this level of detail back from EasyEquities. In that case, Appia might see this as one account that we don't know everything about:
  - A EasyEquities (**institution**) international equities (**asset type**) account with a **balance** of R 1 650. 

An account is **somewhere**, usually at an institution (e.g. Luno, Barclays, on a paper wallet).

## Transaction

Each transaction represents the **flow** of value in and out of an account.

## Institution

# Authentication

> To authorise, use this code:

```ruby
require 'appia'

api = Appia::APIClient.authorize!('mypersonalapikey')
```

```python
import appia

api = appia.authorize('mypersonalapikey')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: mypersonalapikey"
```

```javascript
const appia = require('appia');

let api = appia.authorize('mypersonalapikey');
```

> Make sure to replace `mypersonalapikey` with your API key.

Appia uses API keys to allow access to the API. To register a new API key, buy Kenny a beer and hope that he takes pity on you.

Appia expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: mypersonalapikey`

<aside class="notice">
You must replace <code>mypersonalapikey</code> with your personal API key.
</aside>

# Users

## Get All Users

```ruby
require 'appia'

api = Appia::APIClient.authorize!('mypersonalapikey')
api.users.get
```

```python
import appia

api = appia.authorize('mypersonalapikey')
api.users.get()
```

```shell
curl "http://example.com/api/users"
  -H "Authorization: mypersonalapikey"
```

```javascript
const appia = require('appia');

let api = appia.authorize('mypersonalapikey');
let users = api.users.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 12345678,
    "name": "Sam Beckbessinger",
    "email": "sam@inves.technology",
    "group": {
      "id": 12345678,
      "name": "Inves Club"
    },
    "deleted": false,
    "lastActivity": "2012-04-23T18:25:43.511Z",
    "kyc": "not required"
  },
  {
    "id": 22345678,
    "name": "Simon Dingle",
    "email": "simon@inves.technology",
    "group": null,
    "deleted": false,
    "lastActivity": "2017-04-23T18:25:43.511Z",
    "kyc": "not required"
  }
]
```

This endpoint retrieves all users.

### HTTP Request

`GET http://inves.technology/api/users`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_deleted | false | If set to true, the result will also include deleted users.

## Get a Specific User

```ruby
require 'appia'

api = Appia::APIClient.authorize!('mypersonalapikey')
api.users.get(12345678)
```

```python
import appia

api = appia.authorize('mypersonalapikey')
api.users.get(12345678)
```

```shell
curl "http://inves.technology/users/212345678"
  -H "Authorization: mypersonalapikey"
```

```javascript
const appia = require('appia');

let api = appia.authorize('mypersonalapikey');
let max = api.users.get(12345678);
```

> The above command returns JSON structured like this:

```json
{
  "id": 12345678,
  "name": "Sam Beckbessinger",
  "email": "sam@inves.technology",
  "group": {
    "id": 12345678,
    "name": "Inves Club"
  },
  "deleted": false,
  "lastActivity": "2012-04-23T18:25:43.511Z",
  "kyc": "not required"
}
```

This endpoint retrieves a specific user.

### HTTP Request

`GET http://inves.technology/users/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user to retrieve

## Delete a Specific User

```ruby
require 'appia'

api = Appia::APIClient.authorize!('mypersonalapikey')
api.users.delete(12345678)
```

```python
import appia

api = appia.authorize('mypersonalapikey')
api.users.delete(12345678)
```

```shell
curl "http://inves.technology/api/users/12345678"
  -X DELETE
  -H "Authorization: mypersonalapikey"
```

```javascript
const appia = require('appia');

let api = appia.authorize('mypersonalapikey');
let max = api.users.delete(12345678);
```

> The above command returns JSON structured like this:

```json
{
  "id": 12345678,
  "deleted" : true
}
```

This endpoint deletes a specific user.

### HTTP Request

`DELETE http://inves.technology/users/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user to delete

# Groups

Groups are collections of users who have special defaults applied to them, for instance, they may share a portfolio strategy or be part of the same fund.

## Get All Groups

```ruby
require 'appia'

api = Appia::APIClient.authorize!('mypersonalapikey')
api.groups.get
```

```python
import appia

api = appia.authorize('mypersonalapikey')
api.s.get()
```

```shell
curl "http://example.com/api/groups"
  -H "Authorization: mypersonalapikey"
```

```javascript
const appia = require('appia');

let api = appia.authorize('mypersonalapikey');
let groups = api.groups.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 12345678,
    "name": "Inves Club",
    "members": [
      12345678,
      22345678,
      32345678,
      42345678,
      52345678
    ]
  },
  {
    "id": 12345678,
    "name": "Lettuce",
    "members": [
      12345678,
      32345678,
      92345678,
      11345678,
      22345678
    ]
  }
]
```

This endpoint retrieves all groups.

### HTTP Request

`GET http://inves.technology/api/groups`

## Get members belonging to a specific group

```ruby
require 'appia'

api = Appia::APIClient.authorize!('mypersonalapikey')
api.groups.members.get(12345678)
```

```python
import appia

api = appia.authorize('mypersonalapikey')
api.groups.members.get(12345678)
```

```shell
curl "http://inves.technology/groups/members/12345678"
  -H "Authorization: mypersonalapikey"
```

```javascript
const appia = require('appia');

let api = appia.authorize('mypersonalapikey');
let max = api.groups.members.get(12345678);
```

> The above command returns JSON structured like this:

```json
{
  "members": [
    12345678,
    32345678,
    92345678,
    11345678,
    22345678
  ]
}
```

This endpoint retrieves members belonging to a specific group.

### HTTP Request

`GET http://inves.technology/groups/members/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the group to retrieve members from

## Delete a User from a Group

```ruby
require 'appia'

api = Appia::APIClient.authorize!('mypersonalapikey')
api.groups.members.delete(22345678, 32345678)
```

```python
import appia

api = appia.authorize('mypersonalapikey')
api.groups.members.delete(22345678, 32345678)
```

```shell
curl "http://inves.technology/api/groups/members/22345678&32345678"
  -X DELETE
  -H "Authorization: mypersonalapikey"
```

```javascript
const appia = require('appia');

let api = appia.authorize('mypersonalapikey');
let max = api.groups.members.delete(22345678, 32345678);
```

> The above command returns JSON structured like this:

```json
{
  "id": 32345678,
  "deleted" : true
}
```

This endpoint deletes a specific user from a group. That user is deleted only from the group.

<aside class="notice">
Always list the group ID first, then the user ID.
</aside>

### HTTP Request

`DELETE http://inves.technology/groups/members/<GROUP_ID>&<USER_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
GROUP_ID | The ID of the group to delete the user from
USER_ID | The ID of the user to delete

# Transactions

Transactions are created either from an instruction from a user (e.g. through contributions or withdrawals), or are incurred automatically through fees or rebalancing.

Most transactions recorded in our system are likely to be transfers between one currency type and another. More traditional send and receive transactions need to be supported too, though.

Transactions go through many states which are recorded in the Events log (see below). Only the current state of the transaction is recorded in this database.

Transactions refer to user transactions only. They change values in the ledger but do not actually move underlying assets between accounts. The movement of real assets is referred to as a Trade, in our world.
_(This assumes that we're going with an omnnibus accounts model. If we decide differently, we will need to redesign this.)_

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
const appia = require('appia');

let api = appia.authorize('mypersonalapikey');
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
      "denomination": "ETH",
    },
    "fees": {
      "debitOrCredit": "debit",
      "amount": 0.0004,
      "denomination": "BTC",
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
      "denomination": "GBP",
    },
    "fees": {
      "debitOrCredit": "debit",
      "amount": 0.04,
      "denomination": "GBP",
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
      "denomination": "GBP",
    }, // Would fees not just be built into our quoted price?
    "trade": {
      "id": 10239201 // There is a related outgoing GBP transaction
    },
    "bankAccount": { // Does this rather belong under Trades? In its own database?
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

Parameter | Default | Description
--------- | ------- | -----------
only_processed | false | If set to true, only transactions with a processed state will be returned

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
const appia = require('appia');

let api = appia.authorize('mypersonalapikey');
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
      "denomination": "ETH",
    },
    "fees": {
      "debitOrCredit": "debit",
      "amount": 0.0004,
      "denomination": "BTC",
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

Parameter | Description
--------- | -----------
ID | The ID of the trade to retrieve

# User balances

The historical and current balance of each user, for each asset type that they hold with Inves. These balances are calculated at midnight for each user and stored historically. Today's balance is stored temporarily in this database if it's requested by a front-end, but it is over-written at midnight.

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
    "user": {
      "id": 12345678,
      "name": "Sam Beckbessinger"
    },
    "day": "20180812",
    "baseDenomination": "GBP",
    "total": {
      "amount": 39293.29,
      "denomination": "GBP"
    },
    "balances": [
      {
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

# Accounts

The real accounts where different assets are stored. This could also be called "Value Stores". In future, we could allow users to link accounts, also.

_Is there any purpose in us storing historical account balances?_

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
let users = api.accounts.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 12345678,
    "nickname": "ETH vault",
    "address": "1BoatSLRHtKNngkdXEeobR76b53LETtpyT",
    "asset": "ETH",
    "amount": 203020202.23,
    "value": 23030302023.30 // Today's BTC value
  },
  {
    "id": 12345679,
    "nickname": "Binance hotwallet",
    "address": "1BoatSLRHtKNngkdXEeobR76b53LETtpyT",
    "asset": "BTC",
    "amount": 3.23,
    "value": 3.23 // Will usually equal on a BTC denominated account
  }
]
```

# Trades

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
const appia = require('appia');

let api = appia.authorize('mypersonalapikey');
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
      "name": "Binance",
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
      "denomination": "IOT",
    },
    "fees": {
      "debitOrCredit": "debit",
      "amount": 0.0004,
      "denomination": "BTC",
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
      "denomination": "BTC",
    },
    "fees": {
      "debitOrCredit": "debit",
      "amount": 0.0004,
      "denomination": "BTC",
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
      "name": "Cumberland",
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
      "denomination": "BTC",
    }
  }
]
```

# Assets

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

# Institutions

All of the places where Inves Technology buys cryptocurrency assets from, like Binance or Cumberland.

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
const appia = require('appia');

let api = appia.authorize('mypersonalapikey');
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

# Prices

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

# Events

A log of all of the events that change the values of any account in the system. What occured, at what time. These events are things like: a transaction or trade was initiated, processed, rejected, failed or reversed. A new account was created or deleted.

// To do. This still needs a lot of thinking.