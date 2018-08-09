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
curl "http://inves.technology/users/2"
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

Transactions are created either from an instruction from a user (e.g. through contributions or withdrawals), or are incurred automatically through fees or rebalancing. Most transactions recorded in our system are transfers between one currency type and another.

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
  {
    "id": 10239201,
    "user": "CHLOE",
    "event": "purchase",
    "state": "processed",
    "instruction": {
      "id": 10239201,
      "dateCreated": "",
      "source": "Lettuce iOS app"
    },
    "quote": {

    },

  }
  {
    "id": 10239201,
    "user": "CHLOE",
    "type": "card payment",
    "status": "processed",
    "toCurrency": "GBP",
    "bought": {
      "debitOrCredit": "credit",
      "amount": 2000.05,
      "denomination": "GBP",
    },
    "dateCreated": "2012-04-23T18:25:43.511Z",
    "dateProcessed": "2012-04-23T18:25:44.511Z"
  },
  {
    "id": 10239202,
    "user": "CHLOE",
    "type": "contribution rebalance",
    "status": "processed",
    "fromCurrency": "GBP",
    "toCurrency": "ETH",
    "sold": {
      "debitOrCredit": "debit",
      "amount": 2000.33,
      "denomination": "GBP",
    },
    "trade": {
      "id": 29293938,
      "platform": "Binance",
      "dateCreated": "2012-04-23T18:25:43.511Z",
      "dateProcessed": "2012-04-23T18:25:44.511Z"
    },
  },
  {
    "id": 29382738,
    "user": 22345678,
    "type": "fund",
    "status": "processed",
    "source": "card payment",
    "fromCurrency": "ZAR",
    "toCurrency": "BTC",
    "transactions": [
      {
        "id": 303020203,
        "debitOrCredit": "debit",
        "amount": 2000.50,
        "denomination": "ZAR",
        "accountId": 32939303,
        "type": "sold"
      }
    ]

    },
    "bought": {
      "debitOrCredit": "credit",
      "value": 0.203920992,
      "denomination": "BTC",
      "accountId": 32939304
    },
    "fees": {
      "debitOrCredit": "debit",
      "amount": 0.50,
      "denomination": "ZAR",
      "accountId": 32939304
    },
    "dateCreated": "2012-04-23T18:25:43.511Z",
    "dateProcessed": "2012-04-23T18:25:44.511Z"
  },
  {
    "id": 12345678,
    "user": 32939303,
    "type": "trade",
    "status": "processed",
    "source": "automatic rebalancing",
    "fromCurrency": "BTC",
    "toCurrency": "ETH",
    "sold": {
      "debitOrCredit": "debit",
      "amount": 0.203920992,
      "denomination": "BTC",
      "account": {
        "id": 230392929,
        "description": "BTC hot wallet",
        "status": "verified",
        "type": "external crypto",
        "denomination": "BTC",
        "address": "1BoatSLRHtKNngkdXEeobR76b53LETtpyT"
      }
    },
    "bought": {
      "debitOrCredit": "credit",
      "amount": 3.302992,
      "denomination": "ETH",
      "accountId": 32939304
    },
    "fees": {
      "debitOrCredit": "debit",
      "amount": 0.0004,
      "denomination": "BTC",
      "accountId": 32939303
    },
    "dateCreated": "2012-04-23T18:25:43.511Z",
    "dateProcessed": "2012-04-23T18:25:44.511Z"
  },
  {
    "id": 22345678,
    "user": 32939304,
    "type": "send",
    "status": "processed",
    "source": "withdrawal",
    "fromCurrency": "BTC",
    "toCurrency": "BTC",
    "sold": {
      "debitOrCredit": "debit",
      "amount": 1.506932,
      "denomination": "BTC",
      "account": {
        "id": 230392929,
        "type": "crypto",
        "denomination": "BTC"
      }
    },
    "bought": {
      "debitOrCredit": "credit",
      "value": 1.502932,
      "denomination": "BTC",
      "account": {
        "id": 230392929,
        "description": "Luno wallet",
        "status": "verified",
        "type": "external crypto",
        "denomination": "BTC",
        "address": "1BoatSLRHtKNngkdXEeobR76b53LETtpyT"
      }
    },
    "fees": {
      "debitOrCredit": "debit",
      "amount": 0.004,
      "denomination": "BTC",
      "account": {
        "id": 230392929,
        "type": "crypto",
        "denomination": "BTC"
      }
    },
    "blockchainId": "5409ab60f51112d2652f136d15a37db1d3257c979e6091db4c4f1a9e2c9c0272",
    "dateCreated": "2012-04-23T18:25:43.511Z",
    "dateProcessed": "2012-04-23T18:25:44.511Z"
  },
  {
    "id": 329305828,
    "user": 203838393,
    "type": "withdrawal",
    "fromCurrency": "BTC",
    "toCurrency": "ZAR",
    "bankAccount": {
      "bank": "FNB",
      "branch": 2392002,
      "accountNumber": 293938393093,
      "accountHolder": "Simon Dingle",
      "nickname": "My favourite bank account"
    },
    "amount": {
      "debitOrCredit": "debit",
      "value": 293203.29,
      "denomination": "ZAR"
    },
    "status": "processed"
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
curl "http://inves.technology/users/2"
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

# User balances

> Accounts per currency type
> Cards you load will have an account ID
> External bank accounts you load will have an account ID
> "type": "internal" or "linked"
> "denomination": "ZAR", "BTC", "ETH" etc.

# Value stores
# Trades
# Assets
# Price
# Suppliers
