# 세금계산서 목록 조회

## Request
```
GET https://api.coolsms.co.kr/cash/v1/taxinvoice
```

발급받은 세금계산서 목록을 조회합니다.

### Authorization 인증 필요 [[?]](https://docs.coolsms.co.kr/authentication/authentication)

| 계정 권한 | 회원 권한 | 계정 상태 | 회원 상태 | 계정 인증 |
| :- | :- | :- | :- | :-: |
| `cash:read` | `role-cash:read` |  |  |  |

### Query Params
| Name | Type | Required | Allowed Operator [[?]](https://docs.coolsms.co.kr/api-reference/api-reference#operator) | Description |
| :--- | :--: | :------: | :--------------: | :---------- |
| corpNum | `string` |  | eq | 설명 없음 |
| corpName | `string` |  | eq | 설명 없음 |
| stateCode | `string` |  | eq | 설명 없음 |
| ntsResult | `string` |  | eq | 설명 없음 |
| openYN | `boolean` |  | eq | 설명 없음 |
| startDate | `string` |  | eq | 검색 날짜 시작 범위 |
| endDate | `string` |  | eq | 검색 날짜 끝 범위 |
| offset | `number` |  | eq | 검색 시작 지점 |
| limit | `number` |  | eq | 한 페이지에 불러옥 목록 개수 |

---

## Samples

### getTaxinvoice.spec.js

> **Sample Request**

```
http://api.coolsms.co.kr/cash/v1/taxinvoice
```

> **Sample Response**

```json
[
    {
        "taxType": "tax",
        "issueType": "regular",
        "purposeType": "receipt",
        "itemKey": null,
        "stateCode": "300",
        "openYN": true,
        "openDT": null,
        "ntsResult": "SUC001",
        "ntsResultErrorCode": null,
        "modifyCode": null,
        "accountId": "19041920726336",
        "corpNum": "2178133791",
        "corpName": "(주)누리고",
        "writeDate": "20180705",
        "supplyCostTotal": 10000,
        "taxTotal": 1000,
        "totalAmount": 11000,
        "dateCreated": "2018-01-01T09:00:00.000Z",
        "dateUpdated": "2019-10-28T17:43:53.948Z"
    },
    {
        "taxType": "tax",
        "issueType": "regular",
        "purposeType": "receipt",
        "itemKey": null,
        "stateCode": "300",
        "openYN": true,
        "openDT": null,
        "ntsResult": "SUC001",
        "ntsResultErrorCode": null,
        "modifyCode": null,
        "accountId": "19041920726336",
        "corpNum": "2178133791",
        "corpName": "(주)누리고",
        "writeDate": "20180705",
        "supplyCostTotal": 10000,
        "taxTotal": 1000,
        "totalAmount": 11000,
        "dateCreated": "2018-01-01T09:00:00.000Z",
        "dateUpdated": "2019-10-28T17:43:53.948Z"
    },
    {
        "taxType": "tax",
        "issueType": "regular",
        "purposeType": "receipt",
        "itemKey": null,
        "stateCode": "300",
        "openYN": true,
        "openDT": null,
        "ntsResult": "SUC001",
        "ntsResultErrorCode": null,
        "modifyCode": null,
        "accountId": "19041920726336",
        "corpNum": "2178133791",
        "corpName": "(주)누리고",
        "writeDate": "20180705",
        "supplyCostTotal": 10000,
        "taxTotal": 1000,
        "totalAmount": 11000,
        "dateCreated": "2018-01-01T09:00:00.000Z",
        "dateUpdated": "2019-10-28T17:43:53.948Z"
    },
    {
        "taxType": "tax",
        "issueType": "regular",
        "purposeType": "receipt",
        "itemKey": null,
        "stateCode": "300",
        "openYN": true,
        "openDT": null,
        "ntsResult": "SUC001",
        "ntsResultErrorCode": null,
        "modifyCode": null,
        "accountId": "19041920726336",
        "corpNum": "2178133791",
        "corpName": "(주)누리고",
        "writeDate": "20180705",
        "supplyCostTotal": 10000,
        "taxTotal": 1000,
        "totalAmount": 11000,
        "dateCreated": "2018-01-01T09:00:00.000Z",
        "dateUpdated": "2019-10-28T17:43:53.948Z"
    },
    {
        "taxType": "tax",
        "issueType": "regular",
        "purposeType": "receipt",
        "itemKey": null,
        "stateCode": "300",
        "openYN": true,
        "openDT": null,
        "ntsResult": "SUC001",
        "ntsResultErrorCode": null,
        "modifyCode": null,
        "accountId": "19041920726336",
        "corpNum": "2178133791",
        "corpName": "(주)누리고",
        "writeDate": "20180705",
        "supplyCostTotal": 10000,
        "taxTotal": 1000,
        "totalAmount": 11000,
        "dateCreated": "2018-01-01T09:00:00.000Z",
        "dateUpdated": "2019-10-28T17:43:53.948Z"
    },
    {
        "taxType": "tax",
        "issueType": "regular",
        "purposeType": "receipt",
        "itemKey": null,
        "stateCode": "500",
        "openYN": false,
        "openDT": null,
        "ntsResult": "SUC003",
        "ntsResultErrorCode": null,
        "modifyCode": null,
        "accountId": "19041920726336",
        "corpNum": "2014839201",
        "corpName": "aws",
        "writeDate": "20180705",
        "supplyCostTotal": 10000,
        "taxTotal": 1000,
        "totalAmount": 11000,
        "dateCreated": "2018-03-01T09:00:00.000Z",
        "dateUpdated": "2019-10-28T17:43:53.949Z"
    },
    {
        "taxType": "tax",
        "issueType": "regular",
        "purposeType": "receipt",
        "itemKey": null,
        "stateCode": "500",
        "openYN": false,
        "openDT": null,
        "ntsResult": "SUC003",
        "ntsResultErrorCode": null,
        "modifyCode": null,
        "accountId": "19041920726336",
        "corpNum": "2014839201",
        "corpName": "aws",
        "writeDate": "20180705",
        "supplyCostTotal": 10000,
        "taxTotal": 1000,
        "totalAmount": 11000,
        "dateCreated": "2018-03-01T09:00:00.000Z",
        "dateUpdated": "2019-10-28T17:43:53.949Z"
    },
    {
        "taxType": "tax",
        "issueType": "regular",
        "purposeType": "receipt",
        "itemKey": null,
        "stateCode": "500",
        "openYN": false,
        "openDT": null,
        "ntsResult": "SUC003",
        "ntsResultErrorCode": null,
        "modifyCode": null,
        "accountId": "19041920726336",
        "corpNum": "2014839201",
        "corpName": "aws",
        "writeDate": "20180705",
        "supplyCostTotal": 10000,
        "taxTotal": 1000,
        "totalAmount": 11000,
        "dateCreated": "2018-03-01T09:00:00.000Z",
        "dateUpdated": "2019-10-28T17:43:53.949Z"
    },
    {
        "taxType": "tax",
        "issueType": "regular",
        "purposeType": "receipt",
        "itemKey": null,
        "stateCode": "500",
        "openYN": false,
        "openDT": null,
        "ntsResult": "SUC003",
        "ntsResultErrorCode": null,
        "modifyCode": null,
        "accountId": "19041920726336",
        "corpNum": "2014839201",
        "corpName": "aws",
        "writeDate": "20180705",
        "supplyCostTotal": 10000,
        "taxTotal": 1000,
        "totalAmount": 11000,
        "dateCreated": "2018-03-01T09:00:00.000Z",
        "dateUpdated": "2019-10-28T17:43:53.949Z"
    },
    {
        "taxType": "tax",
        "issueType": "regular",
        "purposeType": "receipt",
        "itemKey": null,
        "stateCode": "500",
        "openYN": false,
        "openDT": null,
        "ntsResult": "SUC003",
        "ntsResultErrorCode": null,
        "modifyCode": null,
        "accountId": "19041920726336",
        "corpNum": "2014839201",
        "corpName": "aws",
        "writeDate": "20180705",
        "supplyCostTotal": 10000,
        "taxTotal": 1000,
        "totalAmount": 11000,
        "dateCreated": "2018-03-01T09:00:00.000Z",
        "dateUpdated": "2019-10-28T17:43:53.949Z"
    },
    {
        "taxType": "tax",
        "issueType": "regular",
        "purposeType": "receipt",
        "itemKey": null,
        "stateCode": "500",
        "openYN": false,
        "openDT": null,
        "ntsResult": "SUC003",
        "ntsResultErrorCode": null,
        "modifyCode": null,
        "accountId": "19041920726336",
        "corpNum": "2014839201",
        "corpName": "aws",
        "writeDate": "20180705",
        "supplyCostTotal": 10000,
        "taxTotal": 1000,
        "totalAmount": 11000,
        "dateCreated": "2018-03-01T09:00:00.000Z",
        "dateUpdated": "2019-10-28T17:43:53.949Z"
    },
    {
        "taxType": "tax",
        "issueType": "regular",
        "purposeType": "receipt",
        "itemKey": null,
        "stateCode": "500",
        "openYN": false,
        "openDT": null,
        "ntsResult": "SUC003",
        "ntsResultErrorCode": null,
        "modifyCode": null,
        "accountId": "19041920726336",
        "corpNum": "2014839201",
        "corpName": "aws",
        "writeDate": "20180705",
        "supplyCostTotal": 10000,
        "taxTotal": 1000,
        "totalAmount": 11000,
        "dateCreated": "2018-03-01T09:00:00.000Z",
        "dateUpdated": "2019-10-28T17:43:53.949Z"
    },
    {
        "taxType": "tax",
        "issueType": "regular",
        "purposeType": "receipt",
        "itemKey": null,
        "stateCode": "500",
        "openYN": false,
        "openDT": null,
        "ntsResult": "SUC003",
        "ntsResultErrorCode": null,
        "modifyCode": null,
        "accountId": "19041920726336",
        "corpNum": "2014839201",
        "corpName": "aws",
        "writeDate": "20180705",
        "supplyCostTotal": 10000,
        "taxTotal": 1000,
        "totalAmount": 11000,
        "dateCreated": "2018-03-01T09:00:00.000Z",
        "dateUpdated": "2019-10-28T17:43:53.949Z"
    },
    {
        "taxType": "tax",
        "issueType": "regular",
        "purposeType": "receipt",
        "itemKey": null,
        "stateCode": "500",
        "openYN": false,
        "openDT": null,
        "ntsResult": "SUC003",
        "ntsResultErrorCode": null,
        "modifyCode": null,
        "accountId": "19041920726336",
        "corpNum": "2014839201",
        "corpName": "aws",
        "writeDate": "20180705",
        "supplyCostTotal": 10000,
        "taxTotal": 1000,
        "totalAmount": 11000,
        "dateCreated": "2018-03-01T09:00:00.000Z",
        "dateUpdated": "2019-10-28T17:43:53.949Z"
    },
    {
        "taxType": "tax",
        "issueType": "regular",
        "purposeType": "receipt",
        "itemKey": null,
        "stateCode": "500",
        "openYN": false,
        "openDT": null,
        "ntsResult": "SUC003",
        "ntsResultErrorCode": null,
        "modifyCode": null,
        "accountId": "19041920726336",
        "corpNum": "2014839201",
        "corpName": "aws",
        "writeDate": "20180705",
        "supplyCostTotal": 10000,
        "taxTotal": 1000,
        "totalAmount": 11000,
        "dateCreated": "2018-03-01T09:00:00.000Z",
        "dateUpdated": "2019-10-28T17:43:53.950Z"
    }
]
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
  url: 'http://api.coolsms.co.kr/cash/v1/taxinvoice'
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
      'HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4'
  },
  method: 'GET',
  url: 'http://api.coolsms.co.kr/cash/v1/taxinvoice'
};

$.ajax(options).done(function(response) {
  console.log(response);
});

```
{% endtab %}

{% tab title="PHP" %}

```php
<?php
$url = "http://api.coolsms.co.kr/cash/v1/taxinvoice";

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

url = "http://api.coolsms.co.kr/cash/v1/taxinvoice"
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
	http://api.coolsms.co.kr/cash/v1/taxinvoice
```
{% endtab %}

{% tab title="RUBY" %}

```ruby
require 'net/http'
require 'uri'
require 'json'

uri = URI.parse("http://api.coolsms.co.kr/cash/v1/taxinvoice")

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
  uri := "http://api.coolsms.co.kr/cash/v1/taxinvoice"

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
package coolsms;

import java.io.BufferedReader;
import java.io.DataOutputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Request {
  public static void main(String[] args) throws Exception {
    String targetUrl = "http://api.coolsms.co.kr/cash/v1/taxinvoice";

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

> 문서 생성일 : 2019-10-28

