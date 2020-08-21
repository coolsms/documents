# GroupMessage



## GroupMessage

Rest 2.0 에서 새롭게 추가 된 그룹메시지 관련 예제 입니다.

### 그룹 생성

- 메시지를 담아둘 그룹을 생성 합니다.

```text
import sys
from sdk.api.group_message import GroupMessage
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to create sms group through CoolSMS Rest API
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    # Optional parameters for your own needs
    params = dict()
    # params["charset"] = "utf8" # utf8, euckr default value is utf8
    # params["srk"] = "293DIWNEK103" # Solution key
    # params["mode"] = "test" # If 'test' value, refund cash to point
    # params["only_ata"] = "true" # If 'true' value, only send ata
    # params["delay"] = "10" # '0~20' delay messages
    # params["force_sms"] = "true"; # true is always send sms ( default true )
    # params["app_version"] = "" # A version

    cool = GroupMessage(api_key, api_secret)

    try:
        response = cool.create_group(params)
        print("Group ID : %s" % response['group_id'])

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

### 그룹 리스트 보기

- 생성된 그룹 리스트를 보여줍니다.

```text
import sys
from sdk.api.group_message import GroupMessage
from sdk.exceptions import CoolsmsException


##  @brief This sample code demonstrate how to check group list through CoolSMS Rest API
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    cool = GroupMessage(api_key, api_secret)

    try:
        response = cool.get_group_list()
        print("Group List : %s" % response['list'])

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

### 그룹 삭제

- 해당 그룹을 삭제 합니다.

- 주의! 그룹안의 메시지들이 전부 삭제 됩니다.

```text
import sys
from sdk.api.group_message import GroupMessage
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to delete sms group through CoolSMS Rest API
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    # group_ids is mandatory
    group_ids = "GID57A82D462CBBFF" # Group IDs "GID57A82D462CBBFF,GID98A82D462CDBFF ..."

    cool = GroupMessage(api_key, api_secret)

    try:
        response = cool.delete_groups(group_ids)
        print("Success Count : %s" % response['success_count'])
        print("Error Count : %s" % response['error_count'])

        if "error_list" in response:
            print("Error List : %s" % response['error_list'])

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

### 그룹 정보 보기

- 해당 그룹의 정보를 보여줍니다.

```text
import sys
from sdk.api.group_message import GroupMessage
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to check group info through CoolSMS Rest API
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    # group_id is mandatory.
    group_id = "GID57A82D462CBBF"

    cool = GroupMessage(api_key, api_secret)

    try:
        response = cool.get_group_info(group_id)
        print("Group ID : %s" % response['group_id'])
        print("Message Count : %s" % response['message_count'])

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

### 메시지 넣기

- 해당 그룹안에 메시지를 넣을 수 있습니다.

- 그룹안에 메시지를 넣을 뿐, 실제로 메시지를 발송 하는 건 아닙니다.

