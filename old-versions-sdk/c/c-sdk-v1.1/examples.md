# Examples



아래 github 에서 예제파일을 확인하세요 [https://github.com/coolsms/rest/tree/master/c](https://github.com/coolsms/rest/tree/master/c)

### SMS 발송

문자메시지 내용을 90바이트\(내부적으로 완성형 한글로 변환되므로 영어 1자는 1바이트, 한글 1자는 2바이트로 취급됩니다\)까지 전송 가능합니다.

#### 간단한 문자

```text
send_opt send_info = send_opt_init();
coolsms_formset(&send_info, COOLSMS_TO, "01000000000");   // 받는 사람 번호
coolsms_formset(&send_info, COOLSMS_FROM, "0100000000");  // 보내는 사람번호
coolsms_formset(&send_info, COOLSMS_TEXT, "안녕하세요.");  // 문자 메시지
result = _send(&user_info, &send_info);
// 결과값은 result_struct 형태로 받습니다. 
coolsms_formfree(&send_info);   // form 값 메모리 해제
printf("Result = %s\n", result.memory);
```

#### 예약발송

```text
send_opt send_info = send_opt_init();
coolsms_formset(&send_info, COOLSMS_TO, "01000000000");   // 받는 사람 번호
coolsms_formset(&send_info, COOLSMS_FROM, "0100000000");  // 보내는 사람번호
coolsms_formset(&send_info, COOLSMS_TEXT, "안녕하세요.");  // 문자 메시지
coolsms_formset(&send_info, COOLSMS_DATETIME, "20140131103000"); 
// 2014년01월31일10시30분00초를 숫자만 붙이시면 됩니다. 20140131103000
result = _send(&user_info, &send_info);
// 결과값은 result_struct 형태로 받습니다. 
coolsms_formfree(&send_info);     //form 값 메모리 해제
printf("Result = %s\n", result.memory);
```

#### 단체문자

```text
send_opt send_info = send_opt_init(); 
coolsms_formset(&send_info, COOLSMS_TO, "01000000000, 01000000001, 010000000002, 01000000003, 01000000004, 01000000005"); // 받는 사람들 번호coolsms_formset(&send_info, COOLSMS_FROM, "0100000000"); // 보내는 사람번호 coolsms_formset(&send_info, COOLSMS_TEXT, "안녕하세요."); // 문자 메시지 result = _send(&user_info, &send_info); 
// 결과값은 result_struct 형태로 받습니다.
coolsms_formfree(&send_info);     //form 값 메모리 해제
printf("Result = %s\n", result.memory);
```

### LMS 발송

문자메시지 내용을 2,000 바이트까지 발송할 수 있습니다. \(내부적으로 완성형 한글로 변환되므로 영어 1자는 1바이트, 한글 1자는 2바이트로 취급됩니다\)

#### 예제

```text
send_opt send_info = send_opt_init(); 
coolsms_formset(&send_info, COOLSMS_TO, "01000000000"); // 받는 사람 번호 
coolsms_formset(&send_info, COOLSMS_FROM, "0100000000"); // 보내는 사람번호
coolsms_formset(&send_info, COOLSMS_TEXT, "잘지내시죠?"); // 문자 메시지 
coolsms_formset(&send_info, COOLSMS_TYPE, "lms");  
//type 은 default 로 sms 로 되있습니다. 
coolsms_formset(&send_info, COOLSMS_SUBJECT, "안녕하세요."); // 문자 제목

result = _send(&user_info, &send_info); 
// 결과값은 result_struct 형태로 받습니다.
coolsms_formfree(&send_info);    // form 값 메모리 해제
printf("Result = %s\n", result.memory);
```

### MMS 발송

문자메시지의 내용을 텍스트 2,000바이트와 이미지 1를 동시 발송 할 수 있습니다. mtype을 mms로 하고 발송할 이미지의 경로를 입력합니다.

#### 예제

```text
send_opt send_info = send_opt_init(); 
coolsms_formset(&send_info, COOLSMS_TO, "01000000000"); // 받는 사람 번호 
coolsms_formset(&send_info, COOLSMS_FROM, "0100000000"); // 보내는 사람번호 
coolsms_formset(&send_info, COOLSMS_TEXT, "잘지내시죠?"); // 문자 메시지 
coolsms_formset(&send_info, COOLSMS_TYPE, "mms"); 
coolsms_formset(&send_info, COOLSMS_IMAGE, "image.jpg"); 
coolsms_formset(&send_info, COOLSMS_SUBJECT, "안녕하세요."); // 문자 제목 

result = _send(&user_info, &send_info); 
// 결과값은 result_struct 형태로 받습니다.
coolsms_formfree(&send_info);     // form 값 메모리 해제
printf("Result : %s\n", result.memory);
```

  option 에 대하여 알고 싶으시면 [API Reference](http://doc.coolsms.co.kr/?page_id=1817)를 참고하시기 바랍니다.  

### 발송결과

#### Response Format

```text
{
  "recipient_number": "01012345678",
  "group_id": "20120217103829612403761364",
  "message_id": "20120217103830163531890062",
  "result_code": "00",
  "result_message": "Success"
}
```

### 문자 전송결과 확인하기 \(SENT\)

```text
response_struct result;
sent_opt sent_info = sent_opt_init();
sent_info.count = "30";   // default 값은 20입니다. 
sent_info.page = "2";
sent_info.s_rcpt = "01022223333"; // 특정 번호의 결과를 알고 싶은경우
sent_info.s_start = "2014-01-01 00:00:00";  //전송결과 검색 범위 시작 날짜
sent_info.s_end = "2014-01-31 00:00:00";    //전송결과 검색 범위 마지막 날짜
result = _sent(&user_info, &sent_info);
printf("Result : %s\n", result.memory);
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

  Result Code 는 [결과코드 해설](http://doc.coolsms.co.kr/?page_id=55)을 참고 하세요.

#### Status Code

| 0 | 대기중 |
| :--- | :--- |
| 1 | 이통사로 전송중 |
| 2 | 이통사로부터 리포트 도착 |

### 잔액 확인하기

```text
response_struct result;
char * api_key = "ENTER_YOUR_OWN";
char * api_secret = "ENTER_YOUR_OWN";
user_opt user_info = user_opt_init(api_key, api_secret);
result = _balance(user_info);
```

### 예약 발송 취소하기

```text
response_struct result;
char * api_key = "ENTER_YOUR_OWN";
char * api_secret = "ENTER_YOUR_OWN";
user_opt user_info = user_opt_init(api_key, api_secret);
cancel_opt cancel_info = cancel_opt_init();
cancel.gid = "ENTER_GID";
cancel.mid = "ENTER_MID"; 
// group id(gid) 나 message id(mid) 둘중에 하나는 입력해야합니다. 
result = _cancel(user_info);
```

###  JSON parsing 하기

REST API C 는 JSON parsing 을 위해 Jansson 을 사용하고 있습니다. 자세한 사용법은 [https://jansson.readthedocs.org/en/2.5/](https://jansson.readthedocs.org/en/2.5/) 을 이용하시기 바랍니다.

```text
#include "coolsms.h"
void print_result(response_struct);
int main()
{
    response_struct result;
    char *api_key = "ENTER_YOUR_OWN";
    char *api_secret = "ENTER_YOUR_OWN";
    user_opt user_info = user_opt_init(api_key, api_secret);
    send_opt send_info = send_opt_init();

    coolsms_formset(&send_info, COOLSMS_TO, "01000000000");
    coolsms_formset(&send_info, COOLSMS_FROM, "01000000000");
    coolsms_formset(&send_info, COOLSMS_TEXT, "msg from c");
    result = _send(&user_info, &send_info);

    print_result(result);
    coolsms_formfree(&send_info);
    return 0;
}

void print_result(response_struct result)
{
	/* parsing json results */
	json_error_t error;
	json_t *root;
	root = json_loads(result.memory, 0, &error);
	if (!root){
		fprintf(stderr, "error : root\n");
		fprintf(stderr, "error : on line %d: %s\n", error.line, error.text);
		exit(1);
	}

	/* print keys and its values */
	json_t *data, *obj, *array;
	const char * key;
	int i;
	json_object_foreach(root, key, obj){
		printf("%s:", key);
		data = json_object_get(root, key);
		if (!json_is_array(data))
			printf("%s\n", json_dumps(data, JSON_ENCODE_ANY));

		json_array_foreach(obj, i, array){
			printf("%s:\n", json_dumps(array, JSON_ENCODE_ANY));
		}
	}

	/* Jansson library is used for parsing JSON data
	   More info found at https://jansson.readthedocs.org/en/2.5/ */
}
```

