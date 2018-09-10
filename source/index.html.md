---
title: DEA API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - html
  - javascript
  - ruby
  - python
  - java 
  - go

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

DEA identification service
community project.
The repository for DEA information is emails.txt hosted at https://github.com/wesbos/burner-email-providers


# API reference

## Validate domain

> HTTP GET:

```Shell
curl "api/dea/check/{email}"
```

```html
GET /api/dea/check/{email} HTTP/1.1
Host: null

Accept: application/json
```

```javascript

var headers = {
  'Accept':'application/json'

};

$.ajax({
  url: '/api/dea/check/{email}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby

require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/dea/check/{email}',
  params: {
  }, headers: headers

p JSON.parse(result)


```

```python

import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/dea/check/{email}', params={

}, headers = headers)

print r.json()

```

```java

URL obj = new URL("/api/dea/check/{email}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go

package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},

    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/dea/check/{email}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> The above command returns JSON structured like this:

```json
{
  "doc":"https://github.com/wesbos/burner-email-providers",
  "query":"test@example.com",
  "result": {
    "isDisposable": true,
    "error":"e.g. no text supplied"
    }
}
```

### HTTP Request

`GET /api/dea/check/{email}`
<br/>
`POST /api/dea/check`

### Inputs

Input | Type | Description | Example Data
--------- | ----------- | ----------- | ----------
query | String (255, not null) | Input domain for checking against DEA domain list. | “example.com”

### Outputs

Output | Type | Description | Example Data
--------- | ----------- | ----------- | ----------
isDisposable | True/False | Output result from matching DEA domain list. | True
Error | String (255, null) | Output error if unable to validate | e.g. “No text supplied”

### Possible Error States

Error type | Text 
--------- | ----------- 
NoText | True/False 
EmailAddressSupplied | String (255, null)
QueryTooLong | True/False 

### Input validation

Condition | Action |  Description | Example
--------- | ------ | ------------ | -------
No text | Generate error state “NoText” | Verify that input is supplied | “”
Query too long | Generate error state “QueryTooLong” | Verify that input < MaxAllowed | “[>255 characters in length]”
Email address supplied | Generate error state “EmailAddressSupplied” | Verify data isn't an email address | “anyone@example.com”