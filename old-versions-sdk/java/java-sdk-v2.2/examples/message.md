# Message



## Message

문자발송 관련 예제 입니다.

### SMS\(단문\) 발송

- 90바이트\( 한글 45자 \) 이내의 내용을 문자 메시지로 보낼 수 있습니다.

```text
package net.nurigo.java_sdk.examples.Message;

import java.util.HashMap;
import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.Message;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleSend
 * @brief This sample code demonstrate how to send sms through CoolSMS Rest API PHP
 */
public class ExampleSend {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";
    Message coolsms = new Message(api_key, api_secret);

    // 4 params(to, from, type, text) are mandatory. must be filled
    HashMap<String, String> params = new HashMap<String, String>();
    params.put("to", "01000000000");
    params.put("from", "01000000000");
    params.put("type", "SMS");
    params.put("text", "Coolsms Testing Message!");
    params.put("app_version", "test app 1.2"); // application name and version

    try {
      JSONObject obj = (JSONObject) coolsms.send(params);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### LMS\(장문\) 발송

- 2000바이트\( 한글 1000자 \) 이내의 내용을 문자 메시지로 보낼 수 있습니다.

- params 의 type 을 'LMS'로 바꿔주시면 됩니다.

```text
package net.nurigo.java_sdk.examples.Message;

import java.util.HashMap;
import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.Message;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleSend
 * @brief This sample code demonstrate how to send sms through CoolSMS Rest API PHP
 */
public class ExampleSend {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";
    Message coolsms = new Message(api_key, api_secret);

    // 4 params(to, from, type, text) are mandatory. must be filled
    HashMap<String, String> params = new HashMap<String, String>();
    params.put("to", "01000000000");
    params.put("from", "01000000000");
    params.put("type", "LMS");
    params.put("text", "Coolsms Testing Message!");
    params.put("app_version", "test app 1.2"); // application name and version

    try {
      JSONObject obj = (JSONObject) coolsms.send(params);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### MMS\(포토문자\) 발송

- 이미지\( 300KB미만의 2024\*2024이하 JPG, GIF, PNG \) 를 포함한 내용을 문자 메시지로 보낼 수 있습니다.

- params 의 type 을 'MMS'로 바꿔주세요.

- params 의 image 에 해당 경로와 함께 이미지 파일명을 넣어주세요. 예\) './images/test.jpg'

```text
package net.nurigo.java_sdk.examples.Message;

import java.util.HashMap;
import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.Message;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleSend
 * @brief This sample code demonstrate how to send sms through CoolSMS Rest API PHP
 */
public class ExampleSend {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";
    Message coolsms = new Message(api_key, api_secret);

    // 4 params(to, from, type, text) are mandatory. must be filled
    HashMap<String, String> params = new HashMap<String, String>();
    params.put("to", "01000000000");
    params.put("from", "01000000000");
    params.put("type", "SMS");
    params.put("text", "Coolsms Testing Message!");
    params.put("app_version", "test app 1.2"); // application name and version
    params.put("image", "images/test.jpg"); // image for MMS. type must be set as "MMS"

    try {
      JSONObject obj = (JSONObject) coolsms.send(params);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### 예약문자 발송

- 예약해둔 날짜에 문자 메시지를 보낼 수 있습니다.

- params 의 datetime 에 날짜를 넣어주세요. 예\) '20160221150000' // 2016년 2월 21일 15시 00분 00초

```text
package net.nurigo.java_sdk.examples.Message;

import java.util.HashMap;
import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.Message;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleSend
 * @brief This sample code demonstrate how to send sms through CoolSMS Rest API PHP
 */
public class ExampleSend {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";
    Message coolsms = new Message(api_key, api_secret);

    // 4 params(to, from, type, text) are mandatory. must be filled
    HashMap<String, String> params = new HashMap<String, String>();
    params.put("to", "01000000000");
    params.put("from", "01000000000");
    params.put("type", "SMS");
    params.put("text", "Coolsms Testing Message!");
    params.put("app_version", "test app 1.2"); // application name and version
    params.put("datetime", "20160221150000"); // Format must be(YYYYMMDDHHMISS) 2016-02-21 15:00:00

