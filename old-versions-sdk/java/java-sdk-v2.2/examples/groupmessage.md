# GroupMessage



## GroupMessage

Rest 2.0 에서 새롭게 추가 된 그룹메시지 관련 예제 입니다.

### 그룹 생성

- 메시지를 담아둘 그룹을 생성 합니다.

```text
package net.nurigo.java_sdk.examples.GroupMessage;

import java.util.HashMap;
import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.GroupMessage;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleCreateGroup
 * @brief This sample code demonstrate how to create sms group through CoolSMS Rest API PHP
 */
public class ExampleCreateGroup {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";
    GroupMessage coolsms = new GroupMessage(api_key, api_secret);

    // Optional parameters for your own needs
    HashMap<String, String> params = new HashMap<String, String>();
    // params.put("charset", "utf8"); // utf8, euckr default value is utf8
    // params.put("srk", "293DIWNEK103"); // Solution key
    // params.put("mode", "test"); // If 'test' value, refund cash to point
    // params.put("delay", '10'); // '0~20' delay messages
    // params.put("force_sms", true); // true is always send sms ( default true )
    // params.put("app_version", ""); 	// App version

    try {
      JSONObject obj = (JSONObject) coolsms.createGroup(params);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### 그룹 리스트 보기

- 생성된 그룹 리스트를 보여줍니다.

```text
package net.nurigo.java_sdk.examples.GroupMessage;

import java.util.HashMap;
import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.GroupMessage;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleCreateGroup
 * @brief This sample code demonstrate how to check group list through CoolSMS Rest API PHP
 */
public class ExampleGroupList {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";
    GroupMessage coolsms = new GroupMessage(api_key, api_secret);

