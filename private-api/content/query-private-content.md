---
description: /content
---

# Query Private Content

This endpoint returns data on what content you have uploaded as private through Pinata.

The results of this call can be filtered using multiple query parameters that will be discussed below.

## Querying Submarined Files

{% swagger method="get" path="/content" baseUrl="https://managed.mypinata.cloud/api/v1" summary="" expanded="true" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="x-api-key" required="true" %}
PRIVATE API KEY
{% endswagger-parameter %}

{% swagger-parameter in="query" name="cidContains" %}
CID of file you are searching for
{% endswagger-parameter %}

{% swagger-parameter in="query" name="createdAtStart" %}
ISO_8601 format date to filter by start date for when file was Submarined
{% endswagger-parameter %}

{% swagger-parameter in="query" name="createdAtEnd" %}
ISO_8601 format date to filter by end date for when file was Submarined
{% endswagger-parameter %}

{% swagger-parameter in="query" name="originalname" %}
The original file name from the file system
{% endswagger-parameter %}

{% swagger-parameter in="query" name="pinSizeMin" %}
Minimum size in bytes of files to return
{% endswagger-parameter %}

{% swagger-parameter in="query" name="pinSizeMax" %}
Maximum size in bytes of files to return
{% endswagger-parameter %}

{% swagger-parameter in="query" name="status" %}
Options are "all", "pinned", or "unpinned"
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" %}
Maximum number of files to return. Default is 10, max is 1000
{% endswagger-parameter %}

{% swagger-parameter in="query" name="offset" %}
Use to paginate through files, default is 0
{% endswagger-parameter %}

{% swagger-parameter in="query" name="metadata" %}
See metadata querying section below
{% endswagger-parameter %}

{% swagger-parameter in="query" name="order" %}
Property (any of the query params above) to order results by
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
  "status": 200,

  "totalItems": 0,
  "items": [
    {
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
  ]
}
```
{% endswagger-response %}
{% endswagger %}



### Metadata Querying

You also have the option to query your content on the associated metadata that may have been included with the content when it was uploaded through either the [PinFileToIPFS](broken-reference) or [PinJSONToIPFS](broken-reference) endpoints.

These queries look very similar to the default parameters but are slightly more complex.

Here are few simple examples, with added explanation afterward.

**To query on the name you provided for your pin, your query would take this form:**

`?metadata[name]=exampleName`

(this will match on names that contain the string of characters provided as a value. For added specificity, please include the full name you're trying to find).

**To query on the metadata key-value attributes:**

`?metadata[keyvalues]={"exampleKey":{"value":"exampleValue","op":"exampleOp"}}`

Or:

`?metadata[keyvalues][exampleKey]={"value":"exampleValue","op":"exampleOp"}`

**To query on both the metadata name and multiple key-value attributes:**

`?metadata[name]=exampleName&metadata[keyvalues]={"exampleKey":{"value":"exampleValue","op":"exampleOp"},"exampleKey2":{"value":"exampleValue2","op":"exampleOp2"}}`

**Explaining the "value" and "op" key / values**

As seen above, each query on custom values takes the form of an object with a "value" key and an "op" key.

The "value" is fairly straightforward. This is simply the value that you wish your query operation to be applied to. These values can be:

* Strings
* Numbers (integers or decimals)
* Dates (Provided in ISO\_8601 format)

The "op" is what query operation will be applied to the value you provided. The following opcodes are available to query with:

* "gt" - (greater than)
* "gte" - (greater than or equal)
* "lt" - (less than)
* "lte" - (less than or equal)
* "ne" - (not equal to)
* "eq" - (equal to)
* "between" - (When querying with the 'between' operation, you need to supply a 'secondValue' to be consumed by the query operation)

For Example:

`?metadata[keyvalues]={"exampleKey":{"value":"2018-01-01 00:00:00.000+00","secondValue":"2018-02-01 00:00:00.000+00","op":"between"}}`

* "notBetween" - (When querying with the 'notBetween' operation, you need to supply a 'secondValue' to be consumed by the query operation)

For Example:

`?metadata[keyvalues]={"exampleKey":{"value":4.00,"secondValue":5.50,"op":"notBetween"}}`

* "like" - (you can use this to find values that are similar to what you've passed in)

For example, this query would find all entries that begin with "testValue". A `%` before your value means anything can come before it, and a `%` sign after means any characters can come after it. So `%testValue%` would contain all entries containing the characters "testValue".

`?metadata[keyvalues]={"exampleKey":{"value":"testValue%","op":"like"}}`

* "notLike" - (you can use this to find values that do not contain the character string you've passed in)
* "iLike" - (The case insensitive version of the "like" opcode)
* "notILike" - (The case insensitive version of the "notLike" opcode)
* "regexp" - (Regular expression matching)
* "iRegexp" - (Case insensitive regular expression matching)

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request GET 'https://managed.mypinata.cloud/api/v1/content?createdAtStart=2022-01-01T06:00:00.000Z&pinSizeMin=100' \
--header 'x-api-key: PRIVATE API KEY'
```
{% endtab %}

{% tab title="Node.js" %}
```javascript
var axios = require('axios');

var config = {
  method: 'get',
  url: 'https://managed.mypinata.cloud/api/v1/content?createdAtStart=2022-01-01T06:00:00.000Z&pinSizeMin=100',
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

url = "https://managed.mypinata.cloud/api/v1/content?createdAtStart=2022-01-01T06:00:00.000Z&pinSizeMin=100"

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

  url := "https://managed.mypinata.cloud/api/v1/content?createdAtStart=2022-01-01T06:00:00.000Z&pinSizeMin=100"
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
