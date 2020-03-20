# 일별 통계 내역 조회

## Request
```
GET https://api.coolsms.co.kr/messages/v4/statistics/daily
```

일별 통계 내역을 조회합니다.

### Authorization 인증 필요 [[?]](https://docs.coolsms.co.kr/authentication/overview#authorization)

| 계정 권한 | 회원 권한 | 계정 상태 | 회원 상태 | 계정 인증 |
| :- | :- | :- | :- | :-: |
| `message:read` | `role-message:read` | `ACTIVE` | `ACTIVE` | O |

### Query Params
| Name | Type | Required | Allowed Operator [[?]](https://docs.coolsms.co.kr/api-reference/overview#operator) | Description |
| :--- | :--: | :------: | :--------------: | :---------- |
| offset | `number` |  | eq | 검색 시작점 |
| limit | `number` |  | eq | 한 페이지에 불러옥 목록 개수 |
| taxIssued | `boolean` |  | eq | 세금 계산서 발행 여부 |
| profitSettlement | `boolean` |  | eq | 수익 정산 여부 |
| startDate | `date` |  | eq | 검색 시작 날짜 |
| endDate | `date` |  | eq | 검색 끝 날짜 |

---

## Samples

### getDailyStatistics.spec.js

> **Sample Request**

```
http://api.coolsms.co.kr/messages/v4/statistics/daily
```

> **Sample Response**

```json
[
    {
        "refund": {
            "balance": 0,
            "point": 0
        },
        "appId": null,
        "balance": 10,
        "point": 100,
        "taxIssued": false,
        "profitSettlement": false,
        "profit": 0,
        "accountId": "12925149",
        "date": "2019-12-11T00:00:00.000Z",
        "count": {
            "4000": {
                "sms": 10
            }
        }
    },
    {
        "refund": {
            "balance": 0,
            "point": 0
        },
        "appId": null,
        "balance": 10,
        "point": 100,
        "taxIssued": false,
        "profitSettlement": false,
        "profit": 0,
        "accountId": "12925149",
        "date": "2019-12-10T00:00:00.000Z",
        "count": {
            "4000": {
                "sms": 10
            }
        }
    },
    {
        "refund": {
            "balance": 0,
            "point": 0
        },
        "appId": null,
        "balance": 10,
        "point": 100,
        "taxIssued": false,
        "profitSettlement": false,
        "profit": 0,
        "accountId": "12925149",
        "date": "2019-12-09T00:00:00.000Z",
        "count": {
            "4000": {
                "sms": 10
            }
        }
    },
    {
        "refund": {
            "balance": 0,
            "point": 0
        },
        "appId": null,
        "balance": 10,
        "point": 100,
        "taxIssued": false,
        "profitSettlement": false,
        "profit": 0,
        "accountId": "12925149",
        "date": "2019-12-08T00:00:00.000Z",
        "count": {
            "4000": {
                "sms": 10
            }
        }
    },
    {
        "refund": {
            "balance": 0,
            "point": 0
        },
        "appId": null,
        "balance": 10,
        "point": 100,
        "taxIssued": false,
        "profitSettlement": false,
        "profit": 0,
        "accountId": "12925149",
        "date": "2019-12-07T00:00:00.000Z",
        "count": {
            "4000": {
                "sms": 10
            }
        }
    },
    {
        "refund": {
            "balance": 0,
            "point": 0
        },
        "appId": null,
        "balance": 10,
        "point": 100,
        "taxIssued": false,
        "profitSettlement": false,
        "profit": 0,
        "accountId": "12925149",
        "date": "2019-12-06T00:00:00.000Z",
        "count": {
            "4000": {
                "sms": 10
            }
        }
    },
    {
        "refund": {
            "balance": 0,
            "point": 0
        },
        "appId": null,
        "balance": 10,
        "point": 100,
        "taxIssued": false,
        "profitSettlement": false,
        "profit": 0,
        "accountId": "12925149",
        "date": "2019-12-05T00:00:00.000Z",
        "count": {
            "4000": {
                "sms": 10
            }
        }
    },
    {
        "refund": {
            "balance": 0,
            "point": 0
        },
        "appId": null,
        "balance": 10,
        "point": 100,
        "taxIssued": false,
        "profitSettlement": false,
        "profit": 0,
        "accountId": "12925149",
        "date": "2019-12-04T00:00:00.000Z",
        "count": {
            "4000": {
                "sms": 10
            }
        }
    },
    {
        "refund": {
            "balance": 0,
            "point": 0
        },
        "appId": null,
        "balance": 10,
        "point": 100,
        "taxIssued": false,
        "profitSettlement": false,
        "profit": 0,
        "accountId": "12925149",
        "date": "2019-12-03T00:00:00.000Z",
        "count": {
            "4000": {
                "sms": 10
            }
        }
    },
    {
        "refund": {
            "balance": 0,
            "point": 0
        },
        "appId": null,
        "balance": 10,
        "point": 100,
        "taxIssued": false,
        "profitSettlement": false,
        "profit": 0,
        "accountId": "12925149",
        "date": "2019-12-02T00:00:00.000Z",
        "count": {
            "4000": {
                "sms": 10
            }
        }
    },
    {
        "refund": {
            "balance": 0,
            "point": 0
        },
        "appId": null,
        "balance": 10,
        "point": 100,
        "taxIssued": false,
        "profitSettlement": false,
        "profit": 0,
        "accountId": "12925149",
        "date": "2019-12-01T00:00:00.000Z",
        "count": {
            "4000": {
                "sms": 10
            }
        }
    },
    {
        "refund": {
            "balance": 0,
            "point": 0
        },
        "appId": null,
        "balance": 10,
        "point": 100,
        "taxIssued": false,
        "profitSettlement": false,
        "profit": 0,
        "accountId": "12925149",
        "date": "2019-11-30T00:00:00.000Z",
        "count": {
            "4000": {
                "sms": 10
            }
        }
    },
    {
        "refund": {
            "balance": 0,
            "point": 0
        },
        "appId": null,
        "balance": 10,
        "point": 100,
        "taxIssued": false,
        "profitSettlement": false,
        "profit": 0,
        "accountId": "12925149",
        "date": "2019-11-29T00:00:00.000Z",
        "count": {
            "4000": {
                "sms": 10
            }
        }
    },
    {
        "refund": {
            "balance": 0,
            "point": 0
        },
        "appId": null,
        "balance": 10,
        "point": 100,
        "taxIssued": false,
        "profitSettlement": false,
        "profit": 0,
        "accountId": "12925149",
        "date": "2019-11-28T00:00:00.000Z",
        "count": {
            "4000": {
                "sms": 10
            }
        }
    },
    {
        "refund": {
            "balance": 0,
            "point": 0
        },
        "appId": null,
        "balance": 10,
        "point": 100,
        "taxIssued": false,
        "profitSettlement": false,
        "profit": 0,
        "accountId": "12925149",
        "date": "2019-11-27T00:00:00.000Z",
        "count": {
            "4000": {
                "sms": 10
            }
        }
    },
    {
        "refund": {
            "balance": 0,
            "point": 0
        },
        "appId": null,
        "balance": 10,
        "point": 100,
        "taxIssued": false,
        "profitSettlement": false,
        "profit": 0,
        "accountId": "12925149",
        "date": "2019-11-26T00:00:00.000Z",
        "count": {
            "4000": {
                "sms": 10
            }
        }
    },
    {
        "refund": {
            "balance": 0,
            "point": 0
        },
        "appId": null,
        "balance": 10,
        "point": 100,
        "taxIssued": false,
        "profitSettlement": false,
        "profit": 0,
        "accountId": "12925149",
        "date": "2019-11-25T00:00:00.000Z",
        "count": {
            "4000": {
                "sms": 10
            }
        }
    },
    {
        "refund": {
            "balance": 0,
            "point": 0
        },
        "appId": null,
        "balance": 10,
        "point": 100,
        "taxIssued": false,
        "profitSettlement": false,
        "profit": 0,
        "accountId": "12925149",
        "date": "2019-11-24T00:00:00.000Z",
        "count": {
            "4000": {
                "sms": 10
            }
        }
    },
    {
        "refund": {
            "balance": 0,
            "point": 0
        },
        "appId": null,
        "balance": 10,
        "point": 100,
        "taxIssued": false,
        "profitSettlement": false,
        "profit": 0,
        "accountId": "12925149",
        "date": "2019-11-23T00:00:00.000Z",
        "count": {
            "4000": {
                "sms": 10
            }
        }
    },
    {
        "refund": {
            "balance": 0,
            "point": 0
        },
        "appId": null,
        "balance": 10,
        "point": 100,
        "taxIssued": false,
        "profitSettlement": true,
        "profit": 0,
        "accountId": "12925149",
        "date": "2019-11-22T00:00:00.000Z",
        "count": {
            "4000": {
                "sms": 10
            }
        }
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
  url: 'http://api.coolsms.co.kr/messages/v4/statistics/daily'
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
$url = "http://api.coolsms.co.kr/messages/v4/statistics/daily";

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

url = "http://api.coolsms.co.kr/messages/v4/statistics/daily"
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
	http://api.coolsms.co.kr/messages/v4/statistics/daily
```
{% endtab %}

{% tab title="RUBY" %}

```ruby
require 'net/http'
require 'uri'
require 'json'

uri = URI.parse("http://api.coolsms.co.kr/messages/v4/statistics/daily")

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
  uri := "http://api.coolsms.co.kr/messages/v4/statistics/daily"

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
    String targetUrl = "http://api.coolsms.co.kr/messages/v4/statistics/daily";

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

> 문서 생성일 : 2020-01-02