    try {
      JSONObject obj = (JSONObject) coolsms.send(params);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### 알림톡 발송

- Sender Key와 Template Code는 필수입니다. 옆에 링크 페이지에 가셔서 발급받아주세요. [발급받기](http://www.coolsms.co.kr/AboutAlimTalk)

- params 의 type을 ATA로 해주세요.

- params-&gt;sender\_key, params-&gt;template\_code에 발급받으신 Sender Key와 Template Code를 넣어주세요.

- params 의 text에는 해당 Template Code와 같은 형태의 내용만 입력 가능하며 {홍길동}과 같이 {}로 둘러 쌓여있는 부분은 다른 내용으로 변환이 가능합니다.

```text
package net.nurigo.java_sdk.examples.Message;

import java.util.HashMap;
import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.Message;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleSend
 * @brief This sample code demonstrate how to send sms through CoolSMS Rest API PHP
 */
public class ExampleSend {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";
    Message coolsms = new Message(api_key, api_secret);

    // 4 params(to, from, type, text) are mandatory. must be filled
    HashMap<String, String> params = new HashMap<String, String>();
    params.put("to", "01000000000"); // 수신번호
    params.put("from", "01000000000"); // 발신번호
    params.put("type", "ATA"); // Message type ( SMS, LMS, MMS, ATA )
    params.put("text", "Test Message"); // 알림톡 사용시 해당 template_code의 메시지 내용과 동일해야하며 "{}"로 둘러쌓여있는 변수는 다른 내용으로 변경 가능합니다.
    params.put("app_version", "JAVA SDK v1.2"); // application name and version
    params.put("sender_key", "55540253a3e61072f57ed5d4cc2ecf965e15bb64"); // 알림톡 사용을 위해 필요합니다. 신청방법 : http://www.coolsms.co.kr/AboutAlimTalk
    params.put("template_code", "C004"); // 알림톡 template code 입니다. 자세한 설명은 http://www.coolsms.co.kr/AboutAlimTalk을 참조해주세요. 
    params.put("button_name", "바로가기"); // 알림톡 버튼이름 입니다.
    params.put("button_url", "http://www.coolsms.co.kr"); // 알림톡 버튼URL 입니다.

    try {
      JSONObject obj = (JSONObject) coolsms.send(params);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### 예약문자 취소

- 아직 발송되지 않은 예약문자를 취소 할 수 있습니다.

- params 의 mid or gid 안에 해당 문자의 mid나 gid를 넣어주시면 됩니다.

```text
package net.nurigo.java_sdk.examples.Message;

import java.util.HashMap;
import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.Message;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleCancel
 * @brief This sample code demonstrate how to cancel reserved sms through CoolSMS Rest API PHP
 */
public class ExampleCancel {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";
    Message coolsms = new Message(api_key, api_secret);

    // Either mid or gid is must be entered
    HashMap<String, String> params = new HashMap<String, String>();
    // params.put("message_id", "M52CB443257C61"); // message id
    // params.put("group_id", "G52CB4432576C8"); // group id

    try {
      JSONObject obj = (JSONObject) coolsms.cancel(params);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### 잔액정보 확인

- Coolsms 잔액정보를 확인 할 수 있습니다.

```text
package net.nurigo.java_sdk.examples.Message;

import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.Message;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleGetBalance
 * @brief This sample code demonstrate how to check cash & point balance through CoolSMS Rest API PHP
 */
public class ExampleGetBalance {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";
    Message coolsms = new Message(api_key, api_secret);

    try {
      JSONObject obj = (JSONObject) coolsms.balance();
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### 메시지내역 보기

- 발송 한 메시지 내역을 확인 할 수 있습니다.

- 관련 Parameter 들은 [Reference gruide](http://www.coolsms.co.kr/opage/manual/java/index.html)를 참고 해주세요.

```text
package net.nurigo.java_sdk.examples.Message;

import java.util.HashMap;
import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.Message;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleSent
 * @brief This sample code demonstrate how to check sms result through CoolSMS Rest API PHP
 */
public class ExampleSent {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";
    Message coolsms = new Message(api_key, api_secret);

    // Optional parameters for your own needs
    HashMap<String, String> params = new HashMap<String, String>();
    // 4 params(to, from, type, text) are mandatory. must be filled
    // params.put("message_id", "M52CB443257C61"); // message id
    // params.put("group_id", "G52CB4432576C8"); // group id
    // params.put("offset", "0"); // default 0
    // params.put("limit", "20"); // default 20
    // params.put("rcpt", "01000000000"); // search sent result by recipient number 
    // params.put("start", "201601070915"); // set search start date 
    // params.put("end", "201601071230"); // set search end date

    try {
      JSONObject obj = (JSONObject) coolsms.sent(params);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

