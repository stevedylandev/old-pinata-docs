---
description: /content/:id
---

# Update File Info/Make Public

This endpoint can be used to update information about a private file, and it can be used to move the file to the public IPFS network.&#x20;

{% hint style="warning" %}
**The Private API currently does not provide progress updates when making files public, and the process can take a very long time**
{% endhint %}

## Updating Submarined File

{% swagger method="put" path="/api/v1/content/:id" baseUrl="https://managed.mypinata.cloud" summary="" expanded="true" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="x-api-key" required="true" %}
PRIVATE API KEY
{% endswagger-parameter %}

{% swagger-parameter in="path" name="id" required="true" %}
ID of the file (not CID)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="pinToIPFS" %}
Set to true if you want to move the file to the public IPFS network
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" %}
Updated name for the file
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
curl --location --request PUT 'https://managed.mypinata.cloud/api/v1/content/95c904a0-4d61-4598-a4c8-fb5f0793c7ab' \
--header 'x-api-key: PRIVATE API KEY' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "New Name", 
    "pinToIPFS": true
}'
```
{% endtab %}

{% tab title="Node.js" %}
```javascript
var axios = require('axios');
var data = JSON.stringify({
  "name": "New Name",
  "pinToIPFS": true
});

var config = {
  method: 'put',
  url: 'https://managed.mypinata.cloud/api/v1/content/95c904a0-4d61-4598-a4c8-fb5f0793c7ab',
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

url = "https://managed.mypinata.cloud/api/v1/content/95c904a0-4d61-4598-a4c8-fb5f0793c7ab"

payload = json.dumps({
  "name": "New Name",
  "pinToIPFS": True
})
headers = {
  'x-api-key': 'PRIVATE API KEY',
  'Content-Type': 'application/json'
}

response = requests.request("PUT", url, headers=headers, data=payload)

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

  url := "https://managed.mypinata.cloud/api/v1/content/95c904a0-4d61-4598-a4c8-fb5f0793c7ab"
  method := "PUT"

  payload := strings.NewReader(`{
    "name": "New Name", 
    "pinToIPFS": true
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
