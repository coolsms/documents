# Python SDK v1.1

## 시작하기

Python SDK를 통해 문자메시지를 발송하기 위해서 우선적으로 [www.coolsms.co.kr](https://www.coolsms.co.kr/signup) 에 회원가입해야 합니다.

2015년 10월 16일부터는 관련 법\(발신번호 사전등록제\)으로 인해 발신번호로 미리 등록 후 사용해야 합니다.

[발신번호 설정](https://www.coolsms.co.kr/senderids) 에서 발신번호를 미리 등록해 두세요.

## API Key 생성

[API Key 관리 페이지](https://www.coolsms.co.kr/credentials)에서 API Key를 생성합니다. 자동으로 생성된 API Key, API Secret 을 예제 실행할 때 사용합니다. API Secret은 외부에 노출되지 않도록 주의하세요.

![credentials.jpg](http://developer.coolsms.co.kr/files/attach/images/563538/550/563/c6b4e7b3905a527593275a92ca5023d2.jpg)

## SDK 다운로드

안정된 버전을 쿨에스엠에스 다운로드 페이지 [http://developer.coolsms.co.kr/545387](https://developer.coolsms.co.kr/download/545387) 에서 다운로드 받으실 수 있습니다. 또한, 아래 링크 github에서도 최신의 소스코드를 받으실 수 있습니다. [https://github.com/coolsms/python-sdk](https://github.com/coolsms/python-sdk)  

## 예제 실행

위에서 발급받은 API Key, API Secret을 아래의 코드에서 수정하고, to, sender, message 내용도 수정하여 실행해 보세요.

```text
# -*- coding: utf8 -*-
"""
 Copyright (C) 2008-2014 NURIGO
 http://www.coolsms.co.kr
"""
import sys
sys.path.append("..")
import coolsms

def main():
	api_key = 'NCS52A57F48C3D32'
	api_secret = '5AC44E03CE8E7212D9D1AD9091FA9966'
	to = '01000000000'
	sender = '01012345678'
	message = '테스트 메시지'
	cool = coolsms.rest(api_key, api_secret)
	status = cool.send(to,message,sender)
	print status

if __name__ == "__main__":
	main()
	sys.exit(0)
```

## 다음 단계

더 많은 예제를 원하신다면 [Examples](https://developer.coolsms.co.kr/SDK_Python_Examples_ko) 에서 확인하세요. 예제 파일 소스코드를 [github 저장소](https://github.com/coolsms/python-sdk/tree/master/examples)에서도 확인하실 수 있습니다.

