# Users

_Update 15 Jan 2019: implemented only in the front-ends_

We do not store any personal information about our users.

Every user is given a unique ID when the account is created.

In the future, users will be able to belong to groups. This is not available in our MVP, though, so set all "groups" to "null".

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
const appia = require("appia");

let api = appia.authorize("mypersonalapikey");
let users = api.users.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 12345678,
    "groups": null,
    "deleted": false,
    "baseCurrency": "ZAR",
    "baseCurrencySymbol": "R",
    "lastActivity": "2012-04-23T18:25:43.511Z",
    "latestBalance": {
      "amount": 203232.39,
      "debitOrCredit": "debit",
      "currency": "ZAR",
      "time": "2012-04-23T18:25:43.511Z"
    }
  },
  {
    "id": 22345679,
    "groups": null,
    "deleted": false,
    "baseCurrency": "BTC",
    "baseCurrencySymbol": "Ƀ",
    "lastActivity": "2017-04-23T18:25:43.511Z",
    "latestBalance": {
      "amount": 2.39,
      "debitOrCredit": "debit",
      "currency": "BTC",
      "time": "2012-04-23T18:25:43.511Z"
    }
  }
]
```

This endpoint retrieves all users.

### HTTP Request

`GET http://inves.technology/api/users`

### Query Parameters

| Parameter       | Default | Description                                                 |
| --------------- | ------- | ----------------------------------------------------------- |
| include_deleted | false   | If set to true, the result will also include deleted users. |

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
const appia = require("appia");

let api = appia.authorize("mypersonalapikey");
let max = api.users.get(12345678);
```

> The above command returns JSON structured like this:

```json
{
  "id": 12345678,
  "groups": null,
  "deleted": false,
  "baseCurrency": "ZAR",
  "baseCurrencySymbol": "R",
  "lastActivity": "2012-04-23T18:25:43.511Z",
  "latestBalance": {
    "amount": 203232.39,
    "debitOrCredit": "debit",
    "currency": "ZAR",
    "time": "2012-04-23T18:25:43.511Z"
  }
}
```

This endpoint retrieves a specific user.

### HTTP Request

`GET http://inves.technology/users/<ID>`

### URL Parameters

| Parameter | Description                    |
| --------- | ------------------------------ |
| ID        | The ID of the user to retrieve |

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
const appia = require("appia");

let api = appia.authorize("mypersonalapikey");
let max = api.users.delete(12345678);
```

> The above command returns JSON structured like this:

```json
{
  "id": 12345678,
  "deleted": true
}
```

This endpoint deletes a specific user.

### HTTP Request

`DELETE http://inves.technology/users/<ID>`

### URL Parameters

| Parameter | Description                  |
| --------- | ---------------------------- |
| ID        | The ID of the user to delete |
