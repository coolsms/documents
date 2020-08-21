# Examples



아래 github 에서 예제파일을 확인하세요.

[https://github.com/coolsms/php-sdk/tree/master/examples](https://github.com/coolsms/php-sdk/tree/1.2.1/examples)

### SMS 발송

문자메시지 내용을 90바이트\(내부적으로 완성형 한글로 변환되므로 영어 1자는 1바이트, 한글 1자는 2바이트로 취급됩니다\)까지 전송 가능합니다.

#### 간단한 문자

```text
$options->to = "01012341234"; // 받는사람번호
$options->from = "029302266"; // 이미 발신번호 등록을 통해 029302266 이 등록돼 있는 경우
$options->text = "안녕하세요. 좋은아침."; // 문자내용

// send messages
$response = $rest->send($options); 

// get result 
$result = $response->getResult(); // 전송 후 결과 받기
print_r($result); //결과 출력

```

\* 웹에서 발신번호 등록하러가기 [바로가기](https://www.coolsms.co.kr/senderids)

\(coolsms.co.kr 메뉴에서 문자보내기 -&gt; 환경설정 -&gt; 발신번호 설정 탭\)

#### 예약발송

```text
$options->to = "받을사람번호";
$options->from = "보내는사람번호";
$options->text = "새해복 많이 받으세요";
$options->datetime = "20140131103000"; // YYYYMMDDHHMISS

// send messages
$response = $rest->send($options);

// get result 
$result = $response->getResult(); // 전송 후 결과 받기 
print_r($result); 
```

#### 단체문자

```text
$options->to ="01012341234, 01023012301, 01012334124, 01012123434";
//여러명의 번호를 콤마로 구분해서 넣으면 됩니다. 
$options->from = "01022223333";
$options->text = "<00휴대폰>2014년 3월2일에 40%세일이벤트가 있습니다.";
$options->datetime = "20140131103000"; // YYYYMMDDHHMISS

// send messages 
$response = $rest->send($options); 

// get result  
$result = $response->getResult(); // 전송 후 결과 받기 
print_r($result); //결과 출력
```

### LMS 발송

문자메시지 내용을 2,000 바이트까지 발송할 수 있습니다. \(내부적으로 완성형 한글로 변환되므로 영어 1자는 1바이트, 한글 1자는 2바이트로 취급됩니다\)

#### 예제

```text
$options->to = "받을사람번호";
$options->from = "보내는사람번호";
$options->type = "LMS";
// type 은 default 가 sms 로 되있으므로 lms 로 바꾸어 주어야 장문으로 보내집니다.
$options->subject = "문자 제목";
$options->text = "안녕하세요 000입니다.";
// LMS(장문), MMS(사진문자)는 제목을 넣으실수 있습니다.

// send messages
$response = $rest->send($options);

// get result 
$result = $response->getResult(); // 전송 후 결과 받기 
print_r($result); 
```

### MMS 발송

문자메시지의 내용을 텍스트 2,000바이트와 이미지 1를 동시 발송 할 수 있습니다. mtype을 mms로 하고 발송할 이미지의 경로를 입력합니다.

#### 예제

```text
$options->to = "받을사람번호";
$options->from = "보내는사람번호";
$options->type = "MMS";
// type 은 default 가 sms 로 되있으므로 mms 로 바꾸어 주어야 사진이 보내집니다.
$options->image = "myPic.jpg";
// 사진은 jpeg, png, gif 가능합니다. 
$options->subject = "문자 제목";
$options->text = "안녕하세요 제 사진입니다.";
// LMS(장문), MMS(사진문자)는 제목을 넣으실수 있습니다.

// send messages
$response = $rest->send($options);

// get result 
$result = $response->getResult(); // 전송 후 결과 받기 
print_r($result); 
```

  $options 에 다양한 옵션을 주고 싶으시면 [Post Send 페이지](https://developer.coolsms.co.kr/SMS_API#POSTsend)를 참고하시기 바랍니다.  

### ATA 발송

알림톡 발송 예제입니다.

#### 예제

```text
$options->to = "받을사람번호";
$options->from = "보내는사람번호";
$options->type = "ATA";
$options->sender_key = "#ENTER_YOUR_SENDER_KEY#";
$options->text = "안녕하세요 제 사진입니다.";

// send messages
$response = $rest->send($options);

// get result 
$result = $response->getResult(); // 전송 후 결과 받기 
print_r($result); 
```

  $options 에 다양한 옵션을 주고 싶으시면 [Post Send 페이지](https://developer.coolsms.co.kr/SMS_API#POSTsend)를 참고하시기 바랍니다.

### 발송결과

#### Response Format

```text
{
  "recipient_number": "01012345678",
  "group_id": "20120217103829612403761364",
  "result_code": "00",
  "result_message": "Success"
}
```

### 문자 전송결과 확인하기 \(SENT\)

```text
$options->mid = 'VAXZxcasd1a'; // Message ID
$options->gid = 'AVCXZ124ASD'; // Group ID
$options->count = '10'; // default 는 20개로 되있습니다.
$options->page = '3'; // 전체 전송결과 갯수 count 로 나온 페이지 중에 자신이 확인하고 싶은 페이지 선택 
$options->s_rcpt = '01000000000'; // 발송번호 검색
$options->s_start = '2014-01-01 00:00:00'; // 검색 시작일
$options->s_end = '2014-12-31 24:59:59'; // 검색 끝나는일

$response = $rest->sent($options);

$result = $response->getResult();
print_r($result);
```

#### Response Format

```text
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
      "text":"Test Message"
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
      "text":"message\nhere"
    }
  ]
}
```

  Result Code 는 [결과코드 해설](https://developer.coolsms.co.kr/SMS_API#%EB%A9%94%EC%8B%9C%EC%A7%80%EC%83%81%ED%83%9C%EC%BD%94%EB%93%9C)을 참고 하세요.

#### Status Code

| 0 | 대기중 |
| :--- | :--- |
| 1 | 이통사로 전송중 |
| 2 | 이통사로부터 리포트 도착 |

### 잔액 확인하기

```text
$response = $rest->balance();

// get result
$result = $response->getResult();
print_r($result);
```

### 예약 발송 취소하기

```text
$options->mid = 'ASDFZCVASD';
// $options->gid = 'zxcvas2asdvc';
// mid 나 gid 둘중에 하나만 넣으시면 됩니다.
$rest->cancel($options);
// cancel 은 결과값이 없습니다.
```

### 에러 핸들링

- 아래와 같이 해주시면 됩니다. \( send, sent, balance, cancel 모두 동일 \)

```text
$response = $rest->balance();

// check error & print error message
if($response->getError()) print_r($response->getError()); // Error가 발생 할 경우 check
```

