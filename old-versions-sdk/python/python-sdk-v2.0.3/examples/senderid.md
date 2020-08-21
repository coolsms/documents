# SenderID



## SenderID

발신번호 관련 예제 입니다.

### 등록 요청

\* 보안상 문제로 현재는 제공하지 않습니다. 쿨에스엠에스 사이트에서 발신번호를 등록해 주세요

- 발신번호 등록을 요청합니다.

- 1544-\*\*\*\*와 같은 번호나 등록이 되지 않는 전화번호는 증빙자료를 이용한 발신번호 등록을 이용해주세요. =&gt; [바로가기](http://www.coolsms.co.kr/index.php?mid=service_setup&act=dispSmsconfigSenderNumbers)

```text
import sys
from sdk.api.sender_id import SenderID 
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to request sender number register through CoolSMS Rest API
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    # phone is mandatory.
    phone = "01000000000"

    cool = SenderID(api_key, api_secret)

    try:
        response = cool.register(phone)
        print("ARS Number : %s" % response['ars_number'])
        print("Handle Key : %s" % response['handle_key'])

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

### 등록 확인

\* 보안상 문제로 현재는 제공하지 않습니다. 쿨에스엠에스 사이트에서 발신번호를 등록해 주세요

- 등록 요청한 전화번호로 '등록 요청'시 나왔던 ARS 번호에 전화를 걸어주세요.

- '지금은 전화를 받지 않습니다' 등의 메시지가 나오면 정상입니다.

- 프로그램이 확인 할 수 있도록 메시지가 나온 뒤 바로 끊지 말고 잠시 대기 해주세요.

- 위 순서를 거친 후 '등록 요청'에서 받은 Handle\_key를 이용해 '등록 확인'을 하시면 됩니다. \( response가 없으면 성공 \)

```text
import sys
from sdk.api.sender_id import SenderID 
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to verify sender number through CoolSMS Rest API 
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    # handle_key is mandatory.
    handle_key = "SID57A8456ADD428"

    cool = SenderID(api_key, api_secret)

    try:
        response = cool.verify(handle_key)
        if response == None:
            print("Register Success")

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

### 발신번호 리스트 가져오기

- 발신번호 리스트를 확인합니다.

```text
import sys
from sdk.api.sender_id import SenderID 
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to check sender number list through CoolSMS Rest API
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    # site_id is optional.
    site_id = "user_id"

    cool = SenderID(api_key, api_secret)

    try:
        response = cool.get_list() # or cool.get_list(site_user)

        for data in response:
            print("Idno : %s" % data['idno'])
            print("Phone Number : %s" % data['phone_number'])
            print("Flag Default : %s" % data['flag_default'])
            print("Updatetime : %s" % data['updatetime'])
            print("Regdate : %s" % data['regdate'])

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

### 발신번호 삭제

- 해당 handle\_key를 가지고 있는 발신번호를 삭제합니다.

```text
import sys
from sdk.api.sender_id import SenderID 
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to delete sender number through CoolSMS Rest API
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    # handle_key is mandatory.
    handle_key = "SID57A8456ADD428"

    cool = SenderID(api_key, api_secret)

    try:
        response = cool.delete(handle_key)
        if response == None:
            print("Register Success")

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit() 
```

### 기본 발신번호 설정

- 기본 발신번호를 설정 합니다.

```text
import sys
from sdk.api.sender_id import SenderID 
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to set default sender number through CoolSMS Rest API PHP
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    # handle_key is mandatory.
    handle_key = "SID567A2B2258CF9"

    cool = SenderID(api_key, api_secret)

    try:
        response = cool.set_default(handle_key)
        if response == None:
            print("Set Default Success")

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit() 
```

### 기본 발신번호 가져오기

- 기본 발신번호를 가져 옵니다.

```text
import sys
from sdk.api.sender_id import SenderID 
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to get default sender number through CoolSMS Rest API
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    cool = SenderID(api_key, api_secret)

    try:
        response = cool.get_default()
        print("Handle Key : %s " % response['handle_key'])
        print("Phone Number : %s " % response['phone_number'])

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit() 
```

