# SMS API Version 1



## Overview

[REST API 1.0](https://developer.coolsms.co.kr/REST\_API\_Global) 에 비해 달라진 점은 아래와 같습니다.

1. 누리고 푸시 앱 전송을 지원합니다.
2. 1만건 메시지 전송을 2분에서 20초 이하로 단축.
3. 후불제 회원 지원.
4. 알림톡 지원.

이 문서는 쿨에스엠에스의 REST API를 통하여 문자전송에서부터 전송된 문자의 상태값을 비롯하여 잔액정보 및 예약취소 등의 작업을 요청하는 방법을 기술하고 있습니다. REST API를 기반으로 PHP, Java, Python, Delphi, C 등 다양한 언어로 구현된 SDK 및 예제를  [SDK](https://developer.coolsms.co.kr/SDK\_ko) 에서 확인하세요.

모든 Request 호출에는 API Key를 비롯한 인증정보를 포함하여 서버의 인증을 거쳐야 합니다. 인증에 대한 상세한 내용은 [Authentication](https://developer.coolsms.co.kr/REST\_API#Authentication) 을 확인하세요.

인증을 위한 API Key 및 API Secret 코드는 [문자메시지 > 환경설정 > API Key 관리](https://www.coolsms.co.kr/credentials) 메뉴에서 발급 및 관리가 가능합니다. [API Key 관리](https://developer.coolsms.co.kr/Man\_Credentials) 문서를 참고하세요.

아래는 Resource Url과 간단한 설명을 테이블로 정리하였습니다. 상세한 설명을 보시려면 해당 Resource Url을 클릭하여 주세요.

| Resource                                                           | Description   |
| ------------------------------------------------------------------ | ------------- |
| [POST send](https://developer.coolsms.co.kr/SMS\_API#POSTsend)     | 문자전송 요청       |
| [GET sent](https://developer.coolsms.co.kr/SMS\_API#GETsent)       | 발송된 문자정보 읽어오기 |
| [POST cancel](https://developer.coolsms.co.kr/SMS\_API#POSTcancel) | 예약문자 취소       |
| [GET balance](https://developer.coolsms.co.kr/SMS\_API#GETbalance) | 잔액정보 읽어오기     |
| [GET status](https://developer.coolsms.co.kr/SMS\_API#GETstatus)   | 전송채널 상태 조회    |

※ Request Parameters 입력시 JSON 포맷의 데이터가 아니라 폼데이터임을 유의해 주세요. Response Body의 데이터가 JSON 형식입니다.

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
| 1.6     | 카카오톡 알림톡 추가(beta)                                              |

## POST send

문자메시지를 전송 요청합니다. 전송 요청에 대한 Response는 휴대전화까지 전송된 결과가 아닙니다.

### Resource URL

[https://api.coolsms.co.kr/sms/1.5/send](https://api.coolsms.co.kr/sms/1.5/send)

### **Parameters**

| Mandatory | Field           | Description                                                                                                                                                                |
| --------- | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Ο         | 인증정보            | 인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST\_API#Authentication) 참고                                                                                       |
|           | to              | 수신번호 입력 콤마(,)로 구분된 수신번호 입력가능 예) 01012345678,01023456789,01034567890                                                                                                        |
|           | from            | <p>발신번호 예) 0212345678<br>2015/10/16 발신번호 사전등록제에 의해 반드시 등록된 번호만 허용됩니다. (해외문자 제외)</p>                                                                                        |
|           | text            | 문자내용                                                                                                                                                                       |
|           | type            | <p>SMS(90바이트), LMS(장문 2,000바이트), MMS(장문+이미지), ATA(알림톡)<br>입력 없으면 SMS가 기본<br>국가코드가 82가 아니면 SMS로 강제</p>                                                                      |
|           | image           | 지원형식 : 300KB 이하의 JPEG, PNG, GIF 형식의 파일 2048x2048 픽셀이하                                                                                                                      |
|           | image\_encoding | 이미지 인코딩 방식 binary(Default), base64                                                                                                                                         |
|           | refname         | 참조내용(이름)                                                                                                                                                                   |
|           | country         | <p>한국: 82, 일본: 81, 중국: 86, 미국: 1, 기타 등등 (기본 한국)</p><p><a href="http://countrycode.org">http://countrycode.org</a> 참고</p>                                                   |
|           | datetime        | <p>예약시간을 YYYYMMDDHHMISS 포맷으로 입력</p><p>입력 없거나 지난날짜를 입력하면 바로 전송<br>예) 20131216090510 (2013년 12월 16일 9시 5분 10초에 발송되도록 예약)</p><p>( 알림톡, 친구톡은 지원이 안, API v2이상에서 사용 가능합니다. )</p> |
|           | subject         | LMS, MMS 일때 제목 (40바이트)                                                                                                                                                     |
|           | charset         | <p>한글 인코딩 방식 지정 유니코드 UTF-8 일 경우 utf8 완성형 한글(EUC-KR) 일 경우 euckr 으로 입력<br>입력 없으면 utf8가 기본</p>                                                                                |
|           | srk             | 솔루션 제공 수수료를 정산받을 솔루션 등록키                                                                                                                                                   |
|           | mode            | test로 입력할 경우 CARRIER 시뮬레이터로 시뮬레이션됨 수신번호를 반드시 01000000000 으로 테스트하세요. 예약필드 datetime는 무시됨 결과값은 60 잔액에서 실제 차감되며 다음날 새벽에 재충전됨                                                   |
|           | extension       | JSON 포맷의 개별 메시지를 담을 수 있음                                                                                                                                                   |
|           | delay           | 0\~20 사이의 값으로 전송지연 시간을 줄 수 있음, 1은 약 1초 (기본값은 0)                                                                                                                            |
|           | force\_sms      | <p>누리고푸시를 사용하더라도 SMS로 발송되도록 강제</p><p>true 혹은 false(기본)</p>                                                                                                                 |
|           | os\_platform    | <p>클라이언트의 OS 및 플랫폼 버전) CentOS 6.6</p><p>(v1.5에서 추가됨)</p>                                                                                                                   |
|           | dev\_lang       | <p>개발 프로그래밍 언어 예) PHP 5.3.3</p><p>(v1.5에서 추가됨)</p>                                                                                                                         |
|           | sdk\_version    | <p>SDK 버전 예) PHP SDK 1.5</p><p>(v1.5에서 추가됨)</p>                                                                                                                            |
|           | app\_version    | <p>어플리케이션 버전 예) Purplebook 4.1</p><p>(v1.5에서 추가됨)</p>                                                                                                                      |
|           | sender\_key     | 알림톡 Sender Key 입력                                                                                                                                                          |
|           | template\_code  | 알림톡 템플릿 코드 입력                                                                                                                                                              |

Mandatory가 Ο 인 필드는 반드시 입력하여야 합니다.

srk 는 앱아이디를 말하는 것으로 [https://www.coolsms.co.kr/my\_app\_list](https://www.coolsms.co.kr/my\_app\_list) 을 참고하세요.

type, to, from, text, subject 등의 필드값을 개별적으로 다른 값으로 발송하고자 할 때 JSON형식으로 extension 포맷을 사용할 수 있습니다.

한번의 Request에 extension을 포함하여 총 받는사람(to) 수는 1000개 까지가 제한이며 1000개가 넘을 경우 오류를 발생시킵니다. (RecipientsTooMany)

한번의 Request의 총 크기는 2MB를 넘을 수 없습니다. (오류코드 미정)

#### extension 포맷

```
[
	{
		"type": "SMS",
		"to": "01000000000,01011111111,01022222222",
		"text": "Hello A"
	},
	{
		"type": "LMS",
		"to": "01000000000,01011111111,01022222222",
		"subject": "LMS Subject",
		"text": "Hello B"
	},
	{
		"type": "MMS",
		"to": "01000000000,01011111111,01022222222",
		"subject": "MMS Subject",
		"text": "Hello C",
	}
]
```

type, country, to, from, datetime, text, subject, delay 가 올 수 있고 입력하지 않는 필드는 상위(기본 필드) 값을 상속 받아 사용됩니다. 단, to는 상속받지 아니하고 필수 입력 사항입니다.

#### 발송형태에 따른 제한사항

이동통신사 내부적으로 완성형한글로 변환되므로 영어 1바이트, 한글 2바이트로 취급됩니다.

| 구분  | 제한사항                                                                                           |
| --- | ---------------------------------------------------------------------------------------------- |
| SMS | 90바이트 까지 전송가능 (한글 45자)                                                                         |
| LMS | 2,000바이트 까지 전송가능 (한글 1,000자)                                                                   |
| MMS | <p>2,000바이트 텍스트 (한글 1,000자)</p><p>1개의 이미지 전송 (300KB. 2048x2048픽셀 이하인 JPEG, PNG, GIF 형식 파일)</p> |
| ATA | <p>카카오톡 알림톡으로 1,000자까지 발송<br>이미지 첨부 불가</p>                                                     |

### &#x20;

### **Example**

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<?php
$api_key = 'NCS52A57F48C3D32';
$api_secret = '5AC44E03CE8E7212D9D1AD9091FA9966';
$timestamp = time();
$salt = uniqid();
$data = strval($timestamp) . $salt;
$signature = hash_hmac('md5', $data, $api_secret);
?>
<html lang="ko" xml:lang="ko" xmlns="http://www.w3.org/1999/xhtml">
	<head>
    	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
	</head>
	<body>
		<form method="post" action="https://api.coolsms.co.kr/sms/1.5/send" enctype="multipart/form-data">
			API Key: <input type="text" name="api_key" value="<?php echo $api_key ?>" /><br />
			Timestame: <input type="text" name="timestamp" value="<?php echo $timestamp ?>" /><br />
			Salt: <input type="text" name="salt" value="<?php echo $salt ?>" /><br />
			Signature: <input type="text" name="signature" value="<?php echo $signature ?>" /><br />
			To: <input type="text" name="to" value="01000000000" /><br />
			From: <input type="text" name="from" value="01000000000" /><br />
			Subject: <input type="text" name="subject" value="TEST" /><br />
			Text: <textarea name="text">HELLO COOLSMS~!</textarea><br />
			Type: <select name="type"><option value="SMS">SMS</option><option value="LMS">LMS</option><option value="MMS">MMS</option></select><br />
			Image: <input type="file" name="image" /><br />
			<input type="submit" value="Submit" />
		</form>
	</body>
</html>
```

### **Response**

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

result\_code 가 00 이면 정상적인 접수이며 이 외의 코드는 [http://www.coolsms.co.kr/Legacy\_Result\_Codes](http://www.coolsms.co.kr/Legacy\_Result\_Codes) 을 참고하세요. 여기서 리턴되는 Response의 내용은 서버에게 전송을 요청한 것에 대한 정보이지 실제 휴대전화로 전송한 것에 대한 정보가 아닙니다. 예를 들어 요청 건수 중 success\_count가 10개라면 서버의 DB에 안전하게 INSERT된 건이 10개라는 의미이며, 나중 sent 리소스를 통해 조회시 이통사를 통해 실제 전송성공된 건수는 8개이고 올바르지 못한 수신번호로 2개로 실패라는 결과가 나올 수 있습니다.

메시지그룹ID(group\_id)는 Request된 메시지들의대표하는 아이디값으로 메시지상태 및 예약취소할 때 키값으로 사용될 수 있습니다. 10건의 문자메시지를 발송할 경우 그 10건의 문자메시지를 대표하는 group\_id 가 리턴되며 sent 리소스를 통해서 10건에 대한 전송상태를 조회할 수 있습니다.

## GET sent

발송된 문자메시지의 목록을 가져옵니다.&#x20;

### Resource Url

[https://api.coolsms.co.kr/sms/1.5/sent](https://api.coolsms.co.kr/sms/1.5/sent)

### Parameters

| Mandatory | Field             | Description                                                                          |
| --------- | ----------------- | ------------------------------------------------------------------------------------ |
| Ο         | 인증정보              | 인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST\_API#Authentication) 참고 |
|           | count             | 기본값 20이며 20개의 목록을 받을 수 있음. 40입력시 40개의 목록이 리턴                                         |
|           | page              | 1부터 시작하는 페이지값                                                                        |
|           | rcpt              | 수신번호로 검색                                                                             |
|           | start             | 검색 시작일시 접수 날짜와 시간으로 검색 YYYY-MM-DD HH:MI:SS 포맷의 날짜와 시간                                |
|           | end               | 검색 종료일시 접수 날짜와 시간으로 검색 YYYY-MM-DD HH:MI:SS 포맷의 날짜와 시간                                |
|           | status            | 메시지 상태 값으로 검색                                                                        |
|           | resultcode        | 전송결과 값으로 검색                                                                          |
|           | notin\_resultcode | 입력된 전송결과 값 이외의 건들만 조회                                                                |
|           | mid               | 메시지ID                                                                                |
|           | gid               | 그룹ID                                                                                 |

검색 옵션이 없는 경우 가장 최신의 발송건부터 20일 전까지 내림차순으로 페이지 단위의 목록을 리턴합니다.

### Example

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<?php
$api_key = 'NCS52A57F48C3D32';
$api_secret = '5AC44E03CE8E7212D9D1AD9091FA9966';
$timestamp = time();
$salt = uniqid();
$data = strval($timestamp) . $salt;
$signature = hash_hmac('md5', $data, $api_secret);
?>
<html lang="ko" xml:lang="ko" xmlns="http://www.w3.org/1999/xhtml">
	<head>
    	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
	</head>
	<body>
		<form method="get" action="https://api.coolsms.co.kr/sms/1.5/sent" enctype="multipart/form-data">
			API Key: <input type="text" name="api_key" value="<?php echo $api_key ?>" /><br />
			Timestame: <input type="text" name="timestamp" value="<?php echo $timestamp ?>" /><br />
			Salt: <input type="text" name="salt" value="<?php echo $salt ?>" /><br />
			Signature: <input type="text" name="signature" value="<?php echo $signature ?>" /><br />
			List Count : <input type="text" name="count" value="20" /><br />
			Page: <input type="text" name="page" value="1" /><br />
			<input type="submit" value="Submit" />
		</form>
	</body>
</html>
```

### **Response**

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
      "sent_time":"201401071814",
      "text":"Test Message",
      "carrier":"SKT",
      "scheduled_time":""
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
      "scheduled_time":"20160401000000"
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
      "scheduled_time":""
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
      "scheduled_time":""
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

result\_code 는 [http://www.coolsms.co.kr/Legacy\_Result\_Codes](http://www.coolsms.co.kr/Legacy\_Result\_Codes) 페이지를 참고 하세요.

## POST cancel

예약된 문자메시지를 취소합니다. 예약되지 않았거나, 예약되었으나 이미 발송된 문자메시지는 취소 할 수 없습니다.

### **Resource URL**

[https://api.coolsms.co.kr/sms/1.5/cancel](https://api.coolsms.co.kr/sms/1.5/cancel)

### **Parameters**

| Mandatory | Field | Description                                                                          |
| --------- | ----- | ------------------------------------------------------------------------------------ |
| Ο         | 인증정보  | 인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST\_API#Authentication) 참고 |
|           | mid   | 메시지ID                                                                                |
|           | gid   | 그룹ID                                                                                 |

mid 혹은 gid 중 하나는 반드시 입력하세요.

## GET balance

잔액을 확인합니다.

### Resource URL

[https://api.coolsms.co.kr/sms/1.5/balance](https://api.coolsms.co.kr/sms/1.5/balance)

### **Parameters**

| Mandatory | Field | Description                                                                          |
| --------- | ----- | ------------------------------------------------------------------------------------ |
| Ο         | 인증정보  | 인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST\_API#Authentication) 참고 |

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

### Resource Url

[https://api.coolsms.co.kr/sms/1.5/status](https://api.coolsms.co.kr/sms/1.5/status)

### Parameters

| Mandatory | Field   | Description                                                                                                                         |
| --------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Ο         | 인증정보    | 인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST\_API#Authentication) 참고                                                |
|           | count   | 기본값 1이며 1개의 최신의 레코드를 받을 수 있음, 10입력시 10분 동안의 레코드 목록을 리턴                                                                              |
|           | unit    | <p>minute(default), hour, day 중 하나<br>minute : 분 단위의 현황<br>hour : 시간 단위의 평균<br>day : 일 단위의 평균<br>(v1.4에서 추가)</p>                    |
|           | date    | <p>데이터를 읽어오는 기준 시각으로 YYYYMMDDHHMISS 형식의 14자리 값<br>예) 20150331095101 (2015년 3월 31일 오전 9시 51분 1초)<br>기본값 : 현재시각</p><p>(v1.4에서 추가)</p> |
|           | channel | <p>1: 1건 발송 채널 (기본 값)</p><p>2: 대량 발송 채널<br>(v1.4에서 추가)</p>                                                                          |

### Response

모든 항목의 값은 초단위(seconds)값입니다. sms\_average와 mms\_average는 각각 SMS채널과 MMS채널의 문자가 접수된 때부터 실제 수신되기까지 걸린 시간으로 계산된 평균값으로 리포트가 오지않은 대기중인 메시지를 합산한 값이므로 다소 높게 나와도 정상입니다. sk, kt, lg 의 경우 수신시각이 분단위로만 제공되어서 약간의 차이가 날 수 있습니다.

```
[
  {
    'registdate': '2014-02-25 10:34:01',
    'sms_average': '23',
    'sms_sk_average': '9',
    'sms_kt_average': '10',
    'sms_lg_average': '11',
    'mms_average': '52',
    'mms_sk_average': '20',
    'mms_kt_average': '25',
    'mms_lg_average': '36'
  }
]
```

## [메시지 상태 코드](https://support.coolsms.co.kr/hc/ko/articles/115009267167-%EA%B2%B0%EA%B3%BC-%EC%BD%94%EB%93%9C-%EB%B0%8F-%EC%83%81%ED%83%9C-%EC%BD%94%EB%93%9C)

| CODE | 설 명                         |
| ---- | --------------------------- |
| 00   | 정상(전송완료)                    |
| 10   | 잘못된 번호                      |
| 11   | 상위 서비스망 스팸 인식됨              |
| 12   | 상위 서버 오류                    |
| 13   | 잘못된 필드값                     |
| 20   | 등록된 계정이 아니거나 패스워드가 틀림       |
| 21   | 존재하지 않는 메시지 ID              |
| 30   | 가능한 전송 잔량이 없음               |
| 31   | 전송할 수 없음                    |
| 32   | 가입자 없음                      |
| 40   | 전송시간 초과                     |
| 41   | 단말기 busy                    |
| 42   | 음영지역                        |
| 43   | 단말기 Power off               |
| 44   | 단말기 메시지 저장갯수 초과             |
| 45   | 단말기 일시 서비스 정지               |
| 46   | 기타 단말기 문제                   |
| 47   | 착신거절                        |
| 48   | Unkown error                |
| 49   | Format Error                |
| 50   | SMS서비스 불가 단말기               |
| 51   | 착신측의 호불가 상태                 |
| 52   | 이통사 서버 운영자 삭제               |
| 53   | 서버 메시지 Que Full             |
| 54   | SPAM                        |
| 55   | SPAM, nospam.or.kr 에 등록된 번호 |
| 56   | 전송실패(무선망단)                  |
| 57   | 전송실패(무선망->단말기단)             |
| 58   | 전송경로 없음                     |
| 60   | 예약취소                        |
| 70   | 허가되지 않은 IP주소                |
| 81   | 게이트웨이 연결 실패                 |
| 82   | 이미지 미입력                     |
| 83   | 수신번호 미입력                    |
| 84   | 발신번호 미입력                    |
| 85   | 메시지 내용 미입력                  |
| 86   | 미지원 이미지 타입                  |
| 99   | 전송대기                        |
