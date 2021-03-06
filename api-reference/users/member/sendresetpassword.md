# 비밀번호 초기화 요청

## Request

```text
POST https://api.coolsms.co.kr/users/v1/member/password/reset
```

비밀번호 초기화 요청 메일을 보냅니다.

### Request Structure

```javascript
{
    "email": "email"
}
```

### Body Params

| Name | Type | Required | Description |
| :--- | :---: | :---: | :--- |
| email | `email` | O | 이메일 |

## Samples

### sendResetPassword.spec.js

> **Sample Request**

```javascript
{
    "email": "i@nter.net"
}
```

> **Sample Response**

```javascript
{
    "_id": "5f6ac5d147c7acc34a009b75",
    "email": "i@nter.net",
    "dateCreated": "2020-09-23T03:49:37.118Z",
    "dateUpdated": "2020-09-23T03:49:37.118Z",
    "hashId": "TzHlUFm5T0MYtH2otKe5U"
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
    email: 'i@nter.net'
  },
  method: 'POST',
  json: true,
  url: 'http://api.coolsms.co.kr/users/v1/member/password/reset'
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
$url = "http://api.coolsms.co.kr/users/v1/member/password/reset";
$data = '{"email":"i@nter.net"}';

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

url = "http://api.coolsms.co.kr/users/v1/member/password/reset"
headers = {
  "Content-Type": "application/json"
}
data = '{"email":"i@nter.net"}'

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
    -d '{"email":"i@nter.net"}' \
    http://api.coolsms.co.kr/users/v1/member/password/reset
```
{% endtab %}

{% tab title="RUBY" %}
```ruby
require 'net/http'
require 'uri'
require 'json'

uri = URI.parse("http://api.coolsms.co.kr/users/v1/member/password/reset")

headers = {
  "Content-Type": "application/json"
}
data = {
  "email": "i@nter.net"
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
  uri := "http://api.coolsms.co.kr/users/v1/member/password/reset"
  data := strings.NewReader(`{"email":"i@nter.net"}`)

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
    String targetUrl = "http://api.coolsms.co.kr/users/v1/member/password/reset";
    String parameters = "{\"email\":\"i@nter.net\"}";

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

