# 웹훅 추가

## Request

```text
POST https://api.coolsms.co.kr/webhook/v1/outgoing
```

사용할 이벤트, URL과 함께 웹훅을 추가합니다.

### Authorization 인증 필요 [\[?\]](https://docs.coolsms.co.kr/authentication/overview#authorization)

| 계정 권한 | 회원 권한 | 계정 상태 | 회원 상태 | 계정 인증 |
| :--- | :--- | :--- | :--- | :---: |
| `webhook:write` | `role-webhook:write` | `ACTIVE` | `ACTIVE` | O |

### 2차 인증 필요

| ARS 전화 인증 | 이메일 OTP |
| :---: | :---: |
|  |  |

### Request Structure

```javascript
{
    "eventId": "string",
    "url": "string",
    "secret": "string"
}
```

### Body Params

| Name | Type | Required | Description |
| :--- | :---: | :---: | :--- |
| eventId | `string` | O | 설명 없음 |
| url | `string` | O | 설명 없음 |
| secret | `string` |  | 설명 없음 |

## Samples

### createOutgoingData.spec.js

> **Sample Request**

```javascript
{
    "eventId": "WH01ET191230002851182aHyWVJXqNhn",
    "url": "https://coolsms.co.kr/report"
}
```

> **Sample Response**

```javascript
{
    "secret": null,
    "status": "ACTIVE",
    "failCount": 0,
    "accountId": "12925149",
    "eventId": "WH01ET191230002851182aHyWVJXqNhn",
    "url": "https://coolsms.co.kr/report",
    "webhookId": "WH01WH191230002851549Lnnn7bv8wEr",
    "dateCreated": "2019-12-30T00:28:51.557Z",
    "dateUpdated": "2019-12-30T00:28:51.557Z"
}
```

> **Sample Code**

{% tabs %}
{% tab title="NODE" %}
```javascript
var request = require('request');

var options = {
  headers: {
    Authorization:
      'HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4',
    'Content-Type': 'application/json'
  },
  body: {
    eventId: 'WH01ET191230002851182aHyWVJ...',
    url: 'https://coolsms.co.kr/report'
  },
  method: 'POST',
  json: true,
  url: 'http://api.coolsms.co.kr/webhook/v1/outgoing'
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
$url = "http://api.coolsms.co.kr/webhook/v1/outgoing";
$data = '{"eventId":"WH01ET191230002851182aHyWVJ...","url":"https://coolsms.co.kr/report"}';

$options = array(
    'http' => array(
        'header'  => "Authorization: HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4\r\n" . "Content-Type: application/json\r\n",
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

url = "http://api.coolsms.co.kr/webhook/v1/outgoing"
headers = {
  "Authorization": "HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4",
  "Content-Type": "application/json"
}
data = '{"eventId":"WH01ET191230002851182aHyWVJ...","url":"https://coolsms.co.kr/report"}'

response = requests.post(url, headers=headers, data=data)
print(response.status_code)
print(response.text)
```
{% endtab %}

{% tab title="CURL" %}
```text
#!/bin/bash
curl -X POST \
    -H 'Authorization: HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4' \
    -H 'Content-Type: application/json' \
    -d '{"eventId":"WH01ET191230002851182aHyWVJ...","url":"https://coolsms.co.kr/report"}' \
    http://api.coolsms.co.kr/webhook/v1/outgoing
```
{% endtab %}

{% tab title="RUBY" %}
```ruby
require 'net/http'
require 'uri'
require 'json'

uri = URI.parse("http://api.coolsms.co.kr/webhook/v1/outgoing")

headers = {
  "Authorization": "HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4",
  "Content-Type": "application/json"
}
data = {
  "eventId": "WH01ET191230002851182aHyWVJ...",
  "url": "https://coolsms.co.kr/report"
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
  uri := "http://api.coolsms.co.kr/webhook/v1/outgoing"
  data := strings.NewReader(`{"eventId":"WH01ET191230002851182aHyWVJ...","url":"https://coolsms.co.kr/report"}`)

  req, err := http.NewRequest("POST", uri, data)
  if err != nil { panic(err) }

  req.Header.Set("Authorization", "HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4")
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
package coolsms;

import java.io.BufferedReader;
import java.io.DataOutputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Request {
  public static void main(String[] args) throws Exception {
    String targetUrl = "http://api.coolsms.co.kr/webhook/v1/outgoing";
    String parameters = "{\"eventId\":\"WH01ET191230002851182aHyWVJ...\",\"url\":\"https://coolsms.co.kr/report\"}";

    URL url = new URL(targetUrl);
    HttpURLConnection con = (HttpURLConnection) url.openConnection();

    con.setRequestMethod("POST");

    con.setRequestProperty("Authorization", "HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4");
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

> 문서 생성일 : 2019-12-30

