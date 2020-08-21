# Message



## Message

문자발송 관련 예제 입니다.

### SMS\(단문\) 발송

- 90바이트\( 한글 45자 \) 이내의 내용을 문자 메시지로 보낼 수 있습니다.

```text
import sys
from sdk.api.message import Message
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to send sms through CoolSMS Rest API PHP
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    ## 4 params(to, from, type, text) are mandatory. must be filled
    params = dict()
    params['type'] = 'sms' # Message type ( sms, lms, mms, ata )
    params['to'] = '01000000000' # Recipients Number '01000000000,01000000001'
    params['from'] = '01000000000' # Sender number
    params['text'] = 'Test Message' # Message

    cool = Message(api_key, api_secret)
    try:
        response = cool.send(params)
        print("Success Count : %s" % response['success_count'])
        print("Error Count : %s" % response['error_count'])
        print("Group ID : %s" % response['group_id'])

        if "error_list" in response:
            print("Error List : %s" % response['error_list'])

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

### LMS\(장문\) 발송

- 2000바이트\( 한글 1000자 \) 이내의 내용을 문자 메시지로 보낼 수 있습니다.

- params\['type'\] 을 'LMS'로 바꿔주시면 됩니다.

```text
import sys
from sdk.api.message import Message
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to send sms through CoolSMS Rest API PHP
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    ## 4 params(to, from, type, text) are mandatory. must be filled
    params = dict()
    params['type'] = 'lms' # Message type ( sms, lms, mms, ata )
    params['to'] = '01000000000' # Recipients Number '01000000000,01000000001'
    params['from'] = '01000000000' # Sender number
    params['text'] = 'LMS Message Until 2000 byte' # Message

    cool = Message(api_key, api_secret)
    try:
        response = cool.send(params)
        print("Success Count : %s" % response['success_count'])
        print("Error Count : %s" % response['error_count'])
        print("Group ID : %s" % response['group_id'])

        if "error_list" in response:
            print("Error List : %s" % response['error_list'])

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

### MMS\(포토문자\) 발송

- 이미지\( 300KB미만의 2024\*2024이하 JPG, GIF, PNG \) 를 포함한 내용을 문자 메시지로 보낼 수 있습니다.

- params\['type'\] 을 'MMS'로 바꿔주세요.

- params\['image'\] 에 해당 경로와 함께 이미지 파일명을 넣어주세요. 예\) '../images/test.jpg'

```text
import sys

from sdk.api.message import Message
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to send sms through CoolSMS Rest API PHP
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    ## 4 params(to, from, type, text) are mandatory. must be filled
    params = dict()
    params['type'] = 'mms' # Message type ( sms, lms, mms, ata )
    params['to'] = '01000000000' # Recipients Number '01000000000,01000000001'
    params['from'] = '01000000000' # Sender number
    params['text'] = 'MMS Message' # Message
    params["image"] = "../image/test.jpg" # image for MMS. type must be set as "MMS"

    cool = Message(api_key, api_secret)
    try:
        response = cool.send(params)
        print("Success Count : %s" % response['success_count'])
        print("Error Count : %s" % response['error_count'])
        print("Group ID : %s" % response['group_id'])

        if "error_list" in response:
            print("Error List : %s" % response['error_list'])

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

### 예약문자 발송

- 예약해둔 날짜에 문자 메시지를 보낼 수 있습니다.

- params\['datetime'\] 에 날짜를 넣어주세요. 예\) '20160221150000' // 2016년 2월 21일 15시 00분 00초

```text
import sys
from sdk.api.message import Message
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to send sms through CoolSMS Rest API PHP
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    ## 4 params(to, from, type, text) are mandatory. must be filled
    params = dict()
    params['type'] = 'sms' # Message type ( sms, lms, mms, ata )
    params['to'] = '01000000000' # Recipients Number '01000000000,01000000001'
    params['from'] = '01000000000' # Sender number
    params['text'] = 'Test Message' # Message
    params["datetime"] = "20140106153000" # Format must be(YYYYMMDDHHMISS) 2014 01 06 15 30 00 (2014 Jan 06th 3pm 30 00)

    cool = Message(api_key, api_secret)
    try:
        response = cool.send(params)
        print("Success Count : %s" % response['success_count'])
        print("Error Count : %s" % response['error_count'])
        print("Group ID : %s" % response['group_id'])

        if "error_list" in response:
            print("Error List : %s" % response['error_list'])

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

### 알림톡 발송

