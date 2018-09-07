---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - html

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

```shell
curl "api/dea/check/{email}"
```

```html
GET /api/dea/check/{email} HTTP/1.1
Host: null

Accept: application/json
```

> HTTP POST:


```shell
curl "api/dea/check"
```

```html
GET /api/dea/check HTTP/1.1
Host: null

Accept: application/json
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