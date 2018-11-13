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