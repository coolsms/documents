# SenderID



## SenderID

발신번호 관련 예제 입니다.

### 등록 요청

\* 보안상 문제로 현재는 제공하지 않습니다. 쿨에스엠에스 사이트에서 발신번호를 등록해 주세요

- 발신번호 등록을 요청합니다.

- 1544-\*\*\*\*와 같은 번호나 등록이 되지 않는 전화번호는 증빙자료를 이용한 발신번호 등록을 이용해주세요. =&gt; [바로가기](http://www.coolsms.co.kr/index.php?mid=service_setup&act=dispSmsconfigSenderNumbers)

```text
package net.nurigo.java_sdk.examples.SenderID;

import java.util.HashMap;
import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.SenderID;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleRegister
 * @brief This sample code demonstrate how to request sender number register through CoolSMS Rest API PHP
 */
public class ExampleRegister {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";

    try {
      SenderID coolsms = new SenderID(api_key, api_secret);

      // phone are mandatory. must be filled
      HashMap<String, String> params = new HashMap<String, String>();
      params.put("phone", "01000000000"); // sender number to register 

      // Optional parameters for your own needs
      // params.put("site_user", "admin"); // site user id. '__private__' is default

      JSONObject obj = (JSONObject) coolsms.register(params);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### 등록 확인

\* 보안상 문제로 현재는 제공하지 않습니다. 쿨에스엠에스 사이트에서 발신번호를 등록해 주세요

- 등록 요청한 전화번호로 '등록 요청'시 나왔던 ARS 번호에 전화를 걸어주세요.

- '지금은 전화를 받지 않습니다' 등의 메시지가 나오면 정상입니다.

- 프로그램이 확인 할 수 있도록 메시지가 나온 뒤 바로 끊지 말고 잠시 대기 해주세요.

- 위 순서를 거친 후 '등록 요청'에서 받은 Handle\_key를 이용해 '등록 확인'을 하시면 됩니다. \( response가 없으면 성공 \)

```text
package net.nurigo.java_sdk.examples.SenderID;

import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.SenderID;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleVerify
 * @brief This sample code demonstrate how to verify sender number through CoolSMS Rest API PHP
 */
public class ExampleVerify {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";

    try {
      SenderID coolsms = new SenderID(api_key, api_secret);

      // handle_key are mandatory
      String handle_key = "SID56FA3A1266426"; // sender number handle key. check for 'ExampleList'

      JSONObject obj = (JSONObject) coolsms.verify(handle_key);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### 발신번호 리스트 가져오기

- 발신번호 리스트를 확인합니다.

```text
package net.nurigo.java_sdk.examples.SenderID;

import java.util.HashMap;
import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.SenderID;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleGetSenderIdList
 * @brief This sample code demonstrate how to check sender number list through CoolSMS Rest API PHP
 */
public class ExampleGetSenderIdList {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";

    try {
      SenderID coolsms = new SenderID(api_key, api_secret);

      // Optional parameters for your own needs
      HashMap<String, String> params = new HashMap<String, String>();
      // params.put("site_user", "admin"); // site user id. '__private__' is default

      JSONObject obj = (JSONObject) coolsms.getSenderidList(params);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### 발신번호 삭제

- 해당 handle\_key를 가지고 있는 발신번호를 삭제합니다.

```text
package net.nurigo.java_sdk.examples.SenderID;

import java.util.HashMap;
import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.SenderID;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleDelete
 * @brief This sample code demonstrate how to delete sender number through CoolSMS Rest API PHP
 */
public class ExampleDelete {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";

    try {
      SenderID coolsms = new SenderID(api_key, api_secret);

      // handle_key are mandatory
      String handle_key = "SID56FA3A1266426"; // sender number handle key. check for 'ExampleList'

      JSONObject obj = (JSONObject) coolsms.delete(handle_key);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### 기본 발신번호 설정

- 기본 발신번호를 설정 합니다.

```text
package net.nurigo.java_sdk.examples.SenderID;

import java.util.HashMap;
import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.SenderID;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleSetDefault
 * @brief This sample code demonstrate how to set default sender number through CoolSMS Rest API PHP
 */
public class ExampleSetDefault {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";

    try {
      SenderID coolsms = new SenderID(api_key, api_secret);

      // handle_key are mandatory
      HashMap<String, String> params = new HashMap<String, String>();
      params.put("handle_key", "SID56FA3A1266426"); // sender number handle key. check for 'ExampleSenderIdList' 

      // Optional parameters for your own needs
      // params.put("site_user", "admin"); // site user id. '__private__' is default

      JSONObject obj = (JSONObject) coolsms.setDefault(params);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### 기본 발신번호 가져오기

- 기본 발신번호를 가져 옵니다.

```text
package net.nurigo.java_sdk.examples.SenderID;

import java.util.HashMap;
import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.SenderID;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleGetDefault
 * @brief This sample code demonstrate how to get default sender number through CoolSMS Rest API PHP
 */
public class ExampleGetDefault {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";

    try {
      SenderID coolsms = new SenderID(api_key, api_secret);

      // Optional parameters for your own needs
      HashMap<String, String> params = new HashMap<String, String>();
      // params.put("site_user", "admin"); // site user id. '__private__' is default

      JSONObject obj = (JSONObject) coolsms.getDefault(params);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

