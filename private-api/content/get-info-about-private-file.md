---
description: /content/:id
---

# Get Info About Private File

This endpoint allows you to get information about a single file that is private. It DOES NOT return the actual file. That is handled by your [Dedicated Gateway](../../gateways/).

## Getting Info About Submarined File

{% swagger method="get" path="/content/:id" baseUrl="https://managed.mypinata.cloud/api/v1" summary="" expanded="true" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="id" required="true" %}
The ID of the content that is Private (not the CID). The ID for a file can be gained by using 

[/content](query-private-content.md)


{% endswagger-parameter %}

{% swagger-parameter in="header" name="x-api-key" required="true" %}
PRIVATE API KEY
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
  "status": 200,

  "totalItems": 0,
  "item": {
      "id": "string",
      "createdAt": "2022-05-20T19:33:36.340Z",
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
curl --location --request GET 'https://managed.mypinata.cloud/api/v1/content/95c904a0-4d61-4598-a4c8-fb5f0793c7ab' \
--header 'x-api-key: PRIVATE API KEY'
```
{% endtab %}

{% tab title="Node.js" %}
```javascript
var axios = require('axios');

var config = {
  method: 'get',
  url: 'https://managed.mypinata.cloud/api/v1/content/95c904a0-4d61-4598-a4c8-fb5f0793c7ab',
  headers: { 
    'x-api-key': 'PRIVATE API KEY'
  }
};

const res = await axios(config);

console.log(res.data);
```
{% endtab %}

{% tab title="Python" %}
```python
import requests

url = "https://managed.mypinata.cloud/api/v1/content/95c904a0-4d61-4598-a4c8-fb5f0793c7ab"

payload={}
headers = {
  'x-api-key': 'PRIVATE API KEY'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)

```
{% endtab %}

{% tab title="Go" %}
```go
package main

import (
  "fmt"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://managed.mypinata.cloud/api/v1/content/95c904a0-4d61-4598-a4c8-fb5f0793c7ab"
  method := "GET"

  client := &http.Client {
  }
  req, err := http.NewRequest(method, url, nil)

  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("x-api-key", "PRIVATE API KEY")

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
