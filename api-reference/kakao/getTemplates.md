# 템플릿 목록 조회

## Request
```
GET https://api.coolsms.co.kr/kakao/v1/templates
```

템플릿의 목록을 조회합니다.

### Authorization 인증 필요 [[?]](https://docs.coolsms.co.kr/authentication/overview#authorization)

| 계정 권한 | 회원 권한 | 계정 상태 | 회원 상태 | 계정 인증 |
| :- | :- | :- | :- | :-: |
| `kakao:read` | `role-kakao:read` |  |  |  |

### Query Params
| Name | Type | Required | Allowed Operator [[?]](https://docs.coolsms.co.kr/api-reference/overview#operator) | Description |
| :--- | :--: | :------: | :--------------: | :---------- |
| name | `string` |  | eq, ne, like | 이름 |
| pfId | `string` |  | eq | 카카오톡채널 고유 아이디 |
| templateId | `string` |  | eq | 템플릿 고유 아이디 |
| isHidden | `boolean` |  | eq | 설명 없음 |
| status | `string` |  | eq | 상태값 |
| startKey | `string` |  | eq | 현재 목록을 불러올 기준이 되는 키 |
| limit | `number` |  | eq | 한 페이지에 불러옥 목록 개수 |
| dateCreated | `date` |  | eq, gte, lte, gt, lt | 최초 생성 날짜 |
| dateUpdated | `date` |  | eq, gte, lte, gt, lt | 최근 수정 날짜 |

---

## Samples

### getTemplates.spec.js

> **Sample Request**

```
http://api.coolsms.co.kr/kakao/v1/templates
```

> **Sample Response**

```json
{
    "limit": 20,
    "templateList": [
        {
            "isHidden": false,
            "accountId": "12925149",
            "templateId": "TP01ID210129012914856zt8YNZDRHFL",
            "name": "A29",
            "pfId": "PF01ID210129012914472SwRBsJNvzu9",
            "codes": [
                {
                    "status": "APPROVED",
                    "service": "biz",
                    "code": "123123",
                    "comments": []
                }
            ],
            "content": "testMessage",
            "dateCreated": "2021-01-29T01:29:14.856Z",
            "dateUpdated": "2021-01-29T01:29:14.856Z",
            "buttons": []
        },
        {
            "isHidden": false,
            "accountId": "12925149",
            "templateId": "TP01ID210129012914856z1Tsz0rtF23",
            "name": "A26",
            "pfId": "PF01ID210129012914472SwRBsJNvzu9",
            "codes": [
                {
                    "status": "APPROVED",
                    "service": "biz",
                    "code": "123123",
                    "comments": []
                }
            ],
            "content": "testMessage",
            "dateCreated": "2021-01-29T01:29:14.856Z",
            "dateUpdated": "2021-01-29T01:29:14.856Z",
            "buttons": []
        },
        {
            "isHidden": false,
            "accountId": "12925149",
            "templateId": "TP01ID210129012914856q6GPin31yVm",
            "name": "A23",
            "pfId": "PF01ID210129012914472SwRBsJNvzu9",
            "codes": [
                {
                    "status": "APPROVED",
                    "service": "biz",
                    "code": "123123",
                    "comments": []
                }
            ],
            "content": "testMessage",
            "dateCreated": "2021-01-29T01:29:14.856Z",
            "dateUpdated": "2021-01-29T01:29:14.856Z",
            "buttons": []
        },
        {
            "isHidden": false,
            "accountId": "12925149",
            "templateId": "TP01ID210129012914856nRsPRCAVKHF",
            "name": "A24",
            "pfId": "PF01ID210129012914472SwRBsJNvzu9",
            "codes": [
                {
                    "status": "APPROVED",
                    "service": "biz",
                    "code": "123123",
                    "comments": []
                }
            ],
            "content": "testMessage",
            "dateCreated": "2021-01-29T01:29:14.856Z",
            "dateUpdated": "2021-01-29T01:29:14.856Z",
            "buttons": []
        },
        {
            "isHidden": false,
            "accountId": "12925149",
            "templateId": "TP01ID210129012914856XR0DzzCNZaL",
            "name": "A28",
            "pfId": "PF01ID210129012914472SwRBsJNvzu9",
            "codes": [
                {
                    "status": "APPROVED",
                    "service": "biz",
                    "code": "123123",
                    "comments": []
                }
            ],
            "content": "testMessage",
            "dateCreated": "2021-01-29T01:29:14.856Z",
            "dateUpdated": "2021-01-29T01:29:14.856Z",
            "buttons": []
        },
        {
            "isHidden": false,
            "accountId": "12925149",
            "templateId": "TP01ID210129012914856UueTSJrSnXZ",
            "name": "A32",
            "pfId": "PF01ID210129012914472SwRBsJNvzu9",
            "codes": [
                {
                    "status": "APPROVED",
                    "service": "biz",
                    "code": "123123",
                    "comments": []
                }
            ],
            "content": "testMessage",
            "dateCreated": "2021-01-29T01:29:14.856Z",
            "dateUpdated": "2021-01-29T01:29:14.856Z",
            "buttons": []
        },
        {
            "isHidden": false,
            "accountId": "12925149",
            "templateId": "TP01ID210129012914856TtV3dOJZy6I",
            "name": "A22",
            "pfId": "PF01ID210129012914472SwRBsJNvzu9",
            "codes": [
                {
                    "status": "APPROVED",
                    "service": "biz",
                    "code": "123123",
                    "comments": []
                }
            ],
            "content": "testMessage",
            "dateCreated": "2021-01-29T01:29:14.856Z",
            "dateUpdated": "2021-01-29T01:29:14.856Z",
            "buttons": []
        },
        {
            "isHidden": false,
            "accountId": "12925149",
            "templateId": "TP01ID210129012914856QA2gGaMExTi",
            "name": "A30",
            "pfId": "PF01ID210129012914472SwRBsJNvzu9",
            "codes": [
                {
                    "status": "APPROVED",
                    "service": "biz",
                    "code": "123123",
                    "comments": []
                }
            ],
            "content": "testMessage",
            "dateCreated": "2021-01-29T01:29:14.856Z",
            "dateUpdated": "2021-01-29T01:29:14.856Z",
            "buttons": []
        },
        {
            "isHidden": true,
            "accountId": "12925149",
            "templateId": "TP01ID210129012914856PQSfPGvwHhR",
            "name": "A35",
            "pfId": "PF01ID210129012914472SwRBsJNvzu9",
            "codes": [
                {
                    "status": "APPROVED",
                    "service": "biz",
                    "code": "123123",
                    "comments": []
                }
            ],
            "content": "testMessage",
            "dateCreated": "2021-01-29T01:29:14.856Z",
            "dateUpdated": "2021-01-29T01:29:14.856Z",
            "buttons": []
        },
        {
            "isHidden": false,
            "accountId": "12925149",
            "templateId": "TP01ID210129012914856DE14CVJcO0a",
            "name": "A27",
            "pfId": "PF01ID210129012914472SwRBsJNvzu9",
            "codes": [
                {
                    "status": "APPROVED",
                    "service": "biz",
                    "code": "123123",
                    "comments": []
                }
            ],
            "content": "testMessage",
            "dateCreated": "2021-01-29T01:29:14.856Z",
            "dateUpdated": "2021-01-29T01:29:14.856Z",
            "buttons": []
        },
        {
            "isHidden": false,
            "accountId": "12925149",
            "templateId": "TP01ID210129012914856CUvEkWeYypy",
            "name": "A34",
            "pfId": "PF01ID210129012914472SwRBsJNvzu9",
            "codes": [
                {
                    "status": "APPROVED",
                    "service": "biz",
                    "code": "123123",
                    "comments": []
                }
            ],
            "content": "testMessage",
            "dateCreated": "2021-01-29T01:29:14.856Z",
            "dateUpdated": "2021-01-29T01:29:14.856Z",
            "buttons": []
        },
        {
            "isHidden": true,
            "accountId": "12925149",
            "templateId": "TP01ID210129012914856BHuCYPDP9LY",
            "name": "A36",
            "pfId": "PF01ID210129012914472SwRBsJNvzu9",
            "codes": [
                {
                    "status": "APPROVED",
                    "service": "biz",
                    "code": "123123",
                    "comments": []
                }
            ],
            "content": "testMessage",
            "dateCreated": "2021-01-29T01:29:14.856Z",
            "dateUpdated": "2021-01-29T01:29:14.856Z",
            "buttons": []
        },
        {
            "isHidden": false,
            "accountId": "12925149",
            "templateId": "TP01ID210129012914856BECs4L626VW",
            "name": "A21",
            "pfId": "PF01ID210129012914472SwRBsJNvzu9",
            "codes": [
                {
                    "status": "APPROVED",
                    "service": "biz",
                    "code": "123123",
                    "comments": []
                }
            ],
            "content": "testMessage",
            "dateCreated": "2021-01-29T01:29:14.856Z",
            "dateUpdated": "2021-01-29T01:29:14.856Z",
            "buttons": []
        },
        {
            "isHidden": false,
            "accountId": "12925149",
            "templateId": "TP01ID2101290129148567b4W2Mxa67h",
            "name": "A33",
            "pfId": "PF01ID210129012914472SwRBsJNvzu9",
            "codes": [
                {
                    "status": "APPROVED",
                    "service": "biz",
                    "code": "123123",
                    "comments": []
                }
            ],
            "content": "testMessage",
            "dateCreated": "2021-01-29T01:29:14.856Z",
            "dateUpdated": "2021-01-29T01:29:14.856Z",
            "buttons": []
        },
        {
            "isHidden": false,
            "accountId": "12925149",
            "templateId": "TP01ID2101290129148565vg7QpWoeLb",
            "name": "A31",
            "pfId": "PF01ID210129012914472SwRBsJNvzu9",
            "codes": [
                {
                    "status": "APPROVED",
                    "service": "biz",
                    "code": "123123",
                    "comments": []
                }
            ],
            "content": "testMessage",
            "dateCreated": "2021-01-29T01:29:14.856Z",
            "dateUpdated": "2021-01-29T01:29:14.856Z",
            "buttons": []
        },
        {
            "isHidden": false,
            "accountId": "12925149",
            "templateId": "TP01ID21012901291485634uU4Fc5OUQ",
            "name": "A20",
            "pfId": "PF01ID210129012914472SwRBsJNvzu9",
            "codes": [
                {
                    "status": "APPROVED",
                    "service": "biz",
                    "code": "123123",
                    "comments": []
                }
            ],
            "content": "testMessage",
            "dateCreated": "2021-01-29T01:29:14.856Z",
            "dateUpdated": "2021-01-29T01:29:14.856Z",
            "buttons": []
        },
        {
            "isHidden": false,
            "accountId": "12925149",
            "templateId": "TP01ID2101290129148562VYRhGs8Unq",
            "name": "A25",
            "pfId": "PF01ID210129012914472SwRBsJNvzu9",
            "codes": [
                {
                    "status": "APPROVED",
                    "service": "biz",
                    "code": "123123",
                    "comments": []
                }
            ],
            "content": "testMessage",
            "dateCreated": "2021-01-29T01:29:14.856Z",
            "dateUpdated": "2021-01-29T01:29:14.856Z",
            "buttons": []
        },
        {
            "isHidden": false,
            "accountId": "12925149",
            "templateId": "TP01ID210129012914855xCRhXa2k0Qk",
            "name": "A11",
            "pfId": "PF01ID2101290129144727FZO6BpZ15E",
            "codes": [
                {
                    "status": "INSPECTING",
                    "service": "biz",
                    "code": "123123",
                    "comments": []
                }
            ],
            "content": "testMessage",
            "dateCreated": "2021-02-08T01:29:14.472Z",
            "dateUpdated": "2021-02-08T01:29:14.472Z",
            "buttons": []
        },
        {
            "isHidden": false,
            "accountId": "12925149",
            "templateId": "TP01ID210129012914855weS4bc3f3AW",
            "name": "A12",
            "pfId": "PF01ID2101290129144727FZO6BpZ15E",
            "codes": [
                {
                    "status": "INSPECTING",
                    "service": "biz",
                    "code": "123123",
                    "comments": []
                }
            ],
            "content": "testMessage",
            "dateCreated": "2021-02-08T01:29:14.472Z",
            "dateUpdated": "2021-02-08T01:29:14.472Z",
            "buttons": []
        },
        {
            "isHidden": false,
            "accountId": "12925149",
            "templateId": "TP01ID210129012914855tv3tLwQzU4p",
            "name": "A5",
            "pfId": "PF01ID2101290129144727FZO6BpZ15E",
            "codes": [
                {
                    "status": "INSPECTING",
                    "service": "biz",
                    "code": "123123",
                    "comments": []
                }
            ],
            "content": "testMessage",
            "dateCreated": "2021-02-08T01:29:14.472Z",
            "dateUpdated": "2021-02-08T01:29:14.472Z",
            "buttons": []
        }
    ],
    "startKey": "TP01ID210129012914856zt8YNZDRHFL",
    "nextKey": "TP01ID210129012914855iRUG0TOC1cR"
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
      'HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4'
  },
  method: 'GET',
  json: true,
  url: 'http://api.coolsms.co.kr/kakao/v1/templates'
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
$url = "http://api.coolsms.co.kr/kakao/v1/templates";

$options = array(
    'http' => array(
        'header'  => "Authorization: HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4\r\n",
        'method'  => 'GET'
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

url = "http://api.coolsms.co.kr/kakao/v1/templates"
headers = {
  "Authorization": "HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4"
}

response = requests.get(url, headers=headers)
print(response.status_code)
print(response.text)

```
{% endtab %}

{% tab title="CURL" %}

```curl
#!/bin/bash
curl -X GET \
	-H 'Authorization: HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4' \
	http://api.coolsms.co.kr/kakao/v1/templates
```
{% endtab %}

{% tab title="RUBY" %}

```ruby
require 'net/http'
require 'uri'
require 'json'

uri = URI.parse("http://api.coolsms.co.kr/kakao/v1/templates")

headers = {
  "Authorization": "HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4"
}
http = Net::HTTP.new(uri.host, uri.port)
request = Net::HTTP::Get.new(uri.request_uri, headers)

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
  uri := "http://api.coolsms.co.kr/kakao/v1/templates"

  req, err := http.NewRequest("GET", uri, nil)
  if err != nil { panic(err) }

  req.Header.Set("Authorization", "HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4")

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
    String targetUrl = "http://api.coolsms.co.kr/kakao/v1/templates";

    URL url = new URL(targetUrl);
    HttpURLConnection con = (HttpURLConnection) url.openConnection();

    con.setRequestMethod("GET");

    con.setRequestProperty("Authorization", "HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4");

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

---

> 문서 생성일 : 2021-01-29

