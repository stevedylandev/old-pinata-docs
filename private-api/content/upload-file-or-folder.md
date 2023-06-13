---
description: /content
---

# Upload File or Folder

This endpoint will accept a single file or a single directory. The request must include a read stream for the payload in order for the API to accept it.&#x20;

## Uploading a Single File

Each upload can optionally include additional information beyond just the file. Metadata in the form of a JSON object can be included. The metadata must be in the form of keyvalue pairs. Nesting of keyvalue pairs is not possible at this time.&#x20;

{% swagger method="post" path="/content" baseUrl="https://managed.mypinata.cloud/api/v1" summary="" expanded="true" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="x-api-key" required="true" %}
PRIVATE API KEY
{% endswagger-parameter %}

{% swagger-parameter in="body" name="files" required="true" %}
Read stream representing the file
{% endswagger-parameter %}

{% swagger-parameter in="body" name="metadata" %}
Optional stringified object
{% endswagger-parameter %}

{% swagger-parameter in="body" name="cidVersion" %}
0 or 1 to represent the IPFS protocol CID version
{% endswagger-parameter %}

{% swagger-parameter in="body" name="wrapWithDirectory" %}
Wrap a single file into a folder if set to true
{% endswagger-parameter %}

{% swagger-parameter in="body" name="pinToIPFS" required="true" %}
False to make file private
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" %}
Optional name for file
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
  "status": 200,
  "totalItems": 0,
  "items": [
    {
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
  ]
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request POST 'https://managed.mypinata.cloud/api/v1/content' \
--header 'x-api-key: PRIVATE API KEY' \
--form 'files=@"/Users/Desktop/images/cat.svg"' \
--form 'name="My File"' \
--form 'metadata="{\"keyvalues\": { \"example\": \"value\" }}"' \
--form 'wrapWithDirectory="false"' \
--form 'pinToIPFS="false"'
```
{% endtab %}

{% tab title="Node.js" %}
```javascript
var axios = require('axios');
var FormData = require('form-data');
var fs = require('fs');
var data = new FormData();
data.append('files', fs.createReadStream('/Users/Desktop/images/cat.svg'));
data.append('name', 'My File');
data.append('metadata', '{"keyvalues": { "example": "value" }}');
data.append('wrapWithDirectory', 'false');
data.append('pinToIPFS', 'false');

var config = {
  method: 'post',
  url: 'https://managed.mypinata.cloud/api/v1/content',
  headers: { 
    'x-api-key': 'PRIVATE API KEY', 
    ...data.getHeaders()
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

url = "https://managed.mypinata.cloud/api/v1/content"

payload={'name': 'My File',
'metadata': '{"keyvalues": { "example": "value" }}',
'wrapWithDirectory': 'false',
'pinToIPFS': 'false'}
files=[
  ('files',('Submarine-Beta_Standard.svg',open('/Users/Desktop/images/cat.svg','rb'),'image/svg+xml'))
]
headers = {
  'x-api-key': 'PRIVATE API KEY'
}

response = requests.request("POST", url, headers=headers, data=payload, files=files)

print(response.text)

```
{% endtab %}

{% tab title="Go" %}
```go
package main

import (
  "fmt"
  "bytes"
  "mime/multipart"
  "os"
  "path/filepath"
  "io"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://managed.mypinata.cloud/api/v1/content"
  method := "POST"

  payload := &bytes.Buffer{}
  writer := multipart.NewWriter(payload)
  file, errFile1 := os.Open("/Users/Desktop/images/cat.svg")
  defer file.Close()
  part1,
         errFile1 := writer.CreateFormFile("files",filepath.Base("/Users/Desktop/images/cat.svg"))
  _, errFile1 = io.Copy(part1, file)
  if errFile1 != nil {
    fmt.Println(errFile1)
    return
  }
  _ = writer.WriteField("name", "My File")
  _ = writer.WriteField("metadata", "{\"keyvalues\": { \"example\": \"value\" }}")
  _ = writer.WriteField("wrapWithDirectory", "false")
  _ = writer.WriteField("pinToIPFS", "false")
  err := writer.Close()
  if err != nil {
    fmt.Println(err)
    return
  }


  client := &http.Client {
  }
  req, err := http.NewRequest(method, url, payload)

  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("x-api-key", "PRIVATE API KEY")

  req.Header.Set("Content-Type", writer.FormDataContentType())
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

## Uploading a Directory

This endpoint also allows users to upload an entire directory as well. This works almost identically to pinning a file, with the main difference being that we provide an array of files and need to provide a relative file path for each file in the directory.

However, our servers will use the exact path that's provided for each file, so it's important that each path begins with the "base" directory that is being uploaded. As an example, if your directory is located at "./../myBuilds/desiredBuild" on your local machine, then each file path should start with "desiredBuild".

We have a JavaScript example of uploading a directory below. Note that in the example, we use the `got` library instead of `axios`, but the same general procedure can be applied using `axios` or any other library.&#x20;

```javascript
const fs = require("fs");
const FormData = require("form-data");
const rfs = require("recursive-fs");
const basePathConverter = require("base-path-converter");
const got = require('got');

const submarineDirectory = async () => {
  const url = `https://managed.mypinata.cloud/api/v1/content`;
  const src = "RELATIVE PATH TO DIRECTORY TO UPLOAD";
  var status = 0;
  try {
    const { dirs, files } = await rfs.read(src);
    let data = new FormData();
    for (const file of files) {
      data.append(`file`, fs.createReadStream(file), {
        filepath: basePathConverter(src, file),
      });
    }    
    const response = await got(url, {
      method: 'POST',
      headers: {
        "Content-Type": `multipart/form-data; boundary=${data._boundary}`,
        "x-api-key": "PRIVATE API KEY"
      },
      body: data
  })		
		.on('uploadProgress', progress => {
			console.log(progress);
		});

	console.log(JSON.parse(response.body));
  } catch (error) {
    console.log(error);
  }
};
view raw
```
