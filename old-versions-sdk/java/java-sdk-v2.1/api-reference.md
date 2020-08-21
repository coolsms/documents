# API Reference



## 문자\(SMS\)

### 문자전송\(SEND\)

**Parameters :**        

* to - 받는사람 번호
* from - 보내는사람 번호
* text - 문자내용
* type - 문자 타입
* app\_version - 어플리케이션 버젼 예\) Purplebook 4.1
* to - 받는사람 번호 여러개 입력시
* image\_path - image file path 이미지 파일 경로 설정 \(기본 "./"\)
* image - image file \(지원형식 : 200KB 이하의 JPEG\)
* refname - 참조내용
* country - 국가코드 한국:KR 일본:JP 미국:US 중국:CN
* datetime - 예약전송시 날짜 설정        
* subject - LMS, MMS 일때 제목        
* charset - 인코딩 방식
* srk - 솔루션 제공 수수료를 정산받을 솔루션 등록키
* mode - test모드 수신번호를 반드시 01000000000 으로 테스트하세요. 예약필드 datetime는 무시됨. 결과값은 60. 잔액에서 실제 차감되며 다음날 새벽에 재충전됨
* extension - 개별문자 보내기        

**Return :** 아래와 같이 JSONObject 형태로 return

```text
{
  'recipient_number': '01012345678',
  'group_id': '20120217103829612403761364',
  'message_id': '20120217103830163531890062',
  'result_code': '00',
  'result_message': 'Success'
}
```

### 전송결과\(SENT\)

**Parameters :**

* mid - message\_id 
* gid - group\_id
* count - count
* page - page
* s\_rcpt - 수신번호
* s\_start - 검색 시작 날짜
* s\_end - 검색 종료 날짜

**Return :** 아래와 같은 구조로 return

```text
{
  'total_count':169,
  'list_count':4,
  'page':1,
  'data':[
    {
      'type':'SMS',
      'accepted_time':'2014-01-07 18:14:54',
      'recipient_number':'01000000000',
      'group_id':'G52CBC596955F0',
      'message_id':'M52CBC59695B31',
      'status':'2',
      'result_code':'58',
      'result_message':'\uc804\uc1a1\uacbd\ub85c \uc5c6\uc74c',
      'sent_time':'201401071814',
      'text':'Test Message'
    },
    {
      'type':'SMS',
      'accepted_time':'2014-01-07 18:14:41',
      'recipient_number':'01000000000',
      'group_id':'G52CBC5897645A',
      'message_id':'M52CBC58976A64',
      'status':'2',
      'result_code':'58',
      'result_message':'\uc804\uc1a1\uacbd\ub85c \uc5c6\uc74c',
      'sent_time':'201401071814',
      'text':'message\nhere'
    }
  ]
}
```

### 잔액확인\(BALANCE\)

**Parameters :**

* 없음

**Return :**  아래와 같이 JSONObject 형태로 return             

```text
{
  'cash': '0',
  'point': '15121',  
}
```

### 예약취소\(CANCEL\)

**Parameters :**

* mid - message\_id
* gid - group\_id

**Return :** Return값이 없습니다.

```text
None
```

## 발신번호\(SENDERID\)

### 등록요청\(REGISTER\)

**Parameters :**        

* site\_user - 사이트 유저 아이디 입력, 미입력시 \_\_private\_\_ 으로 설정됩니다. 예\) admin
* phone - 발신번호 예\) 021234567 

**Return :** 아래와 같이 JSONObject 형태로 return

```text
{
  'handle_key': 'CI283910CCKKI91',
  'ars_number': '01000000000'
}
```

### 등록확인\(VERIFY\)

**Parameters :**        

* handle\_key - register 호출 후 리턴받은 핸들값

**Return :** Return값이 없습니다.

```text
None
```

### 삭제\(DELETE\)

**Parameters :**        

* handle\_key - register 호출 후 리턴받은 핸들값

**Return :** Return값이 없습니다.

```text
None
```

### 리스트보기\(LIST\)

**Parameters :**        

* site\_user - 사이트 유저 아이디 입력, 미입력시 \_\_private\_\_ 으로 설정됩니다. 예\) admin

**Return :** 아래와 같이 JSONObject 형태로 return

```text
{
  "data":
  [
     {
       "regdate":"2015-08-07 12:21:33",
       "phone_number":"01000000001",
       "updatetime":"2015-08-21 18:09:10",
       "idno":"SID55C4FFFDDA2",
       "flag_default":"Y"
     },
     {
       "regdate":"2015-08-21 14:45:01",
       "phone_number":"01000000002",
       "updatetime":"2015-08-21 15:09:43",
       "idno":"SID55SSSD9FAB6",
       "flag_default":"N"
      }
  ,"status":true
}
```

### 기본발신번호설정\(SET\_DEFAULT\)

**Parameters :**        

* site\_user - 사이트 유저 아이디 입력, 미입력시 \_\_private\_\_ 으로 설정됩니다. 예\) admin
* handle\_key - 발신번호 핸들값을 입력

**Return :** Return값이 없습니다.

```text
None
```

### 기본발신번호보기\(GET\_DEFAULT\)

**Parameters :**        

* site\_user - 사이트 유저 아이디 입력, 미입력시 \_\_private\_\_ 으로 설정됩니다. 예\) admin
* phone - 발신번호 예\) 021234567 

**Return :** 아래와 같이 JSONObject 형태로 return

```text
{
  'handle_key': 'CI283910CCKKI91',
  'ars_number': '01000000000'
}
```

