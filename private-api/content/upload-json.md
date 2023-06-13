---
description: /content/json
---

# Upload JSON

This endpoint allows you to upload any JSON object you wish. This endpoint is specifically optimized to only handle JSON content.&#x20;

## Uploading JSON

Each upload can optionally include additional information beyond just the file. Metadata in the form of a JSON object can be included. The metadata must be in the form of keyvalue pairs. Nesting of keyvalue pairs is not possible at this time.&#x20;

{% swagger method="post" path="/content/json" baseUrl="https://managed.mypinata.cloud/api/v1" summary="" expanded="true" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="x-api-key" required="true" %}
PRIVATE API KEY
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" required="false" %}
Name for JSON file
{% endswagger-parameter %}

{% swagger-parameter in="body" name="metadata" %}
Optional Metadata object
{% endswagger-parameter %}

{% swagger-parameter in="body" name="content" required="true" %}
The JSON content to pin
{% endswagger-parameter %}

{% swagger-parameter in="body" name="pinToIPFS" required="false" %}
False to make private
{% endswagger-parameter %}

{% swagger-parameter in="body" name="cidVersion" %}
0 or 1
{% endswagger-parameter %}

{% swagger-parameter in="body" name="wrapWithDirectory" %}
True to put JSON file inside a folder
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
  "status": 200,
  "statusText": "string",
  "totalItems": 0,
  "item": {
    "id": "string",
    "createdAt": "2022-05-20T20:01:26.679Z",
    "cid": "string",
    "name": "string",
    "mimeType": "string",
    "originalname": "string",
    "size": 0,
    "metadata": {},
    "pinToIPFS": false,
    "isDuplicate": false
  }
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request POST 'https://managed.mypinata.cloud/api/v1/content/json' \
--header 'x-api-key: PRIVATE API KEY' \
--header 'Content-Type: application/json' \
--data-raw '{
    "content": {
        "example": "content", 
        "more": "examples"
    }, 
    "name": "My JSON",
    "metadata": {
        "keyvalues": {
            "one": "two"
        }
    }
}'
```
{% endtab %}

{% tab title="Node.js" %}
```javascript
var axios = require('axios');
var data = JSON.stringify({
  "content": {
    "example": "content",
    "more": "examples"
  },
  "name": "My JSON",
  "metadata": {
    "keyvalues": {
      "one": "two"
    }
  }
});

var config = {
  method: 'post',
  url: 'https://managed.mypinata.cloud/api/v1/content/json',
  headers: { 
    'x-api-key': 'PRIVATE API KEY', 
    'Content-Type': 'application/json'
  },
  data : data
};

const res = await axios(config);

console.log(res.data);
```
{% endtab %}

{% tab title="Python" %}
```python
import requests
import json

url = "https://managed.mypinata.cloud/api/v1/content/json"

payload = json.dumps({
  "content": {
    "example": "content",
    "more": "examples"
  },
  "name": "My JSON",
  "metadata": {
    "keyvalues": {
      "one": "two"
    }
  }
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

  url := "https://managed.mypinata.cloud/api/v1/content/json"
  method := "POST"

  payload := strings.NewReader(`{
    "content": {
        "example": "content", 
        "more": "examples"
    }, 
    "name": "My JSON",
    "metadata": {
        "keyvalues": {
            "one": "two"
        }
    }
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