    try {
      JSONObject obj = (JSONObject) coolsms.getGroupList();
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### 그룹 삭제

- 해당 그룹을 삭제 합니다.

- 주의! 그룹안의 메시지들이 전부 삭제 됩니다.

```text
package net.nurigo.java_sdk.examples.GroupMessage;

import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.GroupMessage;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleAddMessages
 * @brief This sample code demonstrate how to delete sms group through CoolSMS Rest API PHP
 */
public class ExampleDeleteGrouops {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";
    GroupMessage coolsms = new GroupMessage(api_key, api_secret);

    // group_ids are mandatory		
    String group_ids = "GID56FCE501593C8,GID56FB7C8A9A135"; // Group IDs

    try {
      JSONObject obj = (JSONObject) coolsms.deleteGroups(group_ids);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### 그룹 정보 보기

- 해당 그룹의 정보를 보여줍니다.

```text
package net.nurigo.java_sdk.examples.GroupMessage;

import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.GroupMessage;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleAddMessages
 * @brief This sample code demonstrate how to check group info through CoolSMS Rest API PHP
 */
public class ExampleGroupInfo {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";
    GroupMessage coolsms = new GroupMessage(api_key, api_secret);

    // group_id, message_ids are mandatory.
    String group_id = "GID56FA3B1BF0826"; // Group ID	

    try {
      JSONObject obj = (JSONObject) coolsms.getGroupInfo(group_id);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### 메시지 넣기

- 해당 그룹안에 메시지를 넣을 수 있습니다.

- 그룹안에 메시지를 넣을 뿐, 실제로 메시지를 발송 하는 건 아닙니다.

- Sender Key와 Template Code는 필수입니다. 옆에 링크 페이지에 가셔서 발급받아주세요. [발급받기](http://www.coolsms.co.kr/AboutAlimTalk)

- params 의 type을 ATA로 해주세요.

- params-&gt;sender\_key, params-&gt;template\_code에 발급받으신 Sender Key와 Template Code를 넣어주세요.

- params 의 text에는 해당 Template Code와 같은 형태의 내용만 입력 가능하며 {홍길동}과 같이 {}로 둘러 쌓여있는 부분은 다른 내용으로 변환이 가능합니다.

- 알림톡 사용시 메시지 내용은 해당 template\_code의 메시지 내용과 동일해야하며 "{}"로 둘러쌓여있는 변수는 다른 내용으로 변경 가능합니다.

```text
package net.nurigo.java_sdk.examples.GroupMessage;

import java.util.HashMap;

import org.json.simple.JSONObject;

import net.nurigo.java_sdk.api.GroupMessage;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleAddMessages
 * @brief This sample code demonstrate how to add messages into group through CoolSMS Rest API PHP
 */
public class ExampleAddMessages {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";
    GroupMessage coolsms = new GroupMessage(api_key, api_secret);

    HashMap<String, String> params = new HashMap<String, String>();

    // options(to, from, text) are mandatory. must be filled
    params.put("to", "01000000000");
    params.put("from", "01000000000");
    params.put("text", "Coolsms Testing Message!"); 
    params.put("group_id", "GID56FA3B1BF0826"); // Group ID	    

    // Optional parameters for your own needs
    // params.put("type", "SMS"); // Message type ( SMS, LMS, MMS, ATA )
    // params.put("image_id", "image_id"); // image_id. type must be set as 'MMS'
    // params.put("refname", ""); // Reference name
    // params.put("country", "82"); // Korea(82) Japan(81) America(1) China(86) Default is Korea
    // params.put("datetime", "20140106153000"); // Format must be(YYYYMMDDHHMISS) 2014 01 06 15 30 00 (2014 Jan 06th 3pm 30 00)
    // params.put("subject", "Message Title"); // set msg title for LMS and MMS
    // params.put("delay", "10"); // '0~20' delay messages
    // params.put("sender_key", "55540253a3e61072f57ed5d4cc2ecf965e15bb64"); // 알림톡 사용을 위해 필요합니다. 신청방법 : http://www.coolsms.co.kr/AboutAlimTalk
    // params.put("template_code", "C004"); // 알림톡 template code 입니다. 자세한 설명은 http://www.coolsms.co.kr/AboutAlimTalk을 참조해주세요.

    try {
      JSONObject obj = (JSONObject) coolsms.addMessages(params);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### 메시지 넣기\( JSON 형식 \)

- JSON 형식으로 된 메시지 리스트를 받아서 해당 그룹안에 원하는 만큼 JSONObject를 넣을 수 있습니다.

- 그룹안에 메시지를 넣을 뿐, 실제로 메시지를 발송 하는 건 아닙니다.

- Sender Key와 Template Code는 필수입니다. 옆에 링크 페이지에 가셔서 발급받아주세요. [발급받기](http://www.coolsms.co.kr/AboutAlimTalk)

- params 의 type을 ATA로 해주세요.

- params-&gt;sender\_key, params-&gt;template\_code에 발급받으신 Sender Key와 Template Code를 넣어주세요.

- params 의 text에는 해당 Template Code와 같은 형태의 내용만 입력 가능하며 {홍길동}과 같이 {}로 둘러 쌓여있는 부분은 다른 내용으로 변환이 가능합니다.

- 알림톡 사용시 메시지 내용은 해당 template\_code의 메시지 내용과 동일해야하며 "{}"로 둘러쌓여있는 변수는 다른 내용으로 변경 가능합니다.

```text
package net.nurigo.java_sdk.examples.GroupMessage;

import java.util.HashMap;
import org.json.simple.JSONArray;
import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.GroupMessage;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleAddMessages
 * @brief This sample code demonstrate how to add messages into group through CoolSMS Rest API PHP
 */
public class ExampleAddMessagesJSON {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";
    GroupMessage coolsms = new GroupMessage(api_key, api_secret);

    JSONObject msg = new JSONObject();
    JSONArray messages = new JSONArray();
    String group_id = "GID5733EFC59F79E"; // Group ID             

    // options(to, from, text) are mandatory. must be filled
    msg.put("type", "SMS");
    msg.put("to", "01000000000, 01000000001"); // 수신번호
    msg.put("text", "Test Message"); // 문자내용
    msg.put("from", "01000000000"); // 10월 16일 부터 발신번호 등록제 적용으로 인해 등록된 발신번호만 사용이 가능합니다

    // Optional parameters for your own needs
    // msg.put("type", "SMS"); // Message type ( SMS, LMS, MMS, ATA )
    // msg.put("image_id", "image_id"); // image_id. type must be set as 'MMS'
    // msg.put("refname", ""); // Reference name
    // msg.put("country", "82"); // Korea(82) Japan(81) America(1) China(86) Default is Korea
    // msg.put("datetime", "20140106153000"); // Format must be(YYYYMMDDHHMISS) 2014 01 06 15 30 00 (2014 Jan 06th 3pm 30 00)
    // msg.put("subject", "Message Title"); // set msg title for LMS and MMS
    // msg.put("delay", "10"); // '0~20' delay messages
    // msg.put("sender_key", "55540253a3e61072f57ed5d4cc2ecf965e15bb64"); // 알림톡 사용을 위해 필요합니다. 신청방법 : http://www.coolsms.co.kr/AboutAlimTalk
    // msg.put("template_code", "C004"); // 알림톡 template code 입니다. 자세한 설명은 http://www.coolsms.co.kr/AboutAlimTalk을 참조해주세요.

    messages.add(msg); // 원하는 만큼 JSONObject를 넣어주시면 됩니다  

    try {
      JSONObject obj = (JSONObject) coolsms.addMessagesJSON(group_id, messages);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### 메시지 리스트 보기

- 메시지 리스트를 확인 할 수 있습니다.

```text
package net.nurigo.java_sdk.examples.GroupMessage;

import java.util.HashMap;
import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.GroupMessage;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleCreateGroup
 * @brief This sample code demonstrate check message list through CoolSMS Rest API PHP
 */
public class ExampleMessageList {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";
    GroupMessage coolsms = new GroupMessage(api_key, api_secret);

    // Optional parameters for your own needs
    HashMap<String, String> params = new HashMap<String, String>();
    params.put("group_id", "GID56FA3B1BF0826"); // Group ID
    // params.put("offset", "0"); // default 0
    // params.put("limit", "20"); // default 20

    try {
      JSONObject obj = (JSONObject) coolsms.getMessageList(params);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### 메시지 삭제

- 해당 메시지를 삭제 합니다.

```text
package net.nurigo.java_sdk.examples.GroupMessage;

import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.GroupMessage;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleAddMessages
 * @brief This sample code demonstrate how to delete messages through CoolSMS Rest API PHP
 */
public class ExampleDeleteMessages {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";
    GroupMessage coolsms = new GroupMessage(api_key, api_secret);

    // group_id, message_ids are mandatory.
    String group_id = "GID56FA3B1BF0826"; // Group ID
    String message_ids = "MID56FA3B405A847, MIDFFFA3B405A847"; // Message Ids

    try {
      JSONObject obj = (JSONObject) coolsms.deleteMessages(group_id, message_ids);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

### 메시지 전송

- 해당 그룹안의 메시지를 전송 합니다.

```text
package net.nurigo.java_sdk.examples.GroupMessage;

import org.json.simple.JSONObject;
import net.nurigo.java_sdk.api.GroupMessage;
import net.nurigo.java_sdk.exceptions.CoolsmsException;

/**
 * @class ExampleAddMessages
 * @brief This sample code demonstrate how to check group info through CoolSMS Rest API PHP
 */
public class ExampleSend {
  public static void main(String[] args) {
    String api_key = "#ENTER_YOUR_OWN#";
    String api_secret = "#ENTER_YOUR_OWN#";
    GroupMessage coolsms = new GroupMessage(api_key, api_secret);

    // group_id, message_ids are mandatory.
    String group_id = "GID56FA3B1BF0826"; // Group ID	

    try {
      JSONObject obj = (JSONObject) coolsms.sendGroupMessage(group_id);
      System.out.println(obj.toString());
    } catch (CoolsmsException e) {
      System.out.println(e.getMessage());
      System.out.println(e.getCode());
    }
  }
}
```

