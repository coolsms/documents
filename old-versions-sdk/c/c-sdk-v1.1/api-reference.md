# API Reference



### coolsms.c

먼저 User\_opt struct 을 생성합니다. 생성한 구조체를 initialize 하는 user\_opt\_init\(\) 함수를 불러줍니다.

```text
#include "coolsms.h"
int main()
{
   char * api_key = "키 입력";
   char * api_secret = "비밀키 입력";
   user_opt user_info = user_opt_init(api_key, api_secret);
```

### \_send

```text
response_struct _send (const user_opt *user_info, const send_opt *send_info)
```

send 메서드는 문자메시지를 보내는 함수로서 user\_opt 포인터와 send\_opt 포인터를 parameter 로 받고 response\_struct 의 값을 리턴합니다.

**send\_opt send\_info 설정하기**

send option 을 설정할때는 coolsms\_formset 함수가 사용됩니다.

```text
send_opt send_info = send_opt_init();
coolsms_formset(&send_info, COOLSMS_TO, "01000000000");
coolsms_formset(&send_info, COOLSMS_FROM, "01000000000");
coolsms_formset(&send_info, COOLSMS_TEXT, "msg from c");
result = _send(&user_info, &send_info);
coolsms_formfree(&send_info);
```

options :

* COOLSMS\_TO                                 받는사람
* COOLSMS\_FROM                          보내는 사람
* COOLSMS\_TEXT                            문자 메시지
* COOLSMS\_TYPE                             문자 타입 \(SMS, LMS, MMS\)
* COOLSMS\_IMAGE                          사진 \(\* 사진 추가시 타입은 MMS 로만 해야함\)
* COOLSMS\_REFNAME                   문자를 기억하기 쉽게 표시하는 이름\(  ex. 광고문자\)
* COOLSMS\_DATETIME                  예약발송 설정시 입력 \(format : YYYYMMDDHHMISS\)
* COOLSMS\_SUBJECT                    문자제목\(LMS 와 MMS 만 해당\)
* COOLSMS\_SRK                               SRK 키 설정\([수익 배분프로그램 참고\)](http://www.coolsms.co.kr/sp)
* COOLSMS\_EXTENSION               확장 문자\([사용법](http://doc.coolsms.co.kr/?page_id=1104)\)

문자를 보낸후에는 coolsms\_formfree\(\) 함수를 호출하여 send\_opt 에 할당된 메모리를 해제 시켜줍니다.

```text
void coolsms_formfree(send_opt *send_info)
```

### \_sent

```text
response_struct _sent(const user_opt *user_info, const sent_opt *send_info)
```

발송 되었던 문자에 대한 정보를 가져옵니다. sent\_opt sent\_info 를 설정합니다.

```text
typedef struct {      
char * count, *page, *s_rcpt, *s_start, *s_end, *mid, *gid;  }send_opt;
```

####  

### \_balance

```text
response_struct _balance(const user_opt *user_info)
```

자신의 계정의 남은 잔액과 포인트를 가져옵니다. 설정된 user\_opt 포인터를 parameter 로 넣으면 서버에서 잔액정보를 가지고옵니다.

### \_cancel

```text
response_struct _cancel(const user_opt *user_info, const cancel_opt *cancel_info)
```

예약문자를 취소한다.

```text
typedef struct { char * mid, *gid; }cancel_opt;
```

