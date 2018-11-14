# Events

A log of all of the events that change the values of any account in the system. What occured, at what time, for what user. These events are things like: a transaction or trade was initiated, processed, rejected, failed or reversed. A new account was created or deleted.

```ruby
require 'appia'

api = Appia::APIClient.authorize!('mypersonalapikey')
api.events.get
```

```python
import appia

api = appia.authorize('mypersonalapikey')
api.events.get()
```

```shell
curl "http://example.com/api/events"
  -H "Authorization: mypersonalapikey"
```

```javascript
const appia = require('appia');

let api = appia.authorize('mypersonalapikey');
let events = api.events.get();
```

> The above command returns JSON structured like this:

```json

[
  {
    "id": 12345678,
    "user": 12345678,
    "time": "2012-04-23T18:25:43.511Z",
    "event": "New account linked",
  },
  // More events //
]
