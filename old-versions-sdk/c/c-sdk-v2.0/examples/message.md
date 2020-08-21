# Message



## Message

문자발송 관련 예제 입니다.

### SMS\(단문\) 발송

- 90바이트\( 한글 45자 \) 이내의 내용을 문자 메시지로 보낼 수 있습니다.

```text
#include "coolsms.h"

/* Set 1 to test example */
#if 0
int main()
{
	/* api_key and api_secret can be obtained from http://www.coolsms.co.kr */
	response_struct result;
	char *api_key = "API_KEY";
	char *api_secret = "API_SECRET";
	user_opt user_info = user_opt_init(api_key, api_secret);
	send_opt send_info = send_opt_init();
	
	send_info.to = "01000000000";
	send_info.from = "01000000000";
	send_info.text = "SMS 문자 테스트입니다.";
	// send_info.type = "SMS";

	result = send_message(&user_info, &send_info);
	print_result(result);

	return 0;
}
#endif
```

### LMS\(장문\) 발송

- 2000바이트\( 한글 1000자 \) 이내의 내용을 문자 메시지로 보낼 수 있습니다.

- send\_info.type 을 'LMS'로 바꿔주시면 됩니다.

```text
#include "coolsms.h"

/* Set 1 to test example */
#if 0
int main()
{
	/* api_key and api_secret can be obtained from http://www.coolsms.co.kr */
	response_struct result;
	char *api_key = "API_KEY";
	char *api_secret = "API_SECRET";
	user_opt user_info = user_opt_init(api_key, api_secret);
	send_opt send_info = send_opt_init();
	
	send_info.to = "01000000000";
	send_info.from = "01000000000";
	send_info.text = "LMS 문자 테스트입니다.";
	send_info.type = "LMS";
	send_info.subject = "LMS Test";

	result = send_message(&user_info, &send_info);
	print_result(result);

	return 0;
}
#endif
```

### MMS\(포토문자\) 발송

- 이미지\( 300KB미만의 2024\*2024이하 JPG, GIF, PNG \) 를 포함한 내용을 문자 메시지로 보낼 수 있습니다.

- send\_info.type 을 'MMS'로 바꿔주세요.

- send\_info.image 에 해당 경로와 함께 이미지 파일명을 넣어주세요. 예\) './images/test.jpg'

```text
#include "coolsms.h"

/* Set 1 to test example */
#if 0
int main()
{
	/* api_key and api_secret can be obtained from http://www.coolsms.co.kr */
	response_struct result;
	char *api_key = "API_KEY";
	char *api_secret = "API_SECRET";
	user_opt user_info = user_opt_init(api_key, api_secret);
	send_opt send_info = send_opt_init();
	
	send_info.to = "01000000000";
	send_info.from = "01000000000";
	send_info.text = "MMS 문자 테스트입니다.";
	send_info.type = "MMS";
	send_info.image = "images/image.jpg";

	result = send_message(&user_info, &send_info);
	print_result(result);

	return 0;
}
#endif
```

### 예약문자 발송

- 예약해둔 날짜에 문자 메시지를 보낼 수 있습니다.

- send\_info.datetime 에 날짜를 넣어주세요. 예\) '20160221150000' // 2016년 2월 21일 15시 00분 00초

```text
#include "coolsms.h"

/* Set 1 to test example */
#if 0
int main()
{
	/* api_key and api_secret can be obtained from http://www.coolsms.co.kr */
	response_struct result;
	char *api_key = "API_KEY";
	char *api_secret = "API_SECRET";
	user_opt user_info = user_opt_init(api_key, api_secret);
	send_opt send_info = send_opt_init();
	
	send_info.to = "01000000000";
	send_info.from = "01000000000";
	send_info.text = "예약 문자 테스트입니다.";
	send_info.type = "SMS";
	send_info.datetime = "20160605031200";

	result = send_message(&user_info, &send_info);
	print_result(result);

	return 0;
}
#endif
```

### 알림톡 발송

