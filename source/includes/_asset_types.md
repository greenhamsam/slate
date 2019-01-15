# Asset Types

_Update 15 Jan 2019: not yet implemented_

A dictionary of all available asset types, and arrays of the asset symbols included in that type.

```ruby
require 'appia'

api = Appia::APIClient.authorize!('mypersonalapikey')
api.assetTypes.get
```

```python
import appia

api = appia.authorize('mypersonalapikey')
api.assetTypes.get()
```

```shell
curl "http://example.com/api/assetTypes"
  -H "Authorization: mypersonalapikey"
```

```javascript
const appia = require("appia");

let api = appia.authorize("mypersonalapikey");
let assetTypes = api.assetTypes.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "assetType": "cryptocurrency",
    "assets": ["ETH", "BTC", "LTC"]
  }
  // More asset types //
]
```
