# SMS API Version 2



## Overview

이 문서는 REST기반의 문자메시지(국내,해외문자,알림톡,친구톡) API로 예약 문자를 포함한 문자전송, 전송된 문자의 상태 확인, 잔액정보 및 예약취소 등의 작업을 요청하는 방법을 기술하고 있습니다. PHP, Java, Python, Delphi, C 등 다양한 언어로 구현된 샘플을 [SDK](https://developer.coolsms.co.kr/SDK\_ko) 페이지에서 제공하고 있습니다..

모든 Request 호출에는 API Key를 비롯한 인증정보를 포함하여 서버의 인증을 거쳐야 합니다. 인증에 대한 상세한 내용은 [Authentication](https://developer.coolsms.co.kr/REST\_API#Authentication) 을 확인하세요.

인증을 위한 API Key 및 API Secret 코드는 [문자메시지 > 환경설정 > API Key 관리](https://www.coolsms.co.kr/credentials) 메뉴에서 발급 및 관리가 가능합니다. [API Key 관리](https://developer.coolsms.co.kr/Man\_Credentials) 문서를 참고하세요.

아래는 각 Resource의 역할을 테이블로 정리하였습니다. 상세한 설명을 보시려면 해당 Resource를 클릭하여 주세요.

| Part                                                                                                                            | Resource                                                                             | Description |
| ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ | ----------- |
| 그룹메시지                                                                                                                           | [GET new\_group](https://developer.coolsms.co.kr/SMS\_API\_v2#GETnew\_group)         | 그룹 생성       |
| [GET group\_list](https://developer.coolsms.co.kr/SMS\_API\_v2#GETgroup\_list)                                                  | 그룹 목록                                                                                |             |
| [POST delete\_groups](https://developer.coolsms.co.kr/SMS\_API\_v2#POSTdelete\_groups)                                          | 그룹 삭제                                                                                |             |
| [GET groups/{group\_id}](https://developer.coolsms.co.kr/SMS\_API\_v2#GETgroupsgroup\_id)                                       | 그룹 정보 리턴                                                                             |             |
| [POST groups/{group\_id}/add\_messages](https://developer.coolsms.co.kr/SMS\_API\_v2#POSTgroupsgroup\_idadd\_messages)          | 메시지 추가                                                                               |             |
| [POST groups/{group\_id}/add\_messages.json](https://developer.coolsms.co.kr/SMS\_API\_v2#POSTgroupsgroup\_idadd\_messagesjson) | JSON형식으로  메시지 추가                                                                     |             |
| [GET groups/{group\_id}/message\_list](https://developer.coolsms.co.kr/SMS\_API\_v2#GETgroupsgroup\_idmessage\_list)            | 추가된 메시지 목록                                                                           |             |
| [GET groups/{group\_id}/delete\_messages](https://developer.coolsms.co.kr/SMS\_API\_v2#POSTgroupsgroup\_iddelete\_messages)     | 메시지 삭제                                                                               |             |
| [POST groups/{group\_id}/send](https://developer.coolsms.co.kr/SMS\_API\_v2#POSTgroupsgroup\_idsend)                            | 메시지 발송                                                                               |             |
| 이미지                                                                                                                             | [POST upload\_image](https://developer.coolsms.co.kr/SMS\_API\_v2#POSTupload\_image) | 이미지 업로드     |
| [GET image\_list](https://developer.coolsms.co.kr/SMS\_API\_v2#GETimage\_list)                                                  | 이미지 목록                                                                               |             |
| [GET images/{image\_id}](https://developer.coolsms.co.kr/SMS\_API\_v2#GETimagesimage\_id)                                       | 이미지 정보                                                                               |             |
| [POST delete\_images](https://developer.coolsms.co.kr/SMS\_API\_v2#POSTdelete\_images)                                          | 이미지                                                                                  |             |
| 기타                                                                                                                              | [POST send](https://developer.coolsms.co.kr/SMS\_API\_v2#POSTsend)                   | 문자발송 요청     |
| [GET sent](https://developer.coolsms.co.kr/SMS\_API\_v2#GETsent)                                                                | 발송된 문자정보 조회                                                                          |             |
| [POST cancel](https://developer.coolsms.co.kr/SMS\_API\_v2#POSTcancel)                                                          | 예약문자 취소                                                                              |             |
| [GET balance](https://developer.coolsms.co.kr/SMS\_API\_v2#GETbalance)                                                          | 전액정보 조회                                                                              |             |
| [GET status](https://developer.coolsms.co.kr/SMS\_API\_v2#GETstatus)                                                            | 전송채널 상태 조회                                                                           |             |

요청에 대한 응답의 상세는 [Response](https://developer.coolsms.co.kr/REST\_API#Response) 를 확인하세요.

REST API 관련 질의 응답 및 정보 공유는 [개발자포럼](https://developer.coolsms.co.kr/devforum)을 이용해주세요.

## Change Log

| Version | Description                                                    |
| ------- | -------------------------------------------------------------- |
| 1.1     | <p>Android 누리고 푸시 지원<br>1만건 전송을 40초 이하로 단축</p><p>후불제 회원 지원</p> |
| 1.2     | <p>iOS 누리고 푸시 지원<br>1만건 전송을 20초 이하로 단축</p>                     |
| 1.3     | 쿨서포터즈 정책 지원 반영                                                 |
| 1.4     | status 리소스에 시간별, 일별 전송현황을 위한 date, unit 필드 추가                  |
| 1.5     | Agent 정보 전송                                                    |
| 1.6     | 카카오 알림톡 기능 추가                                                  |
| 2.0     | 그룹 메시징 추가                                                      |

## 그룹메시지

대용량의 메시지를 안전하고 빠르게 전송하도록 그룹메시지를 위한 API를 제공합니다.\
아래의 API 호출 흐름으로 대량의 그룹메시지를 보낼 수 있습니다.

```
new_group  ->  add_messages  ->  send
```

new\_group 호출로 메시지를 담을 그룹을 생성하고 리턴된 그룹아이디를 키로 add\_messages 호출로 메시지를 접수하고 send 호출로 접수된 메시지를 서버단에 전송을 수행합니다. 이로 인해 한번 접수된 메시지는 유실 없이 안정적으로 발송이 보장됩니다.&#x20;

### GET new\_group

메시지를 담을 그룹을 생성하여 그룹아이디를 리턴합니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/new\_group](https://api.coolsms.co.kr/sms/2/new\_group)

#### Parameters

| Mandatory | Field               | Description                                                                                                                                                                                                                            |
| --------- | ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Ο         | 인증정보                | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST\_API#Authentication) 참고                                                                                                                                            |
|           | charset             | <p>한글 인코딩 방식을 지정합니다.<br>유니코드 UTF-8 일 경우 utf8,<br>완성형 한글(EUC-KR) 일 경우 euckr 으로 입력,<br>입력 없으면 utf8가 기본</p>                                                                                                                               |
|           | srk                 | <p>솔루션 제공 수수료를 정산받을 솔루션 등록키<br>자세한 안내는 <a href="http://www.coolsms.co.kr/sp">http://www.coolsms.co.kr/sp</a> 을 참고하세요.</p>                                                                                                              |
|           | mode (현재 미지원)       | <p>test로 입력할 경우 CARRIER 시뮬레이터로 시뮬레이션됩니다.</p><p>** 수신번호를 반드시 01000000000 으로 테스트 **<br>예약필드 datetime는 무시됩니다.</p><p>결과값은 60 잔액에서 실제 차감되며 다음날 새벽에 재충전됩니다.</p>                                                                              |
|           | force\_sms (현재 미지원) | <p>누리고푸시를 사용하더라도 강제로 문자 발송.</p><p>true 혹은 false(기본)</p>                                                                                                                                                                                |
|           | only\_              | <p>알림톡이 실패해도 문자메시지로 대체하여 발송하지 않습니다.<br>true 혹은 false(기본)</p>                                                                                                                                                                           |
|           | site\_user          | <p>API를 호출하는 사이트에서 관리하는 유저 아이디 입력.</p><p>미입력시 __private__ 으로 입력됩니다.<br>해당 아이디 앞으로 등록된 발신번호를 확인합니다.<br>발신번호 등록 API를 참고하세요.<br><a href="http://developer.coolsms.co.kr/SenderID_API">http://developer.coolsms.co.kr/SenderID_API</a></p> |
|           | os\_platform        | <p>클라이언트의 OS 및 플랫폼 버전</p><p>예) CentOS 6.6</p><p>(v1.5에서 추가됨)</p>                                                                                                                                                                       |
|           | dev\_lang           | <p>개발 프로그래밍 언어</p><p>예) PHP 5.3.3</p><p>(v1.5에서 추가됨)</p>                                                                                                                                                                               |
|           | sdk\_version        | <p>SDK 버전</p><p>예) PHP SDK 1.5</p><p>(v1.5에서 추가됨)</p>                                                                                                                                                                                  |
|           | app\_version        | <p>어플리케이션 버전</p><p>예) Purplebook 4.1</p><p>(v1.5에서 추가됨)</p>                                                                                                                                                                            |

#### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field     | Description |
| --------- | --------- | ----------- |
| O         | group\_id | 그룹 아이디      |

#### Example Request

```
curl -XGET 'https://api.coolsms.co.kr/sms/2/new_group?api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125'
```

#### Example Response

```
{
  "group_id":"565ba3d7d216a"
}
```

### GET group\_list

생성된 그룹 목록을 리턴합니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/group\_list](https://api.coolsms.co.kr/sms/2/group\_list)

#### Parameters

| Mandatory | Field | Description                                                                                 |
| --------- | ----- | ------------------------------------------------------------------------------------------- |
| Ο         | 인증정보  | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST\_API#Authentication) 참고 |

#### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field | Description           |
| --------- | ----- | --------------------- |
| O         | -     | array 형식의 그룹아이디 목록 리턴 |

#### Example Request

```
curl -XGET 'https://api.coolsms.co.kr/sms/2/group_list?api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125'
```

#### Example Response

```
[
    "565ba3d7d216a",
    "565ba3dea161b"
]
```

### POST delete\_groups

그룹을 삭제합니다. 담겨 있는 메시지도 함께 삭제됩니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/delete\_groups](https://api.coolsms.co.kr/sms/2/delete\_groups)

#### Parameters

| Mandatory | Field      | Description                                                                                 |
| --------- | ---------- | ------------------------------------------------------------------------------------------- |
| Ο         | 인증정보       | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST\_API#Authentication) 참고 |
| O         | group\_ids | <p>삭제할 그룹 아이디</p><p>콤마(,)로 구분된 아이디 목록 입력 가능</p>                                             |

#### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field          | Description                                 |
| --------- | -------------- | ------------------------------------------- |
| O         | success\_count | 삭제된 그룹 갯수                                   |
| O         | error\_count   | 오류 처리된 그룹 갯수                                |
| O         | error\_list    | <p>오류 내역<br>["{인덱스}": "{오류코드}", ...] 형식</p> |

#### Example Request

```
curl -XPOST 'https://api.coolsms.co.kr/sms/2/delete_groups' -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&group_ids=565ba3d7d216a'
```

#### Example Response

```
{
  "success_count": 3,
  "error_count": 2,
  "error_list": [
    4: "62",
    5: "54"
  ]
}
```

### GET groups/{group\_id}

그룹 정보를 리턴합니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/groups/{group\_id}](https://api.coolsms.co.kr/sms/2/groups/%7Bgroup\_id%7D)

#### Parameters

| Mandatory | Field     | Description                                                                                 |
| --------- | --------- | ------------------------------------------------------------------------------------------- |
| Ο         | 인증정보      | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST\_API#Authentication) 참고 |
| O         | group\_id | 그룹 아이디                                                                                      |

#### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field          | Description   |
| --------- | -------------- | ------------- |
| O         | group\_id      | 그룹 아이디        |
| O         | message\_count | 그룹에 담긴 메시지 갯수 |

#### Example Request

```
curl -XGET 'https://api.coolsms.co.kr/sms/2/groups/{group_id}' -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&group_id=565ba3d7d216a'
```

#### Example Response

```
{
  "group_id":"565ba3d7d216a",
  "message_count":970
}
```

### POST groups/{group\_id}/add\_messages

그룹에 발송할 문자메시지를 추가합니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/groups/{group\_id}/add\_messages](https://api.coolsms.co.kr/sms/2/groups/%7Bgroup\_id%7D/add\_messages)

#### Parameters

| Mandatory | Field          | Description                                                                                                              |
| --------- | -------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Ο         | 인증정보           | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST\_API#Authentication) 참고                              |
| O         | to             | <p>수신번호 입력<br>콤마(,)로 구분된 수신번호 입력가능<br>예) 01012345678,01023456789,01034567890</p>                                         |
| O         | from           | <p>발신번호 입력<br>2015/10/16 발신번호 사전등록제에 의해 반드시 등록된 번호만 허용됩니다. (해외문자 제외)<br>예) 0212345678</p>                                |
| O         | text           | 문자내용                                                                                                                     |
|           | type           | <p>CTA(친구톡), ATA(알림톡), SMS(90바이트), LMS(장문 2,000바이트), MMS(장문+이미지)<br>미입력시 SMS<br>해외문자인 경우 SMS만 가능</p>                     |
|           | image\_id      | <p>발송할 이미지의 아이디</p><p>type이 MMS일 때 필수</p>                                                                                |
|           | refname        | 참조내용(이름)                                                                                                                 |
|           | country        | <p>한국: 82, 일본: 81, 중국: 86, 미국: 1, 기타 등등 (기본 한국)</p><p><a href="http://countrycode.org">http://countrycode.org</a> 참고</p> |
|           | datetime       | <p>예약시간을 YYYYMMDDHHMISS 포맷으로 입력 (입력 없거나 지난날짜를 입력하면 바로 전송)<br>예) 20131216090510 (2013년 12월 16일 9시 5분 10초에 발송되도록 예약)</p>   |
|           | subject        | LMS, MMS 일때 제목 (40바이트)                                                                                                   |
|           | template\_code | 알림톡 Template Code                                                                                                        |
|           | sender\_key    | 알림톡 Sender Key                                                                                                           |
|           | button\_name   | 알림톡&친구톡 버튼이름                                                                                                             |
|           | button\_url    | 알림톡&친구톡 버튼URL                                                                                                            |

**제한 사항**

to 필드의 전화번호 수는 최대 1,000개이며 넘을 경우 오류를 발생 (RecipientsTooMany)

한번의 Request의 총 데이터 크기는 2MB를 넘을 수 없습니다 (HTTP ERROR 413 발생)

**발송형태별 제한사항**

이동통신사 내부적으로 완성형한글로 변환되므로 영어 1바이트, 한글 2바이트로 취급됩니다.

| 구분  | 제한사항                                                                                           |
| --- | ---------------------------------------------------------------------------------------------- |
| SMS | 90바이트 까지 전송가능 (한글 45자)                                                                         |
| LMS | 2,000바이트 까지 전송가능 (한글 1,000자)                                                                   |
| MMS | <p>2,000바이트 텍스트 (한글 1,000자)</p><p>1개의 이미지 전송 (300KB. 2048x2048픽셀 이하인 JPEG, PNG, GIF 형식 파일)</p> |
| ATA | 카카오톡 알림톡으로 1,000자까지 발송, 친구등록이 안되어있는 계정에게도 발송가능                                                 |
| CTA | 카카오톡 찬구톡으로 1,000자까지 발송, 친구등록이 되어있어야 발송가능                                                       |

#### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field          | Description                                                              |
| --------- | -------------- | ------------------------------------------------------------------------ |
| O         | success\_count | 접수 성공 갯수                                                                 |
| O         | error\_count   | 접수 오류 갯수                                                                 |
|           | error\_list    | <p>오류 발생 문자메시지 아이디 목록<br>["{인덱스}": "{오류코드}", ...] 형식<br>인덱스값은 0부터 시작</p> |

#### Example Request

```
curl -XPOST https://api.coolsms.co.kr/sms/2/groups/GID565bA3D7D216A/add_messages -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&to=01012345678&from=029302266&text=Hello'
```

#### Example Response

```
{
  "success_count": 3,
  "error_count": 2,
  "error_list": [
    0: "62",
    4: "54"
  ]
}
```

추가하신 메시지의 전체 개수가 success\_count로 리턴되면 정상적으로 서버에 접수 완료된 것이며, 에러가 발생한 메시지는 error count 와 error\_list 가 리턴됩니다.\
리턴된 error\_code의 정보는 [http://developer.coolsms.co.kr/Legacy\_Result\_Codes](http://developer.coolsms.co.kr/Legacy\_Result\_Codes) 을 참고하시면 됩니다. 여기서 리턴되는 Response의 내용은 서버에 전송 요청한 것에 대한 정보이며 실제 휴대전화로 전송한 것에 대한 정보가 아닙니다.  sent 조회로 실제 전송된 결과를 확인하실 수 있습니다.

### POST groups/{group\_id}/add\_messages.json

그룹에 발송할 문자메시지를 JSON 형식으로 접수합니다. 대량의 문자를 각각 다른 내용과 타입으로 보내고 싶을 때 용이 합니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/groups/{group\_id}/add\_messages.json](https://api.coolsms.co.kr/sms/2/groups/%7Bgroup\_id%7D/add\_messages.json)

#### Parameters

| Mandatory | Field    | Description                                                                                 |
| --------- | -------- | ------------------------------------------------------------------------------------------- |
| Ο         | 인증정보     | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST\_API#Authentication) 참고 |
| O         | messages | JSON 형식의 메시지 데이터                                                                            |

**JSON Fields**

| Mandatory | Field          | Description                                                                                                              |
| --------- | -------------- | ------------------------------------------------------------------------------------------------------------------------ |
| O         | to             | <p>수신번호 입력<br>콤마(,)로 구분된 수신번호 입력가능<br>예) 01012345678,01023456789,01034567890</p>                                         |
| O         | from           | <p>발신번호 입력<br>2015/10/16 발신번호 사전등록제에 의해 반드시 등록된 번호만 허용됩니다. (해외문자 제외)<br>예) 0212345678</p>                                |
| O         | text           | 문자내용                                                                                                                     |
|           | type           | <p>ATA(알림톡), CTA(친구톡), SMS(90바이트), LMS(장문 2,000바이트), MMS(장문+이미지)<br>미입력시 SMS<br>해외문자인 경우 SMS만 가능</p>                     |
|           | image\_id      | <p>발송할 이미지의 아이디</p><p>type이 MMS일 때 필수</p>                                                                                |
|           | refname        | 참조내용(이름)                                                                                                                 |
|           | country        | <p>한국: 82, 일본: 81, 중국: 86, 미국: 1, 기타 등등 (기본 한국)</p><p><a href="http://countrycode.org">http://countrycode.org</a> 참고</p> |
|           | datetime       | <p>예약시간을 YYYYMMDDHHMISS 포맷으로 입력 (입력 없거나 지난날짜를 입력하면 바로 전송)<br>예) 20131216090510 (2013년 12월 16일 9시 5분 10초에 발송되도록 예약)</p>   |
|           | subject        | LMS, MMS 일때 제목 (40바이트)                                                                                                   |
|           | template\_code | 알림톡 Template Code                                                                                                        |
|           | sender\_key    | 알림톡 Sender Key                                                                                                           |

#### messages 포맷

\[ ] 안에 { } 가 여러 개 들어 갈 수 있는 구조로 되어있으며 각각의 { } 안에는 to, from, text 필드가 필수요소입니다.

```
[
  {
    "type": "SMS",
    "to": "01000000000,01011111111,01022222222",
    "from": "021234567",
    "text": "Hello A"
  },
  {
    "type": "LMS",
    "to": "01000000000,01011111111,01022222222",
    "from": "021234567",
    "text": "Hello B"
    "subject": "LMS Subject",
  },
  {
    "type": "MMS",
    "to": "01000000000,01011111111,01022222222",
    "from": "021234567",
    "text": "Hello C",
    "subject": "MMS Subject",
    "image_id": "abcdefg"
  }
]
```

**제한 사항**

수신받을 전화번호 총 수(to 필드 전화번호 합계)는 최대 1,000개이며 넘을 경우 오류 발생. (RecipientsTooMany)

한번의 Request의 총 데이터 크기는 2MB를 넘을 수 없습니다 (HTTP ERROR 413 발생)

**발송형태에 따른 제한사항**

이동통신사 내부적으로 완성형한글로 변환되므로 영어 1바이트, 한글 2바이트로 취급됩니다.

| 구분  | 제한사항                                                                                           |
| --- | ---------------------------------------------------------------------------------------------- |
| SMS | 90바이트 까지 전송가능 (한글 45자)                                                                         |
| LMS | 2,000바이트 까지 전송가능 (한글 1,000자)                                                                   |
| MMS | <p>2,000바이트 텍스트 (한글 1,000자)</p><p>1개의 이미지 전송 (300KB. 2048x2048픽셀 이하인 JPEG, PNG, GIF 형식 파일)</p> |
| ATA | 카카오톡 알림톡으로 1,000자까지 발송, 친구등록이 안되어있는 계정에게도 발송가능                                                 |
| CTA | 카카오톡 찬구톡으로 1,000자까지 발송, 친구등록이 되어있어야 발송가능                                                       |

#### &#x20;JSON 포맷으로 리턴 됩니다.Response

| Mandatory | Field          | Description                                                              |
| --------- | -------------- | ------------------------------------------------------------------------ |
| O         | success\_count | 접수 성공 갯수                                                                 |
| O         | error\_count   | 접수 오류 갯수                                                                 |
|           | error\_list    | <p>오류 발생 문자메시지 아이디 목록<br>["{인덱스}": "{오류코드}", ...] 형식<br>인덱스값은 0부터 시작</p> |

#### Example Request

```
curl -XPOST https://api.coolsms.co.kr/sms/2/groups/565ba3d7d216a/add_messages -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&messages=JSONArray
```

#### Example Response

```
[
  {
    "success_count": 3,
    "error_count": 0,
  },
  {
    "success_count": 1,
    "error_count": 2,
    "error_list": [
      0: "62",
      1: "54"
    ]
  },
  {
    "success_count": 3,
    "error_count": 0,
  }
]
```

추가하신 메시지의 전체 개수가 success\_count로 리턴되면 정상적으로 서버에 접수 완료된 것이며, 에러가 발생한 메시지는 error count 와 error\_list 가 리턴됩니다.\
리턴된 error\_code의 정보는 [http://www.coolsms.co.kr/Legacy\_Result\_Codes](http://www.coolsms.co.kr/Legacy\_Result\_Codes) 을 참고하시면 됩니다. 여기서 리턴되는 Response의 내용은 서버에 전송 요청한 것에 대한 정보이며 실제 휴대전화로 전송한 것에 대한 정보가 아닙니다.  sent 조회로 실제 전송된 결과를 확인하실 수 있습니다.

### GET groups/{group\_id}/message\_list

문자메시지 목록을 리턴합니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/groups/{group\_id}/message\_list](https://api.coolsms.co.kr/sms/2/groups/%7Bgroup\_id%7D/message\_list)

#### Parameters

| Mandatory | Field  | Description                                                                                 |
| --------- | ------ | ------------------------------------------------------------------------------------------- |
| Ο         | 인증정보   | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST\_API#Authentication) 참고 |
|           | offset | <p>조회할 목록의 시작 위치</p><p>Default) 0</p>                                                       |
|           | limit  | <p>가져올 메시지의 갯수</p><p>Default) 20</p>                                                        |

#### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field        | Description      |
| --------- | ------------ | ---------------- |
| O         | total\_count | 전체 메시지 갯수        |
| O         | offset       | 조회 목록의 시작 위치     |
| O         | limit        | 가져올 메시지의 갯수      |
| O         | list         | Array 형식의 메시지 목록 |

#### Example Request

```
curl -XGET 'https://api.coolsms.co.kr/sms/2/groups/{group_id}/message_list' -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125'
```

#### Example Response

```
{
  "total_count":2,
  "offset":0,
  "limit":20,
  "list":[
     "565ba4e7d316b",
     "565ab383dabcd"
  ]
}
```

### POST groups/{group\_id}/delete\_messages

그룹에 추가된 메시지를 삭제합니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/groups/{group\_id}/delete\_messages](https://api.coolsms.co.kr/sms/2/groups/%7Bgroup\_id%7D/delete\_messages)

#### Parameters

| Mandatory | Field        | Description                                                                                 |
| --------- | ------------ | ------------------------------------------------------------------------------------------- |
| Ο         | 인증정보         | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST\_API#Authentication) 참고 |
| O         | message\_ids | <p>콤마로 구분된 삭제할 메시지 아이디 목록</p><p>ex) MID565BA6D7E325C,MID565433E7D233A</p>                   |

#### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field          | Description                                                       |
| --------- | -------------- | ----------------------------------------------------------------- |
| O         | success\_count | 삭제 성공 갯수                                                          |
| O         | error\_count   |  오류 갯수                                                            |
|           | error\_list    | <p>오류 발생 코드 목록<br>["{인덱스}": "{오류코드}", ...] 형식<br>인덱스값은 0부터 시작</p> |

#### Example Request

```
curl -XPOST 'https://api.coolsms.co.kr/sms/2/groups/{group_id}/delete_messages' -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&message_ids=MID565BA6D7E325C,MID565433E7D233A,MID565643A66AB21'
```

#### Example Response

서버는 json 포맷으로 삭제된 갯수를 리턴합니다.

```
{
  "success_count": 1,
  "error_count": 2,
  "error_list": [
    0: "1021",
    2: "1021"
  ]
}
```

### POST groups/{group\_id}/send

그룹메시지를 전송 요청합니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/groups/{group\_id}/send](https://api.coolsms.co.kr/sms/2/groups/%7Bgroup\_id%7D/send)

#### Parameters

| Mandatory | Field | Description                                                                                 |
| --------- | ----- | ------------------------------------------------------------------------------------------- |
| Ο         | 인증정보  | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST\_API#Authentication) 참고 |

#### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field     | Description   |
| --------- | --------- | ------------- |
| O         | group\_id | 전송 요청된 그룹 아이디 |

#### Example Request

```
curl -XPOST 'https://api.coolsms.co.kr/sms/2/groups/{group_id}/send' -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125'
```

#### Example Response

```
{
  "group_id": "565ba3d7d216a"
}
```

## 이미지

이미지를 서버에 안전하게 미리 업로드하여 문자발송 때 사용할 수 있어 더욱 안정적인 발송을 보장합니다.

### POST upload\_image

MMS 발송에 필요한 이미지 파일을 업로드 합니다.

MMS 발송 때 미리 업로드 된 이미지 파일을 사용하므로 발송과정에서 발생하는 오류률 현저히 줄어듭니다.

이미지 보관 기간은 7일입니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/upload\_image](https://api.coolsms.co.kr/sms/2/upload\_image)

#### Parameters

| Mandatory | Field           | Description                                                                                                                          |
| --------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Ο         | 인증정보            | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST\_API#Authentication) 참고                                          |
| O         | image           | <p>이미지 내용 (파일명이 아니라 내용입니다.)<br>Form Submit 옵션 : method=POST enc-type=multipart/form<br>제한사항) 300KB, 2048x2048 이하, JPEG, PNG, GIF</p> |
|           | image\_encoding | 이미지 인코딩 방식 binary(Default), base64                                                                                                   |

#### Response

JSON 포맷으로 리턴 됩니다.\
리턴되는 image\_id를 MMS 발송 시 {group\_id}/add\_messages 파라메터로 입력하셔야 합니다.

| Mandatory | Field     | Description |
| --------- | --------- | ----------- |
| O         | image\_id | 이미지 아이디     |

#### Example Request

```
curl -XPOST 'https://api.coolsms.co.kr/sms/2/upload_image' -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125' -F 'image=@/path/to/my/file'
```

#### Example Response

```
{
  "image_id": IMG565BA2D9E4239"
}
```

### GET image\_list

서버에 업로드 되어 있는 이미지 목록을 리턴합니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/image\_list](https://api.coolsms.co.kr/sms/2/image\_list)

#### Parameters

| Mandatory | Field  | Description                                                                                 |
| --------- | ------ | ------------------------------------------------------------------------------------------- |
| Ο         | 인증정보   | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST\_API#Authentication) 참고 |
|           | offset | <p>조회할 목록의 시작 위치<br>Default) 0</p>                                                          |
|           | limit  | <p>가져올 이미지 아이디의 갯수<br>Default) 20</p>                                                       |

#### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field        | Description          |
| --------- | ------------ | -------------------- |
| O         | total\_count | 전체 메시지 갯수            |
| O         | offset       | 조회 목록의 시작 위치         |
| O         | limit        | 가져올 이미지 아이디의 갯수      |
| O         | list         | Array 형식의 이미지 아이디 목록 |

#### Example Request

```
curl -XGET 'https://api.coolsms.co.kr/sms/2/image_list' -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125'
```

#### Example Response

```
{
  "total_count":3,
  "offset":0,
  "limit":20,
  "list":[
    "IMG565BA6D7D327C",
    "IMG565BA7ABD338B",
    "IMG565BB9D7D21C7"
  ]
}
```

### GET images/{image\_id}

업로드된 이미지 정보를 리턴합니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/images/{image\_id}](https://api.coolsms.co.kr/sms/2/images/%7Bimage\_id%7D)

#### Parameters

| Mandatory | Field | Description                                                                                 |
| --------- | ----- | ------------------------------------------------------------------------------------------- |
| Ο         | 인증정보  | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST\_API#Authentication) 참고 |

#### Response

해당 이미지의 정보가 JSON 포맷으로 리턴 됩니다.

| Mandatory | Field          | Description     |
| --------- | -------------- | --------------- |
| O         | image\_id      | 이미지 아이디         |
| O         | file\_name     | 파일 명            |
| O         | original\_name | 원본 파일 명         |
| O         | file\_size     | 파일 크기 (Byte 단위) |
| O         | width          | 이미지 가로 픽셀       |
| O         | height         | 이미지 세로 픽셀       |

#### Example Request

```
curl -XGET 'https://api.coolsms.co.kr/sms/2/images/{image_id}' -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125'
```

#### Example Response

```
{
  "image_id":"566fb2266316f",
  "file_name","566fb2266316f.jpg",
  "original_name":"nurigo-200x100.jpg",
  "file_size":"4990",
  "width":"200",
  "height":"100"
}
```

### POST delete\_images

이미지 파일을 삭제합니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/delete\_images](https://api.coolsms.co.kr/sms/2/delete\_images)

#### Parameters

| Mandatory | Field      | Description                                                                                 |
| --------- | ---------- | ------------------------------------------------------------------------------------------- |
| Ο         | 인증정보       | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST\_API#Authentication) 참고 |
| O         | image\_ids | <p>콤마로 구분된 삭제 할 이미지 ID 목록<br>예) IMG565BA6D7E325C,IMG565433E7D233A</p>                       |

#### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field          | Description                                                              |
| --------- | -------------- | ------------------------------------------------------------------------ |
| O         | success\_count | 삭제 성공 갯수                                                                 |
| O         | error\_count   | 삭제 오류 갯수                                                                 |
|           | error\_list    | <p>오류 발생 문자메시지 아이디 목록<br>["{인덱스}": "{오류코드}", ...] 형식<br>인덱스값은 0부터 시작</p> |

#### Example Request

```
curl -XPOST 'https://api.coolsms.co.kr/sms/2/delete_images' -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&image_ids=IMG565BA2D9E4239,IMG565AB2E4A5134,IMG565BB3A4B4342'
```

#### Example Response

```
{
  "success_count": 1,
  "error_count": 2,
  "error_list": [
    0: "1023",
    2: "1024"
  ]
}
```

## POST send

문자메시지를 전송 요청합니다. 전송 요청에 대한 Response는 휴대전화까지 전송된 결과가 아닙니다.

### Resource URL

[https://api.coolsms.co.kr/sms/2/send](https://api.coolsms.co.kr/sms/2/send)

### Parameters

| Mandatory | Field               | Description                                                                                                              |
| --------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Ο         | 인증정보                | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST\_API#Authentication) 참고                              |
| O         | to                  | 수신번호 입력 콤마(,)로 구분된 수신번호 입력가능 예) 01012345678,01023456789,01034567890                                                      |
| O         | from                | <p>발신번호 예) 0212345678<br>2015/10/16 발신번호 사전등록제에 의해 반드시 등록된 번호만 허용됩니다. (해외문자 제외)</p>                                      |
| O         | text                | 문자내용                                                                                                                     |
|           | type                | CTA(친구톡), ATA(알림톡), SMS(80바이트), LMS(장문 2,000바이트), MMS(장문+이미지) 입력 없으면 SMS가 기본 국가코드가 KR이 아니면 SMS로 강제                       |
|           | template\_code      | 알림톡 Template Code                                                                                                        |
|           | sender\_key         | 알림톡 Sender Key                                                                                                           |
|           | image               | 지원형식 : 300KB 이하의 JPEG, PNG, GIF 형식의 파일 2048x2048 픽셀이하                                                                    |
|           | image\_encoding     | 이미지 인코딩 방식 binary(Default), base64                                                                                       |
|           | refname             | 참조내용(이름)                                                                                                                 |
|           | country             | <p>한국: 82, 일본: 81, 중국: 86, 미국: 1, 기타 등등 (기본 한국)</p><p><a href="http://countrycode.org">http://countrycode.org</a> 참고</p> |
|           | datetime            | 예약시간을 YYYYMMDDHHMISS 포맷으로 입력 (입력 없거나 지난날짜를 입력하면 바로 전송) 예) 20131216090510 (2013년 12월 16일 9시 5분 10초에 발송되도록 예약)             |
|           | subject             | LMS, MMS 일때 제목 (40바이트)                                                                                                   |
|           | charset             | 한글 인코딩 방식 지정 유니코드 UTF-8 일 경우 utf8 완성형 한글(EUC-KR) 일 경우 euckr 으로 입력 입력 없으면 utf8가 기본                                        |
|           | srk                 | 솔루션 제공 수수료를 정산받을 솔루션 등록키                                                                                                 |
|           | mode (현재 미지원)       | test로 입력할 경우 CARRIER 시뮬레이터로 시뮬레이션됨 수신번호를 반드시 01000000000 으로 테스트하세요. 예약필드 datetime는 무시됨 결과값은 60 잔액에서 실제 차감되며 다음날 새벽에 재충전됨 |
|           | force\_sms (현재 미지원) | <p>누리고푸시를 사용하더라도 SMS로 발송되도록 강제</p><p>true 혹은 false(기본)</p>                                                               |
|           | only\_ata           | <p>알림톡이 실패해도 문자메시지로 대체하여 발송하지 않습니다.</p><p>true 혹은 false(기본)</p>                                                          |
|           | os\_platform        | <p>클라이언트의 OS 및 플랫폼 버전) CentOS 6.6</p><p>(v1.5에서 추가됨)</p>                                                                 |
|           | dev\_lang           | <p>개발 프로그래밍 언어 예) PHP 5.3.3</p><p>(v1.5에서 추가됨)</p>                                                                       |
|           | sdk\_version        | <p>SDK 버전 예) PHP SDK 1.5</p><p>(v1.5에서 추가됨)</p>                                                                          |
|           | app\_version        | <p>어플리케이션 버전 예) Purplebook 4.1</p><p>(v1.5에서 추가됨)</p>                                                                    |
|           | button\_name        | 알림톡&친구톡 버튼이름                                                                                                             |
|           | button\_url         | 알림톡&친구톡 버튼URL                                                                                                            |

Mandatory가 Ο 인 필드는 반드시 입력하여야 합니다.

srk 는 앱아이디를 말하는 것으로 [https://www.coolsms.co.kr/me/apps](https://www.coolsms.co.kr/me/apps) 을 참고하세요.

한번의 Request에 extension을 포함하여 총 받는사람(to) 수는 1000개 까지가 제한이며 1000개가 넘을 경우 오류를 발생시킵니다. (RecipientsTooMany)

한번의 Request의 총 크기는 2MB를 넘을 수 없습니다. (HTTP ERROR 413 발생)

#### 발송형태에 따른 제한사항

이동통신사 내부적으로 완성형한글로 변환되므로 영어 1바이트, 한글 2바이트로 취급됩니다.

| 구분  | 제한사항                                                                                            |
| --- | ----------------------------------------------------------------------------------------------- |
| SMS | 90바이트 까지 전송가능 (한글 45자)                                                                          |
| LMS | 2,000바이트 까지 전송가능 (한글 1,000자)                                                                    |
| MMS | <p>2,000바이트 텍스트(한글 1,000자)</p><p>1개의 이미지 전송(300KB 이하의 JPEG, PNG, GIF 형식의 파일 2048x2048 픽셀이하)</p> |
| ATA | 카카오톡 알림톡으로 1,000자까지 발송, 친구등록이 안되어 있어도 발송가능                                                      |
| CTA | 카카오톡 친구톡으로 1,000자까지 발송, 친구등록된 계정에게만 발송가능                                                        |

### Response

| Mandatory | Field           | Description |
| --------- | --------------- | ----------- |
| O         | group\_id       | 그룹아이디       |
| O         | success\_count  | 성공 건수       |
| O         | error\_count    | 오류 건수       |
| O         | result\_code    | 마지막 오류 코드   |
| O         | result\_message | 마지막 오류 메시지  |

result\_code 가 00 이면 정상적인 접수이며 이 외의 코드는 [http://www.coolsms.co.kr/Legacy\_Result\_Codes](http://www.coolsms.co.kr/Legacy\_Result\_Codes) 을 참고하세요. 여기서 리턴되는 Response의 내용은 서버에게 전송을 요청한 것에 대한 정보이지 실제 휴대전화로 전송한 것에 대한 정보가 아닙니다. 예를 들어 요청 건수 중 success\_count가 10개라면 서버의 DB에 안전하게 INSERT된 건이 10개라는 의미이며, 나중 sent 리소스를 통해 조회시 이통사를 통해 실제 전송성공된 건수는 8개이고 올바르지 못한 수신번호로 2개로 실패라는 결과가 나올 수 있습니다.

메시지그룹ID(group\_id)는 Request된 메시지들의대표하는 아이디값으로 메시지상태 및 예약취소할 때 키값으로 사용될 수 있습니다. 10건의 문자메시지를 발송할 경우 그 10건의 문자메시지를 대표하는 group\_id 가 리턴되며 sent 리소스를 통해서 10건에 대한 전송상태를 조회할 수 있습니다.

### **Example Request**

```
curl -XPOST https://api.coolsms.co.kr/sms/2/send -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&to=01012345678,01023456789,01034567890&from=029302266&text=Hello'
```

### **Example Response**

서버는 json 포맷으로 접수결과를 리턴합니다.

```
{
  "group_id": "20120217103829612403761364",
  "success_count": 2,
  "error_count": 0,
  "result_code": "00",
  "result_message": "Success"
}
```

## GET sent

발송된 문자메시지의 목록을 가져옵니다.&#x20;

### Resource URL

[https://api.coolsms.co.kr/sms/2/sent](https://api.coolsms.co.kr/sms/2/sent)

### Parameters

| Mandatory | Field             | Description                                                                                 |
| --------- | ----------------- | ------------------------------------------------------------------------------------------- |
| Ο         | 인증정보              | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST\_API#Authentication) 참고 |
|           | offset            | 가져올 목록의 시작 위치                                                                               |
|           | limit             | 기본값 20이며 20개의 목록을 받을 수 있음. 40입력시 40개의 목록이 리턴                                                |
|           | rcpt              | 수신번호로 검색                                                                                    |
|           | start             | 검색 시작일시 접수 날짜와 시간으로 검색 YYYY-MM-DD HH:MI:SS 포맷의 날짜와 시간                                       |
|           | end               | 검색 종료일시 접수 날짜와 시간으로 검색 YYYY-MM-DD HH:MI:SS 포맷의 날짜와 시간                                       |
|           | status            | 메시지 상태 값으로 검색                                                                               |
|           | resultcode        | 전송결과 값으로 검색                                                                                 |
|           | notin\_resultcode | 입력된 전송결과 값 이외의 건들만 조회                                                                       |
|           | message\_id       | 메시지ID                                                                                       |
|           | group\_id         |  ID                                                                                         |

검색 옵션이 없는 경우 가장 최신의 발송건부터 20일 전까지 내림차순으로 페이지 단위의 목록을 리턴합니다.

### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field        | Description |
| --------- | ------------ | ----------- |
| O         | total\_count | 전체 카운트      |
| O         | list\_count  | ...         |

### Example Request

```
curl -XGET https://api.coolsms.co.kr/sms/2/sent -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&salt=abc&offset=0&limit=20'
```

### **Example Response**

Response Format은 json을 사용합니다.

```
{
  "total_count":"169",
  "list_count":4,
  "page":1,
  "data":[
    {
      "type":"SMS",
      "accepted_time":"2014-01-07 18:14:54",
      "recipient_number":"01000000000",
      "group_id":"G52CBC596955F0",
      "message_id":"M52CBC59695B31",
      "status":"2",
      "result_code":"58",
      "result_message":"\uc804\uc1a1\uacbd\ub85c \uc5c6\uc74c",
      "sent_time":"L",
      "text":"Test Message",
      "carrier":"SKT",
      "scheduled_time":"201401071814"
    },
    {
      "type":"SMS",
      "accepted_time":"2014-01-07 18:14:41",
      "recipient_number":"01000000000",
      "group_id":"G52CBC5897645A",
      "message_id":"M52CBC58976A64",
      "status":"2",
      "result_code":"58",
      "result_message":"\uc804\uc1a1\uacbd\ub85c \uc5c6\uc74c",
      "sent_time":"201401071814",
      "text":"message\nhere",
      "carrier":"KTF",
      "scheduled_time":"201401071814"
    },
    {
      "type":"SMS",
      "accepted_time":"2014-01-07 18:11:23",
      "recipient_number":"01000000000",
      "group_id":"G52CBC4C35B3A8",
      "message_id":"M52CBC4C35BA70",
      "status":"2",
      "result_code":"58",
      "result_message":"\uc804\uc1a1\uacbd\ub85c \uc5c6\uc74c",
      "sent_time":"201401071811",
      "text":"message\nhere",
      "carrier":"LGT",
      "scheduled_time":"201401071814"
    },
    {
      "type":"SMS",
      "accepted_time":"2014-01-06 12:42:32",
      "recipient_number":"01012345678",
      "group_id":"G52CA262EC447D",
      "message_id":"M52CA262EC49D8",
      "status":"2",
      "result_code":"00",
      "result_message":"\uc815\uc0c1",
      "sent_time":"201401061257",
      "text":"\ud14c\uc2a4\ud305hi there~",
      "carrier":"KTF",
      "scheduled_time":"201401071814"
    }
  ]
}
```

#### status

| Status Code | Description   |
| ----------- | ------------- |
| 0           | 대기중           |
| 1           | 이통사로 전송중      |
| 2           | 이통사로부터 리포트 도착 |

result\_code 는 [http://www.coolsms.co.kr/Legacy\_Result\_Codes](https://developer.coolsms.co.kr/Legacy\_Result\_Codes) 페이지를 참고 하세요.

## POST cancel

예약된 문자메시지를 취소합니다. 예약되지 않았거나, 예약되었으나 이미 발송된 문자메시지는 취소 할 수 없습니다.

### Resource URL

[https://api.coolsms.co.kr/sms/2/cancel](https://api.coolsms.co.kr/sms/2/cancel)

### Parameters

| Mandatory | Field       | Description                                                                                 |
| --------- | ----------- | ------------------------------------------------------------------------------------------- |
| Ο         | 인증정보        | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST\_API#Authentication) 참고 |
|           | message\_id | 메시지ID                                                                                       |
|           | group\_id   | 그룹ID                                                                                        |

message\_id 혹은 group\_id 중 하나는 반드시 입력하세요.

### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field        | Description |
| --------- | ------------ | ----------- |
| O         | total\_count | 전체 카운트      |
| O         | list\_count  | ...         |

## GET balance

잔액을 확인합니다.

### Resource URL

[https://api.coolsms.co.kr/sms/2/balance](https://api.coolsms.co.kr/sms/2/balance)

### Parameters

| Mandatory | Field | Description                                                                                 |
| --------- | ----- | ------------------------------------------------------------------------------------------- |
| Ο         | 인증정보  | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST\_API#Authentication) 참고 |

### Response

Response Format은 json을 사용합니다.

```
{
  "cash": "23900",
  "point": "890"
}
```

## GET status

전송채널의 상태를 조회합니다.

### Resource URL

[https://api.coolsms.co.kr/sms/2/status](https://api.coolsms.co.kr/sms/2/status)

### Parameters

| Mandatory | Field   | Description                                                                                                                         |
| --------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Ο         | 인증정보    | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST\_API#Authentication) 참고                                         |
|           | count   | 기본값 1이며 1개의 최신의 레코드를 받을 수 있음, 10입력시 10분 동안의 레코드 목록을 리턴                                                                              |
|           | unit    | <p>minute(default), hour, day 중 하나<br>minute : 분 단위의 현황<br>hour : 시간 단위의 평균<br>day : 일 단위의 평균<br>(v1.4에서 추가)</p>                    |
|           | date    | <p>데이터를 읽어오는 기준 시각으로 YYYYMMDDHHMISS 형식의 14자리 값<br>예) 20150331095101 (2015년 3월 31일 오전 9시 51분 1초)<br>기본값 : 현재시각</p><p>(v1.4에서 추가)</p> |
|           | channel | <p>1: 1건 발송 채널 (기본 값)</p><p>2: 대량 발송 채널<br>(v1.4에서 추가)</p>                                                                          |

### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field        | Description |
| --------- | ------------ | ----------- |
| O         | registdate   | 입력일         |
| O         | sms\_average | ...         |

모든 항목의 값은 초단위(seconds)값입니다. sms\_average와 mms\_average는 각각 SMS채널과 MMS채널의 문자가 접수된 때부터 실제 수신되기까지 걸린 시간으로 계산된 평균값으로 리포트가 오지않은 대기중인 메시지를 합산한 값이므로 다소 높게 나와도 정상입니다. sk, kt, lg 의 경우 수신시각이 분단위로만 제공되어서 약간의 차이가 날 수 있습니다.

### Response Example

```
[
  {
    "registdate": "2014-02-25 10:34:01",
    "sms_average": "23",
    "sms_sk_average": "9",
    "sms_kt_average": "10",
    "sms_lg_average": "11",
    "mms_average": "52",
    "mms_sk_average": "20",
    "mms_kt_average": "25",
    "mms_lg_average": "36"
  }
]
```

## 메시지상태코드

숫자 4자리로 구성된 메시지의 상태를 나타내는 코드입니다. 코드 첫번째 자리 숫자의 의미는 아래와 같습니다.

Message API 호출시에는 앞에 두자리와 뒤 두자리가 구분되어 리턴됩니다.

예) 1010 -> status = '1', result\_code = '10'

| 코드   | 내용                         |
| ---- | -------------------------- |
| 1xxx | 접수(전) 상태 코드                |
| 2xxx | 쿨에스엠에스 게이트웨이 내에서 발송중 상태 코드 |
| 3xxx | 연동망에서 발송 상태 코드             |
| 4xxx | 발송완료 상태 코드                 |

### 코드 목록

| 코드   | 내용                          |
| ---- | --------------------------- |
| 1010 | 필수 입력 값 미입력                 |
| 1013 | 필수 입력 값 미입력(2)              |
| 1020 | 등록된 계정이 아니거나 패스워드가 틀림       |
| 1021 | 해당 메시지가 없음                  |
| 1022 | 해당 그룹이 없음                   |
| 1023 | 해당 이미지가 없음                  |
| 1024 | 서버 오류                       |
| 1025 | 이미지 입력되었으나 타입이 MMS가 아님      |
| 1026 | 중복 수신번호                     |
| 1030 | 잔액 부족                       |
| 1061 | 사용자에 의해 수신거부 됨(080무료수신거부)   |
| 1062 | 발신번호 미등록                    |
| 2000 | 정상 접수                       |
| 2100 | (예약) 대기중                    |
| 2160 | 예약 취소                       |
| 2230 | 잔액 부족                       |
| 2254 | 스팸처리(쿨에스엠에스 게이트웨이)          |
| 3000 | 이통사로 접수 완료(정상)              |
| 3054 | 스팸처리(이통사)                   |
| 3032 | 미가입자                        |
| 3040 | 전송시간 초과                     |
| 3041 | 단말기 busy                    |
| 3042 | 음영지역                        |
| 3043 | 단말기 Power off               |
| 3044 | 단말기 메시지 저장갯수 초과             |
| 3045 | 단말기 일시 서비스 정지               |
| 3046 | 기타 단말기 문제                   |
| 3047 | 착신거절                        |
| 3049 | Format Error                |
| 3050 | SMS서비스 불가 단말기               |
| 3051 | 착신측의 호불가 상태                 |
| 3052 | 이통사 서버 운영자 삭제               |
| 3053 | 서버 메시지 Que Full             |
| 3054 | SPAM                        |
| 3055 | SPAM, nospam.or.kr 에 등록된 번호 |
| 3056 | 전송실패(무선망단)                  |
| 3057 | 전송실패(무선망->단말기단)             |
| 3058 | 전송경로 없음                     |
| 3059 | 변작된 발신번호.                   |
| 4000 | 수신완료                        |