- \(알림톡 사용시\) Sender Key와 Template Code는 필수입니다. 옆에 링크 페이지에 가셔서 발급받아주세요. [발급받기](http://www.coolsms.co.kr/AboutAlimTalk)

- \(알림톡 사용시\) params\['type'\]을 ATA로 해주세요.

- \(알림톡 사용시\) params\['sender\_key'\], params\['template\_code'\]에 발급받으신 Sender Key와 Template Code를 넣어주세요.

- \(알림톡 사용시\) params\['text'\]에는 해당 Template Code와 같은 형태의 내용만 입력 가능하며 \#{홍길동}과 같이 \#{}로 둘러 쌓여있는 부분은 다른 내용으로 변환이 가능합니다.

```text
import sys
from sdk.api.group_message import GroupMessage
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to add messages into group through CoolSMS Rest API
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    # Options(group_id, to, from, text) are mandatory. must be filled
    params = dict()
    params["type"] = "sms" # Message type ( sms, lms, mms, ata )
    params['to'] = '01000000000' # Recipients Number '01000000000,01000000001'
    params['from'] = '01000000000' # Sender number
    params['text'] = 'Test Message' # Message
    params["group_id"] = "GID57A82D462CBBF" # Group ID

    # Optional parameters for your own needs
    # params["image_id"] = "image_id" # image_id. type must be set as 'MMS'
    # params["refname"] = "" # Reference name
    # params["country"] = "82" # Korea(82) Japan(81) America(1) China(86) Default is Korea
    # params["datetime"] = "20140106153000" # Format must be(YYYYMMDDHHMISS) 2014 01 06 15 30 00 (2014 Jan 06th 3pm 30 00)
    # params["subject"] = "Message Title" # set msg title for LMS and MMS
    # params["delay"] = "10") # '0~20' delay messages
    # params["sender_key"] = "5554025sa8e61072frrrd5d4cc2rrrr65e15bb64" # 알림톡 사용을 위해 필요합니다. 신청방법 : http://www.coolsms.co.kr/AboutAlimTalk
    # params["template_code"] = "C004" # 알림톡 template code 입니다. 자세한 설명은 http://www.coolsms.co.kr/AboutAlimTalk을 참조해주세요.

    cool = GroupMessage(api_key, api_secret)

    try:
        response = cool.add_messages(params)
        print("Success Count : %s" % response['success_count'])
        print("Error Count : %s" % response['error_count'])

        if "error_list" in response:
            print("Error List : %s" % response['error_list'])

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

### 메시지 넣기\( JSON 형식 \)

- JSON 형식으로 된 메시지 리스트를 받아서 해당 그룹안에 메시지를 넣을 수 있습니다.

- 아래 예제와 같이 텍스트값 등 다양하게 정렬된 메시지를 서버에 JSON 형식으로 보내줍니다.

- 그룹안에 메시지를 넣을 뿐, 실제로 메시지를 발송 하는 건 아닙니다.

-  json\_data에 원하는 만큼 params를 넣을 수 있습니다.

- \(알림톡 사용시\) Sender Key와 Template Code는 필수입니다. 옆에 링크 페이지에 가셔서 발급받아주세요. [발급받기](http://www.coolsms.co.kr/AboutAlimTalk)

- \(알림톡 사용시\) $message-&gt;type을 ATA로 해주세요.

- \(알림톡 사용시\) $messageparams\['sender\_key'\], params\['template\_code'\]에 발급받으신 Sender Key와 Template Code를 넣어주세요.

- \(알림톡 사용시\) $message-&gt;text에는 해당 Template Code와 같은 형태의 내용만 입력 가능하며 \#{홍길동}과 같이 \#{}로 둘러 쌓여있는 부분은 다른 내용으로 변환이 가능합니다

```text
import sys
import json
from sdk.api.group_message import GroupMessage
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to add messages into group through CoolSMS Rest API
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    # Options(group_id, to, from, text) are mandatory. must be filled
    group_id = "GID57A82D462CBBF" # Group ID

    json_data = list()
    params = dict()
    params["type"] = "sms" # Message type ( sms, lms, mms, ata )
    params['to'] = '01000000000' # Recipients Number '01000000000,01000000001'
    params['from'] = '01000000000' # Sender number
    params['text'] = 'Test Message' # Message

    # Optional parameters for your own needs
    # params["image_id"] = "image_id" # image_id. type must be set as 'MMS'
    # params["refname"] = "" # Reference name
    # params["country"] = "82" # Korea(82) Japan(81) America(1) China(86) Default is Korea
    # params["datetime"] = "20140106153000" # Format must be(YYYYMMDDHHMISS) 2014 01 06 15 30 00 (2014 Jan 06th 3pm 30 00)
    # params["subject"] = "Message Title" # set msg title for LMS and MMS
    # params["delay"] = "10") # '0~20' delay messages
    # params["sender_key"] = "5554025sa8e61072frrrd5d4cc2rrrr65e15bb64" # 알림톡 사용을 위해 필요합니다. 신청방법 : http://www.coolsms.co.kr/AboutAlimTalk
    # params["template_code"] = "C004" # 알림톡 template code 입니다. 자세한 설명은 http://www.coolsms.co.kr/AboutAlimTalk을 참조해주세요.

    json_data.append(params) # 원하는 만큼 params를 넣어줍니다
    json_data = json.dumps(json_data)

    cool = GroupMessage(api_key, api_secret)

    try:
        response = cool.add_messages_json(group_id, json_data)
        for data in response:
            print("Success Count : %s" % data['success_count'])
            print("Error Count : %s" % data['error_count'])

            if "error_list" in response:
                print("Error List : %s" % response['error_list'])

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

### 메시지 리스트 보기

- 메시지 리스트를 확인 할 수 있습니다.

```text
import sys
from sdk.api.group_message import GroupMessage
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate check message list through CoolSMS Rest API
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    # group_id is mandatory
    params = dict()
    params['group_id'] = "GID57A82D462CBBF" # Group ID
    # params["offset"] = "0" // default 0
    # params["limit"] = "20" // default 20

    cool = GroupMessage(api_key, api_secret)

    try:
        response = cool.get_message_list(params)
        print("Total Count : %s" % response['total_count'])
        print("Limit : %s" % response['limit'])
        print("Offset : %s" % response['offset'])
        print("List : %s" % response['list'])

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

### 메시지 삭제

- 해당 메시지를 삭제 합니다.

```text
import sys
from sdk.api.group_message import GroupMessage
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to delete messages through CoolSMS Rest API
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    # group_id, message_ids are mandatory.
    group_id = "GID57A82D462CBBF" # Group ID
    message_ids = "MID2738AWQIEQQ" # Message IDs "MID29EII1913,MID1839231REE ..."

    cool = GroupMessage(api_key, api_secret)

    try:
        response = cool.delete_messages(group_id, message_ids)
        print("Success Count : %s" % response['success_count'])
        print("Error Count : %s" % response['error_count'])

        if "error_list" in response:
            print("Error List : %s" % response['error_list'])

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

### 메시지 전송

- 해당 그룹의 메시지를 전송 합니다. 전송 후 그룹은 사라지게 됩니다.

```text
import sys
from sdk.api.group_message import GroupMessage
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to check group info through CoolSMS Rest API
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    # group_id mandatory. must be filled
    group_id = "GID57A82D462CBBF" # Group ID

    cool = GroupMessage(api_key, api_secret)

    try:
        response = cool.send(group_id)
        print("Group ID : %s" % response['group_id'])

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

