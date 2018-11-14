# Assets

A dictionary of all available assets.

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
    "symbol": "ETH",
    "name": "Ethereum",
    "assetType": "cryptocurrency",
  },
  // More assets //
]
```