- Sender Key와 Template Code는 필수입니다. 옆에 링크 페이지에 가셔서 발급받아주세요. [발급받기](http://www.coolsms.co.kr/AboutAlimTalk)

- params\['type'\]을 ATA로 해주세요.

- params\['sender\_key'\], params\['template\_code'\]에 발급받으신 Sender Key와 Template Code를 넣어주세요.

- params\['text'\]에는 해당 Template Code와 같은 형태의 내용만 입력 가능하며 {홍길동}과 같이 {}로 둘러 쌓여있는 부분은 다른 내용으로 변환이 가능합니다.

```text
import sys
from sdk.api.message import Message
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to send sms through CoolSMS Rest API PHP
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    ## 4 params(to, from, type, text) are mandatory. must be filled
    params = dict()
    params['type'] = 'ata' # Message type ( sms, lms, mms, ata )
    params['to'] = '01000000000' # Recipients Number '01000000000,01000000001'
    params['from'] = '01000000000' # Sender number
    params["sender_key"] = "#ENTER_YOUR_SENDER_KEY#" # 알림톡 사용을 위해 필요합니다. 신청방법 : http://www.coolsms.co.kr/AboutAlimTalk
    params["template_code"] = "#ENTER_YOUR_TEMPLATE_CODE#" # 알림톡 template code 입니다. 자세한 설명은 http://www.coolsms.co.kr/AboutAlimTalk을 참조해주세요. 

    # 알림톡에서 메시지내용은 Template Code에 맞는 메시지 내용이어야 하며 '#{홍길동}'과 같은 변수들은 다른 String으로 대체가 가능합니다.
    params['text'] = '#{홍길동}님이 #{게시판}에 새로운 게시물을 등록하였습니다.' 

    cool = Message(api_key, api_secret)
    try:
        response = cool.send(params)
        print("Success Count : %s" % response['success_count'])
        print("Error Count : %s" % response['error_count'])
        print("Group ID : %s" % response['group_id'])

        if "error_list" in response:
            print("Error List : %s" % response['error_list'])

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

### 예약문자 취소

- 아직 발송되지 않은 예약문자를 취소 할 수 있습니다.

- params\['message\_id'\] or params\['group\_id'\] 안에 해당 문자의 message\_id나 group\_id를 넣어주시면 됩니다.

```text
import sys
from sdk.api.message import Message
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to cancel reserved sms through CoolSMS Rest API
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    params = dict()
    params['message_id'] = 'MID57A423F131F01'
    # params['group_id'] = 'GID57A423F131C0F'

    cool = Message(api_key, api_secret)
    try:
        response = cool.cancel(params)
        print("Response : %s" % response)
    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

### 잔액정보 확인

- Coolsms 잔액정보를 확인 할 수 있습니다.

```text
import sys
from sdk.api.message import Message
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to check cash & point balance through CoolSMS Rest API
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    cool = Message(api_key, api_secret)
    try:
        response = cool.balance()
        print("Cash : %s" % response['cash']) # 남은 캐쉬
        print("Point : %s" % response['point']) # 남은 포인트
        print("Deferred Payment: %s" % response['deferred_payment']) # 후불회원인지 확인
    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

### 메시지내역 보기

- 발송 한 메시지 내역을 확인 할 수 있습니다.

- 관련 Parameter 들은 [Reference gruide](http://www.coolsms.co.kr/opage/manual/php/index.html)를 참고 해주세요.

```text
import sys
from sdk.api.message import Message
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to check sms result through CoolSMS Rest API
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    # 4 params(to, from, type, text) are mandatory. must be filled
    params = dict()
    # params["messaage_id"] = "M52CB443257C61" # message id
    # params["group_id"] = "G52CB4432576C8" # group id
    # params["offset"] = "0" # default 0
    # params["limit"] = "1" # default 20
    # params["rcpt"] = "01000000000" # search sent result by recipient number 
    # params["start"] = "201601070915" # set search start date 
    # params["end"] = "201601071230" # set search end date

    cool = Message(api_key, api_secret)
    try:
        i = 0
        response = cool.sent(params)
        for data in response['data']:
            i += 1
            print("Message No.%s" % i)
            print("Type : %s" % data['type'])
            print("Accepted_time : %s" % data['accepted_time'])
            print("Recipient_number : %s" % data['recipient_number'])
            print("Group_id : %s" % data['group_id'])
            print("Message_id : %s" % data['message_id'])
            print("Status : %s" % data['status'])
            print("Result_code : %s" % data['result_code'])
            print("Result_message : %s" % data['result_message'])
            print("Sent_time : %s" % data['sent_time'])
            print("Text : %s" % data['text'])
            print("Carrier : %s" % data['carrier'])
            print("Scheduled_time : %s" % data['scheduled_time'])

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

