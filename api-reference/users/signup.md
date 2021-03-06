# 회원가입

## Request

```text
POST https://api.coolsms.co.kr/users/v1/signup
```

ReCAPTCHA 인증을 포함한 회원가입 절차입니다.

### Request Structure

```javascript
{
    "email": "email",
    "password": "string",
    "passwordConfirmation": "string",
    "captcha": "string",
    "marketerAccountId": "string",
    "name": "string"
}
```

### Body Params

| Name | Type | Required | Description |
| :--- | :---: | :---: | :--- |
| email | `email` | O | 이메일 |
| password | `string` | O | 비밀번호 |
| passwordConfirmation | `string` | O | 비밀번호 확인 |
| captcha | `string` | O | ReCAPTCHA 인증 코드 |
| marketerAccountId | `string` |  | 설명 없음 |
| name | `string` |  | 이름 |

## Samples

### signup.spec.js

> **Sample Request**

```javascript
{
    "email": "test1@nurigo.net",
    "password": "asd123!",
    "passwordConfirmation": "asd123!",
    "captcha": "DUMMY"
}
```

> **Sample Response**

```javascript
{
    "account": {
        "status": "ACTIVE",
        "accountId": "20092346177374",
        "name": "test1님의 계정",
        "members": [
            {
                "dateCreated": "2020-09-23T03:49:34.870Z",
                "dateUpdated": "2020-09-23T03:49:34.870Z",
                "memberId": "MEM0vLVIRYaMXk",
                "role": "OWNER",
                "name": "test1"
            }
        ],
        "dateCreated": "2020-09-23T03:49:37.685Z",
        "dateUpdated": "2020-09-23T03:49:37.685Z"
    },
    "member": {
        "name": "test1",
        "phoneNumber": null,
        "extraPhoneNumbers": [],
        "status": "UNVERIFIED",
        "selectedAccountId": "20092346177374",
        "betaMicroservices": null,
        "appId": null,
        "memberId": "MEM0vLVIRYaMXk",
        "email": "test1@nurigo.net",
        "loginSessions": [],
        "dateCreated": "2020-09-23T03:49:37.680Z",
        "dateUpdated": "2020-09-23T03:49:37.682Z"
    }
}
```

> **Sample Code**

{% tabs %}
{% tab title="NODE" %}
```javascript
var request = require('request');

var options = {
  headers: {
    'Content-Type': 'application/json'
  },
  body: {
    email: 'test1@nurigo.net',
    password: 'asd123!',
    passwordConfirmation: 'asd123!',
    captcha: 'DUMMY'
  },
  method: 'POST',
  json: true,
  url: 'http://api.coolsms.co.kr/users/v1/signup'
};

request(options, function(error, response, body) {
  if (error) throw error;
  console.log('result :', body);
});
```
{% endtab %}

{% tab title="PHP" %}
```php
<?php
$url = "http://api.coolsms.co.kr/users/v1/signup";
$data = '{"email":"test1@nurigo.net","password":"asd123!","passwordConfirmation":"asd123!","captcha":"DUMMY"}';

$options = array(
    'http' => array(
        'header'  => "Content-Type: application/json\r\n",
        'content' => $data,
        'method'  => 'POST'
    )
);

$context  = stream_context_create($options);
$result = file_get_contents($url, false, $context);

var_dump($result);
```
{% endtab %}

{% tab title="PYTHON" %}
```python
import requests

url = "http://api.coolsms.co.kr/users/v1/signup"
headers = {
  "Content-Type": "application/json"
}
data = '{"email":"test1@nurigo.net","password":"asd123!","passwordConfirmation":"asd123!","captcha":"DUMMY"}'

response = requests.post(url, headers=headers, data=data)
print(response.status_code)
print(response.text)
```
{% endtab %}

{% tab title="CURL" %}
```text
#!/bin/bash
curl -X POST \
    -H 'Content-Type: application/json' \
    -d '{"email":"test1@nurigo.net","password":"asd123!","passwordConfirmation":"asd123!","captcha":"DUMMY"}' \
    http://api.coolsms.co.kr/users/v1/signup
```
{% endtab %}

{% tab title="RUBY" %}
```ruby
require 'net/http'
require 'uri'
require 'json'

uri = URI.parse("http://api.coolsms.co.kr/users/v1/signup")

headers = {
  "Content-Type": "application/json"
}
data = {
  "email": "test1@nurigo.net",
  "password": "asd123!",
  "passwordConfirmation": "asd123!",
  "captcha": "DUMMY"
}
http = Net::HTTP.new(uri.host, uri.port)
request = Net::HTTP::Post.new(uri.request_uri, headers)
request.body = data.to_json

response = http.request(request)
puts response.code
puts response.body
```
{% endtab %}

{% tab title="GO" %}
```go
package main

import (
  "fmt"
  "io/ioutil"
  "net/http"
  "strings"
)

func main() {
  uri := "http://api.coolsms.co.kr/users/v1/signup"
  data := strings.NewReader(`{"email":"test1@nurigo.net","password":"asd123!","passwordConfirmation":"asd123!","captcha":"DUMMY"}`)

  req, err := http.NewRequest("POST", uri, data)
  if err != nil { panic(err) }

  req.Header.Set("Content-Type", "application/json")

  client := &http.Client{}
  resp, err := client.Do(req)
  if err != nil { panic(err) }
  defer resp.Body.Close()

  bytes, _ := ioutil.ReadAll(resp.Body)
  str := string(bytes)
  fmt.Println(str)
}
```
{% endtab %}

{% tab title="JAVA" %}
```java
package solapi;

import java.io.BufferedReader;
import java.io.DataOutputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Request {
  public static void main(String[] args) throws Exception {
    String targetUrl = "http://api.coolsms.co.kr/users/v1/signup";
    String parameters = "{\"email\":\"test1@nurigo.net\",\"password\":\"asd123!\",\"passwordConfirmation\":\"asd123!\",\"captcha\":\"DUMMY\"}";

    URL url = new URL(targetUrl);
    HttpURLConnection con = (HttpURLConnection) url.openConnection();

    con.setRequestMethod("POST");

    con.setRequestProperty("Content-Type", "application/json");

    con.setDoOutput(true);
    DataOutputStream wr = new DataOutputStream(con.getOutputStream());
    wr.writeBytes(parameters);
    wr.flush();
    wr.close();

    int responseCode = con.getResponseCode();
    BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
    String line;
    StringBuffer response = new StringBuffer();
    while ((line = in.readLine()) != null) {
      response.append(line);
    }
    in.close();

    System.out.println("HTTP response code : " + responseCode);
    System.out.println("HTTP body : " + response.toString());
  }
}
```
{% endtab %}
{% endtabs %}

> 문서 생성일 : 2020-09-23

