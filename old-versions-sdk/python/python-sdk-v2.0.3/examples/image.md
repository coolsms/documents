# Image



## Image

포토문자\(MMS\)에 사용 될 이미지 관리 관련 예제 입니다.

### 서버에 이미지 파일 등록

- 이미지 파일을 쿨에스엠에스 미디어 서버에 저장합니다.

```text
import sys
from sdk.api.image import Image
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to upload image through CoolSMS Rest API
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    # image is must be entered
    image = "test.jpg" # image file
    cool = Image(api_key, api_secret)

    try:
        response = cool.upload_image(image)
        print("Image ID : %s" % response['image_id'])

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

### 이미지 리스트 보기

- 등록된 이미지를 확인 할 수 있습니다.

```text
import sys
from sdk.api.image import Image
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to check image list through CoolSMS Rest API 
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    # Optional parameters for your own needs
    params = dict()
    # params["offset"] = "0" # default 0
    # params["limit"] = "20" # default 20
    cool = Image(api_key, api_secret)

    try:
        response = cool.get_image_list(params)
        print("Total Count : %s" % response['total_count'])
        print("Limit : %s" % response['limit'])
        print("Offset : %s" % response['offset'])
        print("List : %s" % response['list'])

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

### 이미지 정보 보기

- 해당 이미지 파일의 정보를 확인 할 수 있습니다.

```text
import sys
from sdk.api.image import Image
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to check image info through CoolSMS Rest API
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    image_id = "IMG57A42896DF7B0"
    cool = Image(api_key, api_secret)

    try:
        response = cool.get_image_info(image_id)
        print("Image_id : %s" % response['image_id'])
        print("File_name : %s" % response['file_name'])
        print("Original_name : %s" % response['original_name'])
        print("File_size : %s" % response['file_size'])
        print("Width : %s" % response['width'])
        print("Height : %s" % response['height'])
        
    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

### 이미지 삭제

- 해당 이미지를 서버에서 삭제합니다.

```text
import sys
from sdk.api.image import Image
from sdk.exceptions import CoolsmsException

##  @brief This sample code demonstrate how to delete images through CoolSMS Rest API
if __name__ == "__main__":

    # set api key, api secret
    api_key = "#ENTER_YOUR_OWN#"
    api_secret = "#ENTER_YOUR_OWN#"

    # image_id is must be entered
    image_id = "IMG57A44C8F5DC06"
    cool = Image(api_key, api_secret)

    try:
        response = cool.delete_images(image_id)
        print("Success Count : %s" % response['success_count'])
        print("Error Count : %s" % response['error_count'])
        print("Error List : %s" % response['error_list'])

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```

