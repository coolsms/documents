# 발신번호 중복 해제 요청

## Request

```text
POST https://api.coolsms.co.kr/senderid/v1/papers/duplicate/:phoneNumber
```

발신번호 상태가 중복\('DUPLICATED'\)일 경우 중복 해제를 위한 요청입니다.

### Authorization 인증 필요 [\[?\]](https://docs.coolsms.co.kr/authentication/authentication)

| 계정 권한 | 회원 권한 | 계정 상태 | 회원 상태 | 계정 인증 |
| :--- | :--- | :--- | :--- | :---: |
| `senderid:write` | `role-senderid:write` | `ACTIVE` | `ACTIVE` | O |

### Path Parameters

| Name | Description |
| :---: | :---: |
| :phoneNumber | 핸드폰 번호 |

### Request Structure

```javascript
{
    "reason": "string",
    "name": "string"
}
```

### Body Params

| Name | Type | Required | Description |
| :--- | :---: | :---: | :--- |
| reason | `string` | O | 중복 해제 이유 |
| name | `string` |  | 이름 |

## Samples

### createDuplicateSenderIds.spec.js

> **Sample Request**

```javascript
{
    "reason": "부서에 따른 아이디 할당을 위해 필요"
}
```

> **Sample Response**

```javascript
{
    "limit": 2,
    "accountId": "12925149",
    "senderIds": [
        {
            "unlockDuplicate": {
                "duplicateId": "DUP20191029025925BPD1RFEHPNUKU50",
                "reason": null,
                "reasonForRequested": "부서에 따른 아이디 할당을 위해 필요",
                "name": null,
                "status": "PENDING",
                "dateCreated": "2019-10-28T17:59:25.756Z",
                "dateUpdated": "2019-10-28T17:59:25.756Z"
            },
            "status": "PENDING",
            "expireAt": null,
            "method": null,
            "log": [
                {
                    "createAt": "2019-10-28T17:59:25.756Z",
                    "message": "중복 해제 요청을 하였습니다.\n담당자명: undefined\n사유: 부서에 따른 아이디 할당을 위해 필요"
                }
            ],
            "dateCreated": "2019-10-28T17:59:25.749Z",
            "dateUpdated": "2019-10-28T17:59:25.756Z",
            "approvalDocuments": [],
            "handleKey": "SED20181030105615MMXDST163SYMMX2",
            "phoneNumber": "01000000000"
        }
    ],
    "limitationDocuments": [],
    "dateCreated": "2019-10-28T17:59:25.750Z",
    "dateUpdated": "2019-10-28T17:59:25.757Z"
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
    reason: '부서에 따른 아이디 할당을 위해 필요'
  },
  method: 'POST',
  json: true,
  url: 'http://api.coolsms.co.kr/senderid/v1/papers/duplicate/01000000000'
};

request(options, function(error, response, body) {
  if (error) throw error;
  console.log('result :', body);
});
```
{% endtab %}

{% tab title="JQUERY" %}
```javascript
var options = {
  headers: {
    Authorization:
      'HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4',
    'Content-Type': 'application/json'
  },
  body: {
    reason: '부서에 따른 아이디 할당을 위해 필요'
  },
  method: 'POST',
  url: 'http://api.coolsms.co.kr/senderid/v1/papers/duplicate/01000000000'
};

$.ajax(options).done(function(response) {
  console.log(response);
});
```
{% endtab %}

{% tab title="PHP" %}
```php
<?php
$url = "http://api.coolsms.co.kr/senderid/v1/papers/duplicate/01000000000";
$data = '{"reason":"부서에 따른 아이디 할당을 위해 필요"}';

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

url = "http://api.coolsms.co.kr/senderid/v1/papers/duplicate/01000000000"
headers = {
  "Authorization": "HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4",
  "Content-Type": "application/json"
}
data = '{"reason":"부서에 따른 아이디 할당을 위해 필요"}'

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
    -d '{"reason":"부서에 따른 아이디 할당을 위해 필요"}' \
    http://api.coolsms.co.kr/senderid/v1/papers/duplicate/01000000000
```
{% endtab %}

{% tab title="RUBY" %}
```ruby
require 'net/http'
require 'uri'
require 'json'

uri = URI.parse("http://api.coolsms.co.kr/senderid/v1/papers/duplicate/01000000000")

headers = {
  "Authorization": "HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4",
  "Content-Type": "application/json"
}
data = {
  "reason": "부서에 따른 아이디 할당을 위해 필요"
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
  uri := "http://api.coolsms.co.kr/senderid/v1/papers/duplicate/01000000000"
  data := strings.NewReader(`{"reason":"부서에 따른 아이디 할당을 위해 필요"}`)

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
    String targetUrl = "http://api.coolsms.co.kr/senderid/v1/papers/duplicate/01000000000";
    String parameters = "{\"reason\":\"부서에 따른 아이디 할당을 위해 필요\"}";

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

> 문서 생성일 : 2019-10-28

