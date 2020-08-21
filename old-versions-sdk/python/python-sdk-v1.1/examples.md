# Examples



[github 저장소에서 최신의 예제 소스코드를 확인](https://github.com/coolsms/python-sdk/tree/master/examples)하실 수 있습니다.  

### SMS 발송

문자메시지 내용을 90바이트\(내부적으로 완성형 한글로 변환되므로 영어 1자는 1바이트, 한글 1자는 2바이트로 취급됩니다\)까지 전송 가능합니다.

2015년 10월 16일부터는 관련 법\(발신번호 사전등록제\)으로 인해 발신번호로 미리 등록 후 사용해야 합니다.  
[발신번호 설정](http://www.coolsms.co.kr/index.php?mid=service_setup&act=dispSmsconfigSenderNumbers) 에서 발신번호를 미리 등록해 두세요.

#### 1건 발송

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

#### 2건 발송

같은 내용의 메시지를 2건 이상 발송할 때 to 파라메터에 콤마\(,\)로 구분된 수신번호 목록을 입력합니다. 최대 1000건 입력 가능합니다.

2015년 10월 16일부터는 관련 법\(발신번호 사전등록제\)으로 인해 발신번호로 미리 등록 후 사용해야 합니다.  
[발신번호 설정](http://www.coolsms.co.kr/index.php?mid=service_setup&act=dispSmsconfigSenderNumbers) 에서 발신번호를 미리 등록해 두세요.

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
	to = '01000000000,01011111111' # <--- input comma-separated numbers
	sender = '01012345678'
	message = '테스트 메시지'
	cool = coolsms.rest(api_key, api_secret)
	status = cool.send(to,message,sender)
	print status

if __name__ == "__main__":
	main()
	sys.exit(0)
```

### LMS 발송

문자메시지 내용을 2,000 바이트까지 발송할 수 있습니다.  \(내부적으로 완성형 한글로 변환되므로 영어 1자는 1바이트, 한글 1자는 2바이트로 취급됩니다\)

2015년 10월 16일부터는 관련 법\(발신번호 사전등록제\)으로 인해 발신번호로 미리 등록 후 사용해야 합니다.  
[발신번호 설정](http://www.coolsms.co.kr/index.php?mid=service_setup&act=dispSmsconfigSenderNumbers) 에서 발신번호를 미리 등록해 두세요.

```text
# -*- coding: utf8 -*-
"""
 Copyright (C) 2008-2014 NURIGO
 http://www.coolsms.co.kr
"""
import sys,coolsms

def main():
	api_key = 'NCS52A57F48C3D32'
	api_secret = '5AC44E03CE8E7212D9D1AD9091FA9966'
	to = '01000000000'
	sender = '01012345678'
	message = 'LMS 2,000 바이트까지 입력가능합니다'
	cool = coolsms.rest(api_key, api_secret)
	status = cool.send(to,message,sender,mtype='lms',subject='LMS 제목(40바이트)')
	if status == False:
			print cool.get_error()
	print status

if __name__ == "__main__":
	main()
	sys.exit(0)
```

### MMS 발송

문자메시지의 내용을 텍스트 2,000바이트와 이미지 1를 동시 발송 할 수 있습니다. mtype을 mms로 하고 발송할 이미지의 경로를 입력합니다.

2015년 10월 16일부터는 관련 법\(발신번호 사전등록제\)으로 인해 발신번호로 미리 등록 후 사용해야 합니다.  
[발신번호 설정](http://www.coolsms.co.kr/index.php?mid=service_setup&act=dispSmsconfigSenderNumbers) 에서 발신번호를 미리 등록해 두세요.

```text
# -*- coding: utf8 -*-
"""
 Copyright (C) 2008-2014 NURIGO
 http://www.coolsms.co.kr
"""
import sys,coolsms

def main():
	api_key = 'NCS52A57F48C3D32'
	api_secret = '5AC44E03CE8E7212D9D1AD9091FA9966'
	to = '01000000000'
	sender = '01012345678'
	message = 'MMS 2,000 바이트까지 입력가능합니다'
	cool = coolsms.rest(api_key, api_secret)
	status = cool.send(to,message,sender,mtype='mms',subject='MMS 제목(40바이트)',image='test.jpg')
	if status == False:
			print cool.get_error()
	print status

if __name__ == "__main__":
	main()
	sys.exit(0)
```

### 예약 발송

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
	status = cool.send(to,message,sender,datetime='20140113140000')
	print status

if __name__ == "__main__":
	main()
	sys.exit(0)
```

### 예약 취소

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
	status = cool.cancel(mid='R1M52D35EAF44960')
	print status

if __name__ == "__main__":
	main()
	sys.exit(0)
```

### 발송내역 조회

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
	cool = coolsms.rest(api_key, api_secret)
	status = cool.status()
	print status

if __name__ == "__main__":
	main()
	sys.exit(0)
```

### 잔액정보 읽어오기

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
	cool = coolsms.rest(api_key, api_secret)
	cash, point = cool.balance()
	print "cash : %u, point : %u" % (cash, point)

if __name__ == "__main__":
	main()
	sys.exit(0)
```

