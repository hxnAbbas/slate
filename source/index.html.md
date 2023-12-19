---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='#'>Documentation Powered by BerryTalks</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the BerryTalks API
---



# Introduction

Welcome to the BerryTalks API! You can use our API to access API endpoints, which can get information for various API's.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.


# Authenticate
> All these apis are private protect by Security token, Use these Api to get token:


| Parameter | REQUIRED | Description                            |
|-----------|----------|----------------------------------------|
| email     | true     | Agent Email provided by BerryTalks.    |
| password  | true     | Agent Password provided by BerryTalks. |


```ruby
require 'uri'
require 'net/http'

url = URI("{BASE_URL}/auth/client/login")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Post.new(url)
request["cookie"] = 'JSESSIONID=C443CDB2B1C66D02F5E0A0683ADB357E'
request["Content-Type"] = 'application/json'
request["User-Agent"] = 'insomnia/2023.5.8'
request.body = { "email": "EMAIL_ADDRESS", "password": "PASSWORD"  }

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPConnection("localhost:8080")

payload = { "email": "EMAIL_ADDRESS",  "password": "PASSWORD" }

headers = {
    'cookie': "JSESSIONID=C443CDB2B1C66D02F5E0A0683ADB357E",
    'Content-Type': "application/json",
    'User-Agent': "insomnia/2023.5.8"
    }

conn.request("POST", "/auth/client/login", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```shell
curl --request POST \
  --url {BASE_URL}/auth/client/login \
  --header 'Content-Type: application/json' \
  --header 'User-Agent: insomnia/2023.5.8' \
  --cookie JSESSIONID=C443CDB2B1C66D02F5E0A0683ADB357E \
  --data '{
    "email": "EMAIL_ADDRESS",
    "password": "PASSWORD"
}'
```

```javascript
const data = JSON.stringify({
  "email": "EMAIL_ADDRESS",
  "password": "PASSWORD"
});

const xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === this.DONE) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "{BASE_URL}/auth/client/login");
xhr.setRequestHeader("cookie", "JSESSIONID=C443CDB2B1C66D02F5E0A0683ADB357E");
xhr.setRequestHeader("Content-Type", "application/json");
xhr.setRequestHeader("User-Agent", "insomnia/2023.5.8");

xhr.send(data);
```


```json
{
  "status": 1,
  "message": null,
  "data": {
    "token": "eyJhbGciOiJIUzI1NiJ9.....",
    "type": "Bearer",
    "userDataResponses": null,
    "accessToken": "eyJhbGciOiJIUzI1NiJ9....."
  }
}
```


# Send OTP Template

> To Send OTP Template , use this code:

| Parameter     | REQUIRED | Description                                    |
|---------------|----------|------------------------------------------------|
| to            | true     | Number you want to send message.               |
| templateId    | true     | Template ID of your template.                  |
| param         | true     | Param is Json Object of your array.            |
| type          | true     | Type of parameter of component "text/image".   |
| value         | true     | OTP code to send with API.                     |
| componentType | true     | Type of Component "body/header/footer/button". |
| buttonType    | true     | if template contain button, "quick_reply/Url"  |

```ruby
require 'uri'
require 'net/http'

url = URI("{BASE_URL}/broadcast/send")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Post.new(url)
request["cookie"] = 'JSESSIONID=C443CDB2B1C66D02F5E0A0683ADB357E'
request["Content-Type"] = 'application/json'
request["User-Agent"] = 'insomnia/2023.5.8'
request["Authorization"] = 'Bearer eyJhbGciOiJIUzI1NiJ9....'
request.body = "{"to" : "NUMBER","templateId" : "TEMPLATE_NUMBER","param" :[{ "type" :"text", "value" : "OTP_CODE", "componentType" : "body" }, { "type " : "text", "value" : "OTP_CODE","componentType" :"button","buttonType" : "url" }]}"

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPConnection("localhost:8080")

payload = {"to" : "NUMBER","templateId" : "TEMPLATE_NUMBER","param" :[{ "type" :"text", "value" : "OTP_CODE", "componentType" : "body" }, { "type " : "text", "value" : "OTP_CODE","componentType" :"button","buttonType" : "url" }]}

headers = {
    'cookie': "JSESSIONID=C443CDB2B1C66D02F5E0A0683ADB357E",
    'Content-Type': "application/json",
    'User-Agent': "insomnia/2023.5.8",
    'Authorization': "Bearer eyJhbGciOiJIUzI1NiJ9...."
    }

conn.request("POST", "/broadcast/send", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```shell
# With shell, you can just pass the correct header with each request
curl --request POST \
  --url {BASE_URL}/broadcast/send \
  --header 'Authorization: Bearer eyJhbGciOiJIUzI1....' \
  --header 'Content-Type: application/json' \
  --header 'User-Agent: insomnia/2023.5.8' \
  --cookie JSESSIONID=C443CDB2B1C66D02F5E0A0683ADB357E \
  --data '{
	"to" : "RECIPIENT_NUMBER",
	"templateId" : "TEMPLATE_ID",
	 "param" :[{
		 "type" :"text",
		 "value" : "YOUR_OTP_CODE",
		 "componentType" :"body"
		 
	 },
	{
		 "type" :"text",
		 "value" : "YOUR_OTP_CODE",
		 "componentType" :"button",
		 "buttonType" : "url"
		 
	 }]
}'
```

```javascript
const data = JSON.stringify({
  "to": "NUMBER",
  "templateId": "TEMPLATE_NUMBER",
  "param": [
    {
      "type": "text",
      "value": "OTP_CODE",
      "componentType": "body"
    },
    {
      "type": "text",
      "value": "OTP_CODE",
      "componentType": "button",
      "buttonType": "url"
    }
  ]
});

const xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === this.DONE) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "{BASE_URL}/broadcast/send");
xhr.setRequestHeader("cookie", "JSESSIONID=C443CDB2B1C66D02F5E0A0683ADB357E");
xhr.setRequestHeader("Content-Type", "application/json");
xhr.setRequestHeader("User-Agent", "insomnia/2023.5.8");
xhr.setRequestHeader("Authorization", "Bearer eyJhbGciOiJIUzI1NiJ9....");

xhr.send(data);
```

> Make sure to replace `eyJhbGciOiJIUzI1NiJ9....` with your Token.
