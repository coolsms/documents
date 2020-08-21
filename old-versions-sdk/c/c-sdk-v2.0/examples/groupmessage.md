# GroupMessage



## GroupMessage

SMS API v2 에서 새롭게 추가된 그룹메시지 관련 예제 입니다.

### 그룹 생성

- 메시지를 담아둘 그룹을 생성 합니다.

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
	new_group_opt new_group_info = new_group_opt_init();

	new_group_info.charset = "utf8 ";
	new_group_info.srk = "";
	// new_group_info.mode = "test";
	// new_group_info.delay = 10;
	// new_group_info.force_sms = true;
	// new_group_info.app_version = "";

	result = create_group(&user_info, &new_group_info);
	print_result(result);

	return 0;
}
#endif
```

### 그룹 리스트 보기

- 생성된 그룹 리스트를 보여줍니다.

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

	result = get_group_list(&user_info);
	print_result(result);

	return 0;
}
#endif
```

### 그룹 삭제

- 해당 그룹을 삭제 합니다.

- 주의! 그룹 안의 메시지들이 전부 삭제 됩니다.

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
	delete_groups_opt delete_groups_info = delete_groups_opt_init();

	delete_groups_info.group_ids = "GID573D2C9C8A4CE, GID573D2CB85E4F9";

	result = delete_groups(&user_info, &delete_groups_info);
	print_result(result);

	return 0;
}
#endif
```

### 그룹 정보 보기

- 해당 그룹의 정보를 보여줍니다.

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
	group_info_opt group_info_info = group_info_opt_init();

	group_info_info.group_id = "GID573D2C9C8A4CE";

	result = get_group_info(&user_info, &group_info_info);
	print_result(result);

	return 0;
}
#endif
```

### 메시지 넣기

- 해당 그룹 안에 메시지를 넣을 수 있습니다.

- 그룹 안에 메시지를 넣을 뿐, 실제로 메시지를 발송 하는 건 아닙니다.

- \(알림톡 사용시\) Sender Key와 Template Code는 필수입니다. 옆에 링크 페이지에 가셔서 발급받아주세요. [발급받기](http://www.coolsms.co.kr/AboutAlimTalk)

- \(알림톡 사용시\) add\_messages\_info.type을 ATA로 해주세요.

- \(알림톡 사용시\) add\_messages\_info.sender\_key, add\_messages\_info.template\_code에 발급받으신 Sender Key와 Template Code를 넣어주세요.

- \(알림톡 사용시\) add\_messages\_info.text에는 해당 Template Code와 같은 형태의 내용만 입력 가능하며 \#{홍길동}과 같이 \#{}로 둘러 쌓여있는 부분은 다른 내용으로 변환이 가능합니다.

```text
#include "coolsms.h"

/* Set 1 to test example */
#if 0
int main()
{
	/* api_key and api_secret can be obtained from http://www.coolsms.co.kr */
	response_struct result;
	char *api_key = "NCS55F7C0B9269DB";
	char *api_secret = "D2ED4C0E5C55D59F33E74484E89F232B";
	user_opt user_info = user_opt_init(api_key, api_secret);
	add_messages_opt add_messages_info = add_messages_opt_init();

	add_messages_info.group_id = "GID573D2CD5BDFED";
	add_messages_info.to = "01000000000";
	add_messages_info.from = "01000000000";
	add_messages_info.text = "CoolSMS Message Test!";
	// add_messages_info.subject = "";
	add_messages_info.type = "SMS";
	// add_messages_info.image_id = "IMG234LSFN234OQ";
	// add_messages_info.refname = "";
	// add_messages_info.country_code = "82";

	result = add_messages(&user_info, &add_messages_info);
	print_result(result);

	return 0;
}
#endif
```

### 메시지 넣기\( JSON 형식 \)

- JSON 형식으로 된 메시지 리스트를 받아서 해당 그룹 안에 메시지를 넣을 수 있습니다.

- 아래 예제와 같이 텍스트값 등 다양하게 정렬된 메시지를 서버에 JSON 형식으로 보내줍니다.

- 그룹안에 메시지를 넣을 뿐, 실제로 메시지를 발송 하는 것은 아닙니다.

- add\_messages\_json\_info.messages에 원하는 만큼 Object를 넣을 수 있습니다.

- \(알림톡 사용시\) Sender Key와 Template Code는 필수입니다. 옆에 링크 페이지에 가셔서 발급받아주세요. [발급받기](http://www.coolsms.co.kr/AboutAlimTalk)

- \(알림톡 사용시\) add\_messages\_json\_info.messages의 type을 ATA로 해주세요.

- \(알림톡 사용시\) add\_messages\_json\_info.messages의 sender\_key, add\_messages\_json\_info.messages의 template\_code에 발급받으신 Sender Key와 Template Code를 넣어주세요.

- \(알림톡 사용시\) add\_messages\_json\_info.messages의 text에는 해당 Template Code와 같은 형태의 내용만 입력 가능하며 \#{홍길동}과 같이 \#{}로 둘러 쌓여있는 부분은 다른 내용으로 변환이 가능합니다

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
	add_messages_json_opt add_messages_json_info = add_messages_json_opt_init();
	
	add_messages_json_info.group_id = "GID5730430CBE318";
	add_messages_json_info.messages = "[{'type': 'SMS', 'to' : '01000000000,01011111111,01022222222',
            'from' : '01000000000',	'text' : 'Hello A'}, {'type': 'LMS', 'to' : '01033333333', 'from' : 
            '01000000000', 'text' : 'Hello B', 'subject' : 'LMS Subject'}, {'type': 'MMS', 'to' : '01044444444,
             01055555555', 'from' : '01000000000', 'text' : 'Hello C', 'subject' : 'MMS Subject', 'image_id' : 
            'IMG234LSFN234OQ'}]";

	result = add_messages_json(&user_info, &add_messages_json_info);
	print_result(result);

	return 0;
}
#endif
```

### 메시지 리스트 보기

- 메시지 리스트를 확인 할 수 있습니다.

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
	message_list_opt message_list_info = message_list_opt_init();

	message_list_info.group_id = "GID573D2CD5BDFED";
	message_list_info.offset = "0";
	message_list_info.limit = "20";

	result = get_message_list(&user_info, &message_list_info);
	print_result(result);

	return 0;
}
#endif
```

### 메시지 삭제

- 해당 메시지를 삭제합니다.

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
	delete_messages_opt delete_messages_info = delete_messages_opt_init();

	delete_messages_info.group_id = "GID573D2CD5BDFED";
	delete_messages_info.message_ids = "MID573D35A4BB4F4, MID573D35A4BB4A2";

	result = delete_messages(&user_info, &delete_messages_info);
	print_result(result);

	return 0;
}
#endif
```

### 메시지 전송

- 해당 그룹 안의 메시지를 전송합니다.

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
	send_group_opt send_group_info = send_group_opt_init();

	send_group_info.group_id = "GID573D2CD5BDFED";

	result = send_group(&user_info, &send_group_info);
	print_result(result);

	return 0;
}
#endif
```

