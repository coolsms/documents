# API Reference

Python SMS SDK에서는 coolsms 모듈 아래로 rest 클래스 한 개로 구성되어 있습니다.

### coolsms.rest

coolsms 모듈의 rest 클래스를 설명합니다. 아래와 같은 코드로 객체를 생성할 수 있습니다.

```text
import coolsms
cool = coolsms.rest(api_key, api_secret)
cool.send(to,sender,message)
```

수익배분을 받기 위한 솔루션등록키\(srk\) 설정은 srk='K00001234' 처럼 파라메터를 추가해 줍니다.

```text
import coolsms
cool = coolsms.rest(api_key, api_secret, srk='K00001234')
cool.send(to,sender,message)
```

#### set\_type\(mtype\)

문자발송 형태를 설정합니다.

**Parameters:**

* * mtype\(string\) - 대소문자 구별없이 SMS, LMS, MMS 중 하나 입력가능, 기본값은 SMS입니다.

**Return:** None

**발송형태에 따른 제한사항** 내부적으로 완성형한글로 변환되므로 영어 1바이트, 한글 2바이트로 취급됩니다.

| 구분 | 제한사항 |
| :--- | :--- |
| SMS | 90바이트 까지 전송가능 |
| LMS | 2,000바이트 까지 전송가능 |
| MMS | 2,000바이트 텍스트, 1개의 이미지 전송   |

#### set\_image\(image\)

발송할 이미지를 지정한다.

**Parameters:**

* * image\(string\) - MMS에 첨부할 이미지 경로

**Return:** None

#### send\(to=None, text=None, sender=None, mtype=None, subject=None, image=None, datetime=None, extension=None\)

문자를 발송합니다.

**Parameters:**

* * to\(string\) - 수신번호\(받는 사람의 휴대폰 번호\) 입력
  * sender\(string\) - 발신번호\(보내는 사람의 전화번호\) 입력
  * text\(string\) - 문자메시지 내용
  * mtype\(string\) - SMS, LMS, MMS 중 하나 선택 set\_type으로 설정된 값에 영향을 미치지 않습니다. 미입력시 set\_type에 의해 설정된 값으로 발송됩니다.
  * subject\(string\) - LMS, MMS 형식일 때 제목 입력
  * image\(string\) - mtype이 MMS일 때 발송할 이미지의 경로 입력

**Return:**  아래와 같은 구조의 dictionary 형식으로 리턴

```text
{
  'recipient_number': '01012345678',
  'group_id': '20120217103829612403761364',
  'message_id': '20120217103830163531890062',
  'result_code': '00',
  'result_message': 'Success'
}
```

#### status\(\)

발송된 문자를 읽어온다.

**Parameters:**

* * page\(integer\) - 페이지 번호 입력
  * mid\(string\) - 메시지ID 입력
  * gid\(string\) - 그룹ID 입력
  * s\_rcpt\(string\) -  \(검색옵션\) 수신번호로 검색
  * s\_start\(string\) - \(검색옵션\) 발송시각으로 검색, 시작시간 입력
  * s\_end\(string\) - \(검색옵션\) 발송시각으로 검색, 끝시간 입력

 **Return:** 아래와 같은 자료구조로 리턴

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
    },
    {
      'type':'SMS',
      'accepted_time':'2014-01-07 18:11:23',
      'recipient_number':'01000000000',
      'group_id':'G52CBC4C35B3A8',
      'message_id':'M52CBC4C35BA70',
      'status':'2',
      'result_code':'58',
      'result_message':'\uc804\uc1a1\uacbd\ub85c \uc5c6\uc74c',
      'sent_time':'201401071811',
      'text':'message\nhere'
    },
    {
      'type':'SMS',
      'accepted_time':'2014-01-06 12:42:32',
      'recipient_number':'01012345678',
      'group_id':'G52CA262EC447D',
      'message_id':'M52CA262EC49D8',
      'status':'2',
      'result_code':'00',
      'result_message':'\uc815\uc0c1',
      'sent_time':'201401061257',
      'text':'\ud14c\uc2a4\ud305hi there~'
    }
  ]
}
```

#### balance\(\)

잔액정보를 읽어온다.

**Return:**  \( cash, point \) 캐쉬, 포인트를 담은 tuple 형식으로 리턴

**Example:** cash, point = cool.balance\(\)

#### cancel\(\)

예약문자를 취소한다.

 **Return:** True : 성공, False : 실패

