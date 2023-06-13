---
description: /auth/content/jwt
---

# Generate Access Token

This endpoint allows you to create an access token that will be used for viewing private content through a Dedicated Gateway. The token is time-limited, and you control the time through this endpoint.&#x20;

## Generating an Access Token

{% swagger method="post" path="/auth/content/jwt" baseUrl="https://managed.mypinata.cloud/api/v2" summary="" expanded="true" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="x-api-key" required="true" %}
PRIVATE API KEY
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timeoutSeconds" required="true" %}
Number of seconds the access token should be valid for
{% endswagger-parameter %}

{% swagger-parameter in="body" name="contentIds" required="true" %}
Stringified array of IDs (not CIDs) for files
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
"TOKEN"
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request POST 'https://managed.mypinata.cloud/api/v1/auth/content/jwt' \
--header 'x-api-key: PRIVATE API KEY' \
--header 'Content-Type: application/json' \
--data-raw '{
    "timeoutSeconds": 3600,
    "contentIds": ["95c904a0-4d61-4598-a4c8-fb5f0793c7ab"]
}'
```
{% endtab %}

{% tab title="Node.js" %}
```javascript
var axios = require('axios');
var data = JSON.stringify({
  "timeoutSeconds": 3600,
  "contentIds": [
    "95c904a0-4d61-4598-a4c8-fb5f0793c7ab"
  ]
});

var config = {
  method: 'post',
  url: 'https://managed.mypinata.cloud/api/v1/auth/content/jwt',
  headers: { 
    'x-api-key': 'PRIVATE API KEY', 
    'Content-Type': 'application/json'
  },
  data: data
};

const res = await axios(config);

console.log(res.data);
```
{% endtab %}

{% tab title="Python" %}
```python
import requests
import json

url = "https://managed.mypinata.cloud/api/v1/auth/content/jwt"

payload = json.dumps({
  "timeoutSeconds": 3600,
  "contentIds": [
    "95c904a0-4d61-4598-a4c8-fb5f0793c7ab"
  ]
})
headers = {
  'x-api-key': 'PRIVATE API KEY',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)

```
{% endtab %}

{% tab title="Go" %}
```go
package main

import (
  "fmt"
  "strings"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://managed.mypinata.cloud/api/v1/auth/content/jwt"
  method := "POST"

  payload := strings.NewReader(`{
    "timeoutSeconds": 3600,
    "contentIds": ["95c904a0-4d61-4598-a4c8-fb5f0793c7ab"]
}`)

  client := &http.Client {
  }
  req, err := http.NewRequest(method, url, payload)

  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("x-api-key", "PRIVATE API KEY")
  req.Header.Add("Content-Type", "application/json")

  res, err := client.Do(req)
  if err != nil {
    fmt.Println(err)
    return
  }
  defer res.Body.Close()

  body, err := ioutil.ReadAll(res.Body)
  if err != nil {
    fmt.Println(err)
    return
  }
  fmt.Println(string(body))
}
```
{% endtab %}
{% endtabs %}
