# 파일 목록 조회

## Request
```
GET https://api.coolsms.co.kr/storage/v1/files
```

한 계정이 가지고 있는 파일들의 목록을 조회합니다.

### Authorization 인증 필요 [[?]](https://docs.coolsms.co.kr/authentication/overview#authorization)

| 계정 권한 | 회원 권한 | 계정 상태 | 회원 상태 | 계정 인증 |
| :- | :- | :- | :- | :-: |
| `storage:read` |  | `ACTIVE` | `ACTIVE` |  |

### Query Params
| Name | Type | Required | Allowed Operator [[?]](https://docs.coolsms.co.kr/api-reference/overview#operator) | Description |
| :--- | :--: | :------: | :--------------: | :---------- |
| fileId | `string` |  | eq | 파일 고유 아이디 |
| name | `string` |  | eq | 파일 이름 |
| url | `string` |  | eq | 파일 주소 |
| originalName | `string` |  | eq | 원본 파일 이름 |
| handleKey | `string` |  | eq | 참조의 핸들키 |
| category | `string` |  | eq | 참조 이름 |
| refId | `string` |  | eq | 참조 대상의 리소스 아이디 |
| dateCreated | `date` |  | eq | 최초 생성 날짜 |
| dateUpdated | `date` |  | eq | 최근 수정 날짜 |
| startKey | `string` |  | eq | 현재 목록을 불러올 기준이 되는 키 |
| limit | `number` |  | eq | 한 페이지에 불러옥 목록 개수 |
| type | `string` |  | eq | 문서 타입(DOCUMENT, KAKAO, MMS) |
| useDaou | `boolean` |  | eq | [카카오 채널] 다우기술 이미지 연동 여부 |
| useBiztalk | `boolean` |  | eq | [카카오 채널] 비즈톡 이미지 연동 여부 |

---

## Samples

### getFileList.spec.js

> **Sample Request**

```
http://api.coolsms.co.kr/storage/v1/files
```

> **Sample Response**

```json
{
    "fileList": [
        {
            "kakao": {
                "daou": null,
                "biztalk": null
            },
            "type": "DOCUMENT",
            "originalName": "파일 원본 이름34",
            "link": null,
            "width": null,
            "height": null,
            "fileSize": null,
            "fileId": "FILEID20092304334104438hwt31oH2U",
            "accountId": "19013037529548",
            "name": "파일 이름34",
            "url": "https://coolsms.co.kr/godori",
            "references": [
                {
                    "handleKey": "REFERE200923043341044E9Oon6Wjfy1",
                    "category": "SENDERID_APPROVAL",
                    "refId": "REFID5200923043341044kEFQ1piSl4a"
                }
            ],
            "dateCreated": "2020-09-23T03:33:41.045Z",
            "dateUpdated": "2020-09-23T03:33:41.045Z"
        },
        {
            "kakao": {
                "daou": null,
                "biztalk": null
            },
            "type": "DOCUMENT",
            "originalName": "파일 원본 이름33",
            "link": null,
            "width": null,
            "height": null,
            "fileSize": null,
            "fileId": "FILEID200923043341038CPh3a2cP2tl",
            "accountId": "19013037529548",
            "name": "파일 이름33",
            "url": "https://coolsms.co.kr/godori",
            "references": [
                {
                    "handleKey": "REFERE200923043341038lAT9z1vlfbz",
                    "category": "SENDERID_APPROVAL",
                    "refId": "REFID5200923043341038CGdWrs0wFXm"
                }
            ],
            "dateCreated": "2020-09-23T03:33:41.040Z",
            "dateUpdated": "2020-09-23T03:33:41.040Z"
        },
        {
            "kakao": {
                "daou": null,
                "biztalk": null
            },
            "type": "DOCUMENT",
            "originalName": "파일 원본 이름32",
            "link": null,
            "width": null,
            "height": null,
            "fileSize": null,
            "fileId": "FILEID200923043341033kfQtax8oxsp",
            "accountId": "19013037529548",
            "name": "파일 이름32",
            "url": "https://coolsms.co.kr/godori",
            "references": [
                {
                    "handleKey": "REFERE200923043341033mvwVoblxHVG",
                    "category": "SENDERID_APPROVAL",
                    "refId": "REFID5200923043341033ESLuEcqlPc5"
                }
            ],
            "dateCreated": "2020-09-23T03:33:41.034Z",
            "dateUpdated": "2020-09-23T03:33:41.034Z"
        },
        {
            "kakao": {
                "daou": null,
                "biztalk": null
            },
            "type": "DOCUMENT",
            "originalName": "파일 원본 이름31",
            "link": null,
            "width": null,
            "height": null,
            "fileSize": null,
            "fileId": "FILEID200923043341028hw27kObyvWg",
            "accountId": "19013037529548",
            "name": "파일 이름31",
            "url": "https://coolsms.co.kr/godori",
            "references": [
                {
                    "handleKey": "REFERE200923043341028X7OVuBKAf8m",
                    "category": "SENDERID_APPROVAL",
                    "refId": "REFID5200923043341028nWTmLsyAFCI"
                }
            ],
            "dateCreated": "2020-09-23T03:33:41.029Z",
            "dateUpdated": "2020-09-23T03:33:41.029Z"
        },
        {
            "kakao": {
                "daou": null,
                "biztalk": null
            },
            "type": "DOCUMENT",
            "originalName": "파일 원본 이름30",
            "link": null,
            "width": null,
            "height": null,
            "fileSize": null,
            "fileId": "FILEID200923043341024kho3jc4I2Av",
            "accountId": "19013037529548",
            "name": "파일 이름30",
            "url": "https://coolsms.co.kr/godori",
            "references": [
                {
                    "handleKey": "REFERE200923043341024EMAKd1k9qCB",
                    "category": "SENDERID_APPROVAL",
                    "refId": "REFID5200923043341024fKBaeTYF9RS"
                }
            ],
            "dateCreated": "2020-09-23T03:33:41.025Z",
            "dateUpdated": "2020-09-23T03:33:41.025Z"
        },
        {
            "kakao": {
                "daou": null,
                "biztalk": null
            },
            "type": "DOCUMENT",
            "originalName": "파일 원본 이름29",
            "link": null,
            "width": null,
            "height": null,
            "fileSize": null,
            "fileId": "FILEID20092304334101830jgL7PT549",
            "accountId": "19013037529548",
            "name": "파일 이름29",
            "url": "https://coolsms.co.kr/godori",
            "references": [
                {
                    "handleKey": "REFERE200923043341019jr51bZOSZeD",
                    "category": "SENDERID_APPROVAL",
                    "refId": "REFID5200923043341019UwUCeUt01DE"
                }
            ],
            "dateCreated": "2020-09-23T03:33:41.019Z",
            "dateUpdated": "2020-09-23T03:33:41.019Z"
        },
        {
            "kakao": {
                "daou": null,
                "biztalk": null
            },
            "type": "DOCUMENT",
            "originalName": "파일 원본 이름28",
            "link": null,
            "width": null,
            "height": null,
            "fileSize": null,
            "fileId": "FILEID200923043341014PVP8SE7ADn4",
            "accountId": "19013037529548",
            "name": "파일 이름28",
            "url": "https://coolsms.co.kr/godori",
            "references": [
                {
                    "handleKey": "REFERE200923043341014SW6jJDzTf2m",
                    "category": "SENDERID_APPROVAL",
                    "refId": "REFID5200923043341014KkSRYgJVOFe"
                }
            ],
            "dateCreated": "2020-09-23T03:33:41.015Z",
            "dateUpdated": "2020-09-23T03:33:41.015Z"
        },
        {
            "kakao": {
                "daou": null,
                "biztalk": null
            },
            "type": "DOCUMENT",
            "originalName": "파일 원본 이름27",
            "link": null,
            "width": null,
            "height": null,
            "fileSize": null,
            "fileId": "FILEID2009230433410096yHZJtH8zbj",
            "accountId": "19013037529548",
            "name": "파일 이름27",
            "url": "https://coolsms.co.kr/godori",
            "references": [
                {
                    "handleKey": "REFERE200923043341009JYiwHxYVytS",
                    "category": "SENDERID_APPROVAL",
                    "refId": "REFID5200923043341009QyUHCMVf6cm"
                }
            ],
            "dateCreated": "2020-09-23T03:33:41.010Z",
            "dateUpdated": "2020-09-23T03:33:41.010Z"
        },
        {
            "kakao": {
                "daou": null,
                "biztalk": null
            },
            "type": "DOCUMENT",
            "originalName": "파일 원본 이름26",
            "link": null,
            "width": null,
            "height": null,
            "fileSize": null,
            "fileId": "FILEID200923043341005oVDYQaPjkkP",
            "accountId": "19013037529548",
            "name": "파일 이름26",
            "url": "https://coolsms.co.kr/godori",
            "references": [
                {
                    "handleKey": "REFERE200923043341005nGUVq6kShHc",
                    "category": "SENDERID_APPROVAL",
                    "refId": "REFID5200923043341005h4we9Ax8Rtx"
                }
            ],
            "dateCreated": "2020-09-23T03:33:41.006Z",
            "dateUpdated": "2020-09-23T03:33:41.006Z"
        },
        {
            "kakao": {
                "daou": null,
                "biztalk": null
            },
            "type": "DOCUMENT",
            "originalName": "파일 원본 이름25",
            "link": null,
            "width": null,
            "height": null,
            "fileSize": null,
            "fileId": "FILEID200923043341000OndpntQ1SxD",
            "accountId": "19013037529548",
            "name": "파일 이름25",
            "url": "https://coolsms.co.kr/godori",
            "references": [
                {
                    "handleKey": "REFERE200923043341000EkTxzl0eSpP",
                    "category": "SENDERID_APPROVAL",
                    "refId": "REFID5200923043341000LOcc0POowC9"
                }
            ],
            "dateCreated": "2020-09-23T03:33:41.001Z",
            "dateUpdated": "2020-09-23T03:33:41.001Z"
        },
        {
            "kakao": {
                "daou": null,
                "biztalk": null
            },
            "type": "DOCUMENT",
            "originalName": "파일 원본 이름24",
            "link": null,
            "width": null,
            "height": null,
            "fileSize": null,
            "fileId": "FILEID200923043340996gnKdGcAAWyz",
            "accountId": "19013037529548",
            "name": "파일 이름24",
            "url": "https://coolsms.co.kr/godori",
            "references": [
                {
                    "handleKey": "REFERE200923043340996ZSU7wBtpNVT",
                    "category": "SENDERID_APPROVAL",
                    "refId": "REFID5200923043340996q0petfCdtBP"
                }
            ],
            "dateCreated": "2020-09-23T03:33:40.997Z",
            "dateUpdated": "2020-09-23T03:33:40.997Z"
        },
        {
            "kakao": {
                "daou": null,
                "biztalk": null
            },
            "type": "DOCUMENT",
            "originalName": "파일 원본 이름23",
            "link": null,
            "width": null,
            "height": null,
            "fileSize": null,
            "fileId": "FILEID200923043340989rciHdGaZwIn",
            "accountId": "19013037529548",
            "name": "파일 이름23",
            "url": "https://coolsms.co.kr/godori",
            "references": [
                {
                    "handleKey": "REFERE200923043340989se1U36U34Ky",
                    "category": "SENDERID_APPROVAL",
                    "refId": "REFID5200923043340989alE4ozcxbfx"
                }
            ],
            "dateCreated": "2020-09-23T03:33:40.991Z",
            "dateUpdated": "2020-09-23T03:33:40.991Z"
        },
        {
            "kakao": {
                "daou": null,
                "biztalk": null
            },
            "type": "DOCUMENT",
            "originalName": "파일 원본 이름22",
            "link": null,
            "width": null,
            "height": null,
            "fileSize": null,
            "fileId": "FILEID200923043340983NyJsHJtHvHu",
            "accountId": "19013037529548",
            "name": "파일 이름22",
            "url": "https://coolsms.co.kr/godori",
            "references": [
                {
                    "handleKey": "REFERE200923043340983Asl75D9Egdn",
                    "category": "SENDERID_APPROVAL",
                    "refId": "REFID5200923043340983cJQyIcwzizt"
                }
            ],
            "dateCreated": "2020-09-23T03:33:40.984Z",
            "dateUpdated": "2020-09-23T03:33:40.984Z"
        },
        {
            "kakao": {
                "daou": null,
                "biztalk": null
            },
            "type": "DOCUMENT",
            "originalName": "파일 원본 이름21",
            "link": null,
            "width": null,
            "height": null,
            "fileSize": null,
            "fileId": "FILEID200923043340978b4lRqhLMrzd",
            "accountId": "19013037529548",
            "name": "파일 이름21",
            "url": "https://coolsms.co.kr/godori",
            "references": [
                {
                    "handleKey": "REFERE200923043340978OQfGLUxS42u",
                    "category": "SENDERID_APPROVAL",
                    "refId": "REFID5200923043340978eJzAFVxsUwW"
                }
            ],
            "dateCreated": "2020-09-23T03:33:40.979Z",
            "dateUpdated": "2020-09-23T03:33:40.979Z"
        },
        {
            "kakao": {
                "daou": null,
                "biztalk": null
            },
            "type": "DOCUMENT",
            "originalName": "파일 원본 이름20",
            "link": null,
            "width": null,
            "height": null,
            "fileSize": null,
            "fileId": "FILEID200923043340971OkeUvqwiySL",
            "accountId": "19013037529548",
            "name": "파일 이름20",
            "url": "https://coolsms.co.kr/godori",
            "references": [
                {
                    "handleKey": "REFERE200923043340971CVppAmIjqTO",
                    "category": "SENDERID_APPROVAL",
                    "refId": "REFID5200923043340971RCbTqyIfZQx"
                }
            ],
            "dateCreated": "2020-09-23T03:33:40.972Z",
            "dateUpdated": "2020-09-23T03:33:40.972Z"
        },
        {
            "kakao": {
                "daou": null,
                "biztalk": "https://solapi.com"
            },
            "type": "KAKAO",
            "originalName": "파일 원본 이름19",
            "link": null,
            "width": null,
            "height": null,
            "fileSize": null,
            "fileId": "FILEID200923043340966qEu1nbYqYzS",
            "accountId": "19013037529548",
            "name": "파일 이름19",
            "url": "https://coolsms.co.kr/godori",
            "references": [
                {
                    "handleKey": "REFERE200923043340966A2xbHmXjrWF",
                    "category": "SENDERID_APPROVAL",
                    "refId": "REFID5200923043340966zB2AZcpPGAC"
                }
            ],
            "dateCreated": "2020-09-23T03:33:40.968Z",
            "dateUpdated": "2020-09-23T03:33:40.968Z"
        },
        {
            "kakao": {
                "daou": null,
                "biztalk": "https://solapi.com"
            },
            "type": "KAKAO",
            "originalName": "파일 원본 이름18",
            "link": null,
            "width": null,
            "height": null,
            "fileSize": null,
            "fileId": "FILEID200923043340961Xixd5S2vBS4",
            "accountId": "19013037529548",
            "name": "파일 이름18",
            "url": "https://coolsms.co.kr/godori",
            "references": [
                {
                    "handleKey": "REFERE200923043340961tPkVTeyl2eH",
                    "category": "SENDERID_APPROVAL",
                    "refId": "REFID5200923043340961IbRdiQSzNrn"
                }
            ],
            "dateCreated": "2020-09-23T03:33:40.963Z",
            "dateUpdated": "2020-09-23T03:33:40.963Z"
        },
        {
            "kakao": {
                "daou": null,
                "biztalk": "https://solapi.com"
            },
            "type": "KAKAO",
            "originalName": "파일 원본 이름17",
            "link": null,
            "width": null,
            "height": null,
            "fileSize": null,
            "fileId": "FILEID2009230433409568wPKBNr0FCM",
            "accountId": "19013037529548",
            "name": "파일 이름17",
            "url": "https://coolsms.co.kr/godori",
            "references": [
                {
                    "handleKey": "REFERE200923043340956DoV6CBWgHD6",
                    "category": "SENDERID_APPROVAL",
                    "refId": "REFID5200923043340956cP4hKbhyAbd"
                }
            ],
            "dateCreated": "2020-09-23T03:33:40.958Z",
            "dateUpdated": "2020-09-23T03:33:40.958Z"
        },
        {
            "kakao": {
                "daou": null,
                "biztalk": "https://solapi.com"
            },
            "type": "KAKAO",
            "originalName": "파일 원본 이름16",
            "link": null,
            "width": null,
            "height": null,
            "fileSize": null,
            "fileId": "FILEID2009230433409465ugxpl3zAms",
            "accountId": "19013037529548",
            "name": "파일 이름16",
            "url": "https://coolsms.co.kr/godori",
            "references": [
                {
                    "handleKey": "REFERE200923043340946ve6AJzUzk8g",
                    "category": "SENDERID_APPROVAL",
                    "refId": "REFID5200923043340946q7oaU28Zerx"
                }
            ],
            "dateCreated": "2020-09-23T03:33:40.947Z",
            "dateUpdated": "2020-09-23T03:33:40.947Z"
        },
        {
            "kakao": {
                "daou": null,
                "biztalk": "https://solapi.com"
            },
            "type": "KAKAO",
            "originalName": "파일 원본 이름15",
            "link": null,
            "width": null,
            "height": null,
            "fileSize": null,
            "fileId": "FILEID2009230433409409ZzIG1ZPg7S",
            "accountId": "19013037529548",
            "name": "파일 이름15",
            "url": "https://coolsms.co.kr/godori",
            "references": [
                {
                    "handleKey": "REFERE200923043340940DsUGqn7gtDc",
                    "category": "SENDERID_APPROVAL",
                    "refId": "REFID5200923043340940Xk9g4tZML9g"
                }
            ],
            "dateCreated": "2020-09-23T03:33:40.941Z",
            "dateUpdated": "2020-09-23T03:33:40.941Z"
        }
    ],
    "startKey": null,
    "nextKey": "FILEID200923043340935aYu26RpyNJu"
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
  url: 'http://api.coolsms.co.kr/storage/v1/files'
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
$url = "http://api.coolsms.co.kr/storage/v1/files";

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

url = "http://api.coolsms.co.kr/storage/v1/files"
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
	http://api.coolsms.co.kr/storage/v1/files
```
{% endtab %}

{% tab title="RUBY" %}

```ruby
require 'net/http'
require 'uri'
require 'json'

uri = URI.parse("http://api.coolsms.co.kr/storage/v1/files")

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
  uri := "http://api.coolsms.co.kr/storage/v1/files"

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
    String targetUrl = "http://api.coolsms.co.kr/storage/v1/files";

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

> 문서 생성일 : 2020-09-23

