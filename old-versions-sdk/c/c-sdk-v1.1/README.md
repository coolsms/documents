# C SDK v1.1



1. 회원가입
2. API Key 생성
3. SDK 다운로드
4. 예제 실행

### 회원가입

[쿨에스엠에스 www.coolsms.co.kr](https://www.coolsms.co.kr/signup) 에서 회원가입 합니다. 회원가입시 300원을 무료 충전하여 드립니다.

### API Key 생성

[API Key 관리 페이지](https://www.coolsms.co.kr/credentials)에서 API Key를 생성합니다. 자동으로 생성된 API Key, API Secret 을 예제 실행할 때 사용합니다. API Secret은 외부에 노출되지 않도록 주의하세요.

### SDK 다운로드

아래 링크 github에서 다운로드 받으세요. \([https://github.com/coolsms/rest/tree/master/c](https://github.com/coolsms/rest/tree/master/c)\)  

### 예제 실행

예제 파일을 아래 링크의 github 저장소에서 다운로드 받으세요. [https://github.com/coolsms/rest/tree/master/C/ ](https://github.com/coolsms/rest/tree/master/c/)위에서 발급받은 API Key, API Secret을 아래의 코드에서 수정하고, to, sender, message 내용도 수정하여 실행해 보세요.  

```text
#include "coolsms.h"

int main()
{
   response_struct result;
   char *api_key = "API_KEY";
   char *api_secret = "API_SECRET";
   user_opt user_info = user_opt_init(api_key, api_secret);
```

  더 많은 예제를 원하신다면 [Examples](https://developer.coolsms.co.kr/SDK_C_Examples_ko) 에서 확인하세요.  