- Sender Key와 Template Code는 필수입니다. 옆에 링크 페이지에 가셔서 발급받아주세요. [발급받기](http://www.coolsms.co.kr/AboutAlimTalk)

- send\_info.type을 ATA로 해주세요.

- send\_info.sender\_key, send\_info.template\_code에 발급받으신 Sender Key와 Template Code를 넣어주세요.

- send\_info.text에는 해당 Template Code와 같은 형태의 내용만 입력 가능하며 \#{홍길동}과 같이 \#{}로 둘러 쌓여있는 부분은 다른 내용으로 변환이 가능합니다.

```text
#include "coolsms.h"

/* Set 1 to test example */
#if 0
int main()
{
	/* api_key and api_secret can be obtained from http://www.coolsms.co.kr */
	response_struct result;
	char *api_key = "API_KEY";
	char *api_secret = "API_SECRET";
	user_opt user_info = user_opt_init(api_key, api_secret);
	send_opt send_info = send_opt_init();
	
	send_info.to = "01000000000";
	send_info.from = "01000000000";
	send_info.text = "알림톡 문자 테스트입니다.";
	send_info.type = "ATA";
	send_info.sender_key = "SENDER_KEY";
	send_info.template_code = "TEMPLATE_CODE";

	result = send_message(&user_info, &send_info);
	print_result(result);

	return 0;
}
#endif 
```

### 예약문자 취소

- 아직 발송되지 않은 예약문자를 취소 할 수 있습니다.

- cancel\_info.mid 또는 cancel\_info.gid 에 해당 문자의 mid나 gid를 넣어주시면 됩니다.

```text
#include "coolsms.h"

/* Set 1 to test example */
#if 0
int main()
{
	/* api_key and api_secret can be obtained from http://www.coolsms.co.kr */
	response_struct result;
	char *api_key = "API_KEY";
	char *api_secret = "API_SECRET";
	user_opt user_info = user_opt_init(api_key, api_secret);
	cancel_opt cancel_info = cancel_opt_init();

	/* set send infomations
	More info found at http://doc.coolsms.co.kr?page_id=1811 */
	// cancel_info.gid = "GID24HL31K4H234";
	cancel_info.mid = "MID52CA262EC49D8";

	result = cancel(&user_info, &cancel_info);
	print_result(result);

	return 0;
}
#endif
```

### 잔액정보 확인

- Coolsms 잔액정보를 확인 할 수 있습니다.

```text
#include "coolsms.h"

/* Set 1 to test example */
#if 0
int main()
{
	/* api_key and api_secret can be obtained from http://www.coolsms.co.kr */
	response_struct result;
	char *api_key = "API_KEY";
	char *api_secret = "API_SECRET";
	user_opt user_info = user_opt_init(api_key, api_secret);

	result = balance(&user_info);
	print_result(result);

	return 0;
}
#endif
```

### 메시지내역 보기

- 발송 한 메시지 내역을 확인 할 수 있습니다.

- 관련 Parameter 들은 [Reference gruide](http://www.coolsms.co.kr/PHP_SDK_EXAMPLE_ReferenceGuide)를 참고 해주세요.

```text
#include "coolsms.h"

/* Set 1 to test example */
#if 0
int main()
{
	/* api_key and api_secret can be obtained from http://www.coolsms.co.kr */
	response_struct result;
	char *api_key = "API_KEY";
	char *api_secret = "API_SECRET";
	user_opt user_info = user_opt_init(api_key, api_secret);
	sent_opt sent_info = sent_opt_init();

	sent_info.offset = "0";                         // 가져올 목록의 시작 위치
	sent_info.limit = "10";                         // 기본값 20, 20개의 목록을 받을 수 있으며 40 입력시 40개의 목록이 리턴
	// sent_info.rcpt = "01000000000";              // 수신번호로 검색
	// sent_info.start = "201603121020";            // 검색 시작일시
	// sent_info.end = "201603121159";              // 검색 종료일시
	// sent_info.status = "00";                     // 메세지 상태 값
	// sent_info.resultcode = "54";                 // 전송결과 값
	// sent_info.notin_resultcode = "00";           // 입력된 전송결과 값 이외의 건
	// sent_info.messate_id = "MID52CA262EC49D8";   // 메세지 ID 값
	// sent_info.group_id = "GID24HL31K4H234";      // 그룹 ID 값

	result = sent(&user_info, &sent_info);
	print_result(result);

	return 0;
}
#endif
```

