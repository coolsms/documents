# Image



## Image

포토 문자에 사용 될 이미지 관리 관련 예제 입니다.

### 서버에 이미지 파일 등록

- 이미지 파일을 쿨에스엠에스 미디어 서버에 저장합니다.

```text
package net.nurigo.java_sdk.examples.Image;

import java.util.HashMap;
import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.Image;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleUploadImage
 * @brief This sample code demonstrate how to upload image through CoolSMS Rest API PHP
 */
public class ExampleUploadImage {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";
    Image coolsms = new Image(api_key, api_secret);

    // Optional parameters for your own needs
    HashMap<String, String> params = new HashMap<String, String>();
    params.put("image", "./test.jpg"); // image
    // params.put("encoding", "binary"); // image encoding type (base64, binary) default binary
    // params.put("limit", "20"); // default 20

    try {
      JSONObject obj = (JSONObject) coolsms.uploadImage(params);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### 이미지 리스트 보기

- 등록된 이미지를 확인 할 수 있습니다.

```text
package net.nurigo.java_sdk.examples.Image;

import java.util.HashMap;
import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.Image;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleGetImageList
 * @brief This sample code demonstrate how to check image list through CoolSMS Rest API PHP
 */
public class ExampleGetImageList {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";
    Image coolsms = new Image(api_key, api_secret);

    // Optional parameters for your own needs
    HashMap<String, String> params = new HashMap<String, String>();
    // params.put("offset", "0"); // default 0
    // params.put("limit", "20"); // default 20

    try {
      JSONObject obj = (JSONObject) coolsms.getImageList(params);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### 이미지 정보 보기

- 해당 이미지 파일의 정보를 확인 할 수 있습니다.

```text
package net.nurigo.java_sdk.examples.Image;

import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.Image;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleGetImageInfo
 * @brief This sample code demonstrate how to check image info through CoolSMS Rest API PHP
 */
public class ExampleGetImageInfo {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";
    Image coolsms = new Image(api_key, api_secret);

    // image_id are mandatory
    String image_id = "IMG56fce743e4daa"; // image id

    try {
      JSONObject obj = (JSONObject) coolsms.getImageInfo(image_id);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### 이미지 삭제

- 해당 이미지를 서버에서 삭제합니다.

```text
package net.nurigo.java_sdk.examples.Image;

import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.Image;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleDeleteImage
 * @brief This sample code demonstrate how to delete images through CoolSMS Rest API PHP
 */
public class ExampleDeleteImage {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";
    Image coolsms = new Image(api_key, api_secret);

    // image_ids are mandatory
    String image_ids = "IMG56fce743e4daa,IMG56fce598851bc"; // image ids. ex)'IM34BWIDJ12','IMG2559GBB'

    try {
      JSONObject obj = (JSONObject) coolsms.deleteImages(image_ids);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

