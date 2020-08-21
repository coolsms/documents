# Examples



Coolsms REST-API SDK JAVA 예제파일은 다운받으신 SDK JAVA 폴더에 들어있습니다.

## 사용방법

REST-API SDK JAVA 는 Coolsms.java를 이용해 문자발송, 발송내역, 잔액정보등을 서버에 요청합니다.  
서버로부터 온 Return값은 jsonObject이며 status가 true면 성공입니다.  
아래 예제들을 보시면 이해가 더 쉬울 것 입니다.

## 문자예제

- 아래는 SMS 관련 예제입니다.

### SMS발송

HashMap set에 받는사람번호, 보내는사람번호, 문자내용 등 을 저장한뒤 Coolsms클래스의 send를 이용해 보냅니다.

```text
public class SendExample {
    public static void main(String[] args) {    
        /*
         * 서버에서 받은 API_KEY, API_SECRET를 입력해주세요.
         */
        String api_key = "NS52A122851C04F";
        String api_secret = "8B2A5A6923C9BE081920A085BFB835A";
        Coolsms coolsms = new Coolsms(api_key, api_secret);
    
        /*
         * Parameters
         * 관련정보 : http://www.coolsms.co.kr/SDK_Java_API_Reference_ko#toc-0
         */
        HashMap<String, String> set = new HashMap<String, String>();
        set.put("to", "01000000000"); // 수신번호
        
       * 10월 16일 이후로 발신번호 사전등록제로 인해 등록된 발신번호로만 문자를 보내실 수 있습니다. 바로가기
        set.put("from", "029302266"); // 발신번호 
        set.put("text", "Test Message"); // 문자내용
        set.put("type", "sms"); // 문자 타입

        
        JSONObject result = coolsms.send(set); // 보내기&전송결과받기
        if (result.get("status") == true) {
            // 메시지 보내기 성공 및 전송결과 출력
            System.out.println("성공");            
            System.out.println(result.get("group_id")); // 그룹아이디
            System.out.println(result.get("result_code")); // 결과코드
            System.out.println(result.get("result_message"));  // 결과 메시지
            System.out.println(result.get("success_count")); // 메시지아이디
            System.out.println(result.get("error_count"));  // 여러개 보낼시 오류난 메시지 수
        } else {
            // 메시지 보내기 실패
            System.out.println("실패");
            System.out.println(result.get("code")); // REST API 에러코드
            System.out.println(result.get("message")); // 에러메시지
        }        
    }    
}
```

### SMS발송\(개별\)

SMS발송\(개별\)은 여러명의 사용자에게 각가 다른 내용이 들어간 문자를 보내고 싶을때 사용합니다.

HashMap set에 각각의 JSONObject들이 들어간 JSONArray를 toString으로 parameter extension에 넣어주시면됩니다.

```text
public class SendExtensionExample {
    public static void main(String[] args) {    
        /*
         * 서버에서 받은 API_KEY, API_SECRET를 입력해주세요.
         */
        String api_key = "CS3588FB7DE511A";
        String api_secret = "FB5FF8B9AB7D0E0AEB840D403DE0F74";
        Coolsms coolsms = new Coolsms(api_key, api_secret);

    
        /*
         * Parameters
         * 관련정보 : http://www.coolsms.co.kr/SDK_Java_API_Reference_ko#toc-0
         */
        HashMap<String, String> set = new HashMap<String, String>(); 
        JSONObject obj = new JSONObject();
        JSONArray list = new JSONArray();       
        
        obj.put("type", "sms"); // 문자타입
        obj.put("to", "01000000000, 01000000001"); // 받는사람번호
        obj.put("text", "Test Message"); // 문자내용        

        list.add(obj); // 원하는 만큼 obj를 넣어주면 됩니다.        
        set.put("extension", list.toString()); // set extension   


       * 10월 16일 이후로 발신번호 사전등록제로 인해 등록된 발신번호로만 문자를 보내실 수 있습니다. 바로가기        
        set.put("from", "029302266"); // 발신번호     

        JSONObject result = coolsms.send(set); // 보내기&전송결과받기

        if ((Boolean) result.get("status") == true) {
            // 메시지 보내기 성공 및 전송결과 출력
            System.out.println("성공");            
            System.out.println(result.get("group_id")); // 그룹아이디
            System.out.println(result.get("result_code")); // 결과코드
            System.out.println(result.get("result_message"));  // 결과메시지
            System.out.println(result.get("success_count")); // 성공갯수
            System.out.println(result.get("error_count"));  // 발송실패 메시지 수
        } else {
            // 메시지 보내기 실패
            System.out.println("실패");
            System.out.println(result.get("code")); // REST API 에러코드
            System.out.println(result.get("message")); // 에러메시지
        }        
    }    
}
```

### LMS발송

set.put\("type"\) 을 LMS로 바꿔주시기만하면됩니다.

```text
public class SendExample {
    public static void main(String[] args) {    
        /*
         * 서버에서 받은 API_KEY, API_SECRET를 입력해주세요.
         */
        String api_key = "NCS52A122851C04F";
        String api_secret = "8B2AE5A6923C9BE081920A085BFB835A";
        Coolsms coolsms = new Coolsms(api_key, api_secret);
    
        /*
         * Parameters
         * 관련정보 : http://www.coolsms.co.kr/SDK_Java_API_Reference_ko#toc-0
         */
        HashMap<String, String> set = new HashMap<String, String>();
        set.put("to", "01000000000"); // 수신번호

       * 10월 16일 이후로 발신번호 사전등록제로 인해 등록된 발신번호로만 문자를 보내실 수 있습니다. 바로가기
        set.put("from", "029302266"); // 발신번호
        set.put("text", "Test Message"); // 문자내용
        set.put("type", "lms"); // 문자 타입

        
        JSONObject result = coolsms.send(set); // 보내기&전송결과받기
        if (result.get("status") == true) {
            // 메시지 보내기 성공 및 전송결과 출력
            System.out.println("성공");            
            System.out.println(result.get("group_id")); // 그룹아이디
            System.out.println(result.get("result_code")); // 결과코드
            System.out.println(result.get("result_message"));  // 결과 메시지
            System.out.println(result.get("success_count")); // 메시지아이디
            System.out.println(result.get("error_count"));  // 여러개 보낼시 오류난 메시지 수
        } else {
           // 메시지 보내기 실패
            System.out.println("실패");
            System.out.println(result.get("code")); // REST API 에러코드
            System.out.println(result.get("message")); // 에러메시지
        }        
    }    
}
```

### MMS발송

type을 MMS로 바꿔준뒤 전송할 파일정보를 입력합니다. 

```text
public class SendExample {
    public static void main(String[] args) {    
        /*
         * 서버에서 받은 API_KEY, API_SECRET를 입력해주세요.
         */
        String api_key = "NCS52A122851C04F";
        String api_secret = "8B2AE5A6923C9BE081920A085BFB835A";
        Coolsms coolsms = new Coolsms(api_key, api_secret);
    
        /*
         * Parameters
         * 관련정보 : http://www.coolsms.co.kr/SDK_Java_API_Reference_ko#toc-0
         */
        HashMap<String, String> set = new HashMap<String, String>();
        set.put("to", "01000000000"); // 수신번호        

        * 10월 16일 이후로 발신번호 사전등록제로 인해 등록된 발신번호로만 문자를 보내실 수 있습니다. 바로가기
        set.put("from", "029302266"); // 발신번호
        set.put("text", "Test Message"); // 문자내용
        set.put("type", "mms"); // 문자 타입

        set.put("image_path", "../images/"); // image file path 이미지 파일 경로 설정 (기본 "./")
        set.put("image", "test.jpg"); // image file (지원형식 : 200KB 이하의 JPEG)

        
        JSONObject result = coolsms.send(set); // 보내기&전송결과받기
        if (result.get("status") == true) {
            // 메시지 보내기 성공 및 전송결과 출력
            System.out.println("성공");            
            System.out.println(result.get("group_id")); // 그룹아이디
            System.out.println(result.get("result_code")); // 결과코드
            System.out.println(result.get("result_message"));  // 결과 메시지
            System.out.println(result.get("success_count")); // 메시지아이디
            System.out.println(result.get("error_count"));  // 여러개 보낼시 오류난 메시지 수
        } else {
            // 메시지 보내기 실패
            // 메시지 보내기 실패
            System.out.println("실패");
            System.out.println(result.get("code")); // REST API 에러코드
            System.out.println(result.get("message")); // 에러메시지
        }        
    }    
}
```

### 예약발송

parameter에 datetime을 추가해주시면 됩니다.

```text
public class SendExample {
    public static void main(String[] args) {    
        /*
         * 서버에서 받은 API_KEY, API_SECRET를 입력해주세요.
         */
        String api_key = "NCS52A122851C04F";
        String api_secret = "8B2AE5A6923C9BE081920A085BFB835A";
        Coolsms coolsms = new Coolsms(api_key, api_secret);
    
        /*
         * Parameters
         * 관련정보 : http://www.coolsms.co.kr/SDK_Java_API_Reference_ko#toc-0
         */
        HashMap<String, String> set = new HashMap<String, String>();
        set.put("to", "01000000000"); // 받는사람 번호

        * 10월 16일 이후로 발신번호 사전등록제로 인해 등록된 발신번호로만 문자를 보내실 수 있습니다. 바로가기
        set.put("from", "029302266"); // 보내는사람 번호
        set.put("text", "Test Message"); // 문자내용
        set.put("type", "sms"); // 문자 타입

        set.put("datetime", "201401151230"); // 예약전송시 날짜 설정    

        
        JSONObject result = coolsms.send(set); // 보내기&전송결과받기
        if (result.get("status") == true) {
            // 메시지 보내기 성공 및 전송결과 출력
            System.out.println("성공");            
            System.out.println(result.get("group_id")); // 그룹아이디
            System.out.println(result.get("result_code")); // 결과코드
            System.out.println(result.get("result_message"));  // 결과 메시지
            System.out.println(result.get("success_count")); // 메시지아이디
            System.out.println(result.get("error_count"));  // 여러개 보낼시 오류난 메시지 수
        } else {
            // 메시지 보내기 실패
            System.out.println("실패");
            System.out.println(result.get("code")); // REST API 에러코드
            System.out.println(result.get("message")); // 에러메시지
        }        
    }    
}
```

### 예약취소

```text
HashMap set에 Mid나 Gid를 입력하신뒤 Coolsms클래스의 cancel로 취소할 수 있습니다.


public class CancelExample {
    public static void main(String[] args) {
        /*
         * 서버에서 받은 API_KEY, API_SECRET를 입력해주세요.
         */
        String api_key = "NCS52A122851C04F";
        String api_secret = "8B2AE5A6923C9BE081920A085BFB835A";
        Coolsms coolsms = new Coolsms(api_key, api_secret);

        HashMap<String, String> set = new HashMap<String, String>();
        set.put("mid", "R2M5566B2C01922A"); // message_id
        //set.put("gid", "R2G52F9A0CDB76F8"); //group_id
        
        //message_id나 group_id중 하나는 반드시 입력하셔야 됩니다.
        JSONObject result = coolsms.cancel(set);
        if (result.get("status") == true) {
            System.out.println("예약취소 성공");
        } else {
            System.out.println("예약취소 실패");            
            System.out.println(result.get("code")); // REST API 에러코드
            System.out.println(result.get("message")); // 에러메시지
        }
    }
}
```

### 발송내역

HashMap set에 Mid나 Gid를 입력하신후 Coolsms클래스의 sent를 이용하시면 됩니다.

Return 값은 jsonObject 안에 jsonArray로 받습니다.

```text
public class SentExample {
    public static void main(String[] args) {
        /*
         * 서버에서 받은 API_KEY, API_SECRET를 입력해주세요.
         */
        String api_key = "NCS52B222858B03F";
        String api_secret = "8B2AE5A6926B9AE091910A085BFB835A";
        Coolsms coolsms = new Coolsms(api_key, api_secret);
        
        /*
         * Parameters
         * 관련정보 : http://www.coolsms.co.kr/SDK_Java_API_Reference_ko#toc-1    
         */
        HashMap<String, String> set = new HashMap<String, String>();
        //set.put("mid", "R2M553DD58703AEC");  // message_id 
        set.put("gid", "R1G5564CBC62E9A4"); // group_id
        //set.put("count", "20"); // count
        //set.put("page", "1"); // page
        //set.put("s_rcpt", "01025555544"); // 수신번호
        //set.put("s_start", "2014-01-01 14:10:10"); // 검색 시작 날짜
        //set.put("s_end", "2014-02-01 14:10:10");    //검색 종료 날짜
        
        JSONObject result = coolsms.sent(set);
        if(result.get("status") == true) {
            System.out.println("total_count is = " + result.get("total_count")); // Total Count
            System.out.println("list_count is = " + result.get("list_count")); // List Count
            System.out.println("page is = " + result.get("page")); // Page

            JSONArray data = (JSONArray) result.get("data");
            for (int i = 0; i < data.size(); i++) {
                JSONObject obj = (JSONObject) data.get(i);
                System.out.println("\n=======================================\n");
                System.out.println("SENT 성공");
                System.out.println(obj.get("result_message")); // 결과 메시지
                System.out.println(obj.get("result_code")); // 결과 코드
                System.out.println(obj.get("text")); // 문자내용
                System.out.println(obj.get("status")); // 상태 0:대기중 1:전송완료 2:이통사로부터 리포트 도착
                System.out.println(obj.get("accepted_time")); // 접수시간
                System.out.println(obj.get("sent_time")); // 기지국에서 받는사람한테 보낸시간
                System.out.println(obj.get("group_id")); // Group ID
                System.out.println(obj.get("message_id")); // Message ID
                System.out.println(obj.get("type")); // 메시지 타입 SMS, LMS, MMS
                System.out.println(obj.get("recipient_number")); // 받는사람 번호
            }
        } else {
            System.out.println("SENT 실패");
            System.out.println(result.get("code")); // REST API 에러코드
            System.out.println(result.get("message")); // 에러메시지
        }
    }
}
```

### 잔액정보

Coolsms클래스의 balance를 이용하시면 됩니다.

```text
public class BalanceExample {
    public static void main(String[] args) {
        /*
         * 서버에서 받은 API_KEY, API_SECRET를 입력해주세요.
         */
        String api_key = "NCS52A122851C04F";
        String api_secret = "8B2AE5A6923C9BE081920A085BFB835A";
        Coolsms coolsms = new Coolsms(api_key, api_secret);
        
        JSONObject result = coolsms.balance(); // 잔액정보 가져오기
        if (result.get("status") == true) {
            System.out.println("잔액정보 불러오기 성공");
            System.out.println(result.get("cash")); // 잔여 캐쉬
            System.out.println(result.get("point")); // 잔여 포인트
        } else {
            System.out.println("실패");
            System.out.println(result.get("code")); // REST API 에러코드
            System.out.println(result.get("message")); // 에러메시지
        }        
    }
}
```

## 발신번호예제   

- 아래는 SENDERID\(발신번호\) 관련 예제입니다.

### 발신번호등록요청

\* 보안상 문제로 현재는 제공하지 않습니다. 쿨에스엠에스 사이트에서 발신번호를 등록해 주세요

발신번호 등록 요청을 하는 예제입니다.

coolsms.register를 이용합니다.

```text
public class RegisterExample {

    public static void main(String[] args) {

        /*

         * 서버에서 받은 API_KEY, API_SECRET를 입력해주세요.

         */

        String api_key = "1CS5588FB7DE511A";

        String api_secret = "4FB5FF8B9AB7D0E0AEB840D404DE0F4";

        Coolsms coolsms = new Coolsms(api_key, api_secret);

    

        /*

         * Parameters

         * 관련정보 : http://www.coolsms.co.kr/SenderID_API#POSTregister

         */

        HashMap<String, String> set = new HashMap<String, String>();

        set.put("phone", "01000000000"); // 등록할 발신번호

        

        JSONObject result = coolsms.register(set); // 발신번호 등록요청

        if ((Boolean) result.get("status") == true) {

            // 성공 및 전송결과 출력

            System.out.println("성공");            

            System.out.println(result.toString());

            System.out.println(result.get("handle_key")); // 그룹아이디

            System.out.println(result.get("ars_number")); // 결과코드

        } else {

            // 실패

            System.out.println("실패");

            System.out.println(result.get("code")); // REST API 에러코드

            System.out.println(result.get("message")); // 에러메시지

        }       
 }
```

### 발신번호등록확인

\* 보안상 문제로 현재는 제공하지 않습니다. 쿨에스엠에스 사이트에서 발신번호를 등록해 주세요

발신번호등록요청을 한 후 받은 handle\_key를 가지고 등록확인을 합니다.

전화를 거신 후 등록확인을 해야만 발신번호로 등록이 됩니다.

coolsms.verify를 이용합니다.

```text
public class VerifyExample {

    public static void main(String[] args) {

        /*

         * 서버에서 받은 API_KEY, API_SECRET를 입력해주세요.

         */

        String api_key = "1CS5588FB7DE511A";

        String api_secret = "4FB5FF8B9AB7D0E0AEB840D404DE0F4";

        Coolsms coolsms = new Coolsms(api_key, api_secret);

        /*

         * Parameters

         * 관련정보 : http://www.coolsms.co.kr/SenderID_API#GETget_default

         */

        HashMap<String, String> set = new HashMap<String, String>();

        set.put("handle_key", "SID55D6E62620DED"); // 등록할 발신번호

        

        JSONObject result = coolsms.verify(set); // 발신번호 등록요청

        System.out.println(result.toString());

        if ((Boolean) result.get("status") == true) {

            // 성공 및 전송결과 출력

            System.out.println("성공");            

        } else {

            // 실패

            System.out.println("실패");

            System.out.println(result.get("code")); // REST API 에러코드

            System.out.println(result.get("message")); // 에러메시지

        }        

    }    

}  
```

### 발신번호삭제

handle\_key로 발신번호를 삭제합니다.

coolsms.delete를 이용합니다.

```text
public class DeleteExample {
    public static void main(String[] args) {
        /*
         * 서버에서 받은 API_KEY, API_SECRET를 입력해주세요.
         */
        String api_key = "1CS5588FB7DE511A";
        String api_secret = "4FB5FF8B9AB7D0E0AEB840D404DE0F4";
        Coolsms coolsms = new Coolsms(api_key, api_secret);
    
        /*
         * Parameters
         * 관련정보 : http://www.coolsms.co.kr/SenderID_API#POSTdelete
         */
        HashMap<String, String> set = new HashMap<String, String>();
        set.put("handle_key", "SID55D5877614ED3"); // 등록할 발신번호
        
        JSONObject result = coolsms.delete(set); // 발신번호 등록요청
        if ((Boolean) result.get("status") == true) {
            // 성공 및 전송결과 출력
            System.out.println("성공");            
        } else {
            // 실패
            System.out.println("실패");
            System.out.println(result.get("code")); // REST API 에러코드
            System.out.println(result.get("message")); // 에러메시지
        }        
    }    
}  
```

### 발신번호리스트보기

발신번호리스트를 가져옵니다.

coolsms.list를 이용합니다.

```text
public class ListExample {

    public static void main(String[] args) {

        /*

         * 서버에서 받은 API_KEY, API_SECRET를 입력해주세요.

         */

        String api_key = "1CS5588FB7DE511A";

        String api_secret = "4FB5FF8B9AB7D0E0AEB840D404DE0F4";

        Coolsms coolsms = new Coolsms(api_key, api_secret);


        /*

         * Parameters

         * 관련정보 : http://www.coolsms.co.kr/SenderID_API#GETlist

         */

        JSONObject result = coolsms.list(); // 발신번호 등록요청

        if ((Boolean) result.get("status") == true) {

            // 성공 및 전송결과 출력

            System.out.println("성공");            

            JSONArray data = (JSONArray) result.get("data");

            for (int i = 0; i < data.size(); i++) {

                JSONObject obj = (JSONObject) data.get(i);

                System.out.println("\n=======================================\n");

                System.out.println(obj.get("phone_number")); // 발신번호

                System.out.println(obj.get("idno")); // Handle Key

                System.out.println(obj.get("flag_default")); // 삭제여부

                System.out.println(obj.get("regdate")); // 생성시간

                System.out.println(obj.get("updatetime")); // 업데이트시간

            }

        } else {

            // 실패

            System.out.println("실패");

            System.out.println(result.get("code")); // REST API 에러코드

            System.out.println(result.get("message")); // 에러메시지

        }        

    }    

}
```

### 기본발신번호설정

해당 번호를 기본발신번호로 설정

coolsms.setDefault를 이용합니다.

```text
public class SetDefaultExample {
    public static void main(String[] args) {
        /*
         * 서버에서 받은 API_KEY, API_SECRET를 입력해주세요.
         */
        String api_key = "1CS5588FB7DE511A";
        String api_secret = "4FB5FF8B9AB7D0E0AEB840D404DE0F4";
        Coolsms coolsms = new Coolsms(api_key, api_secret);
    
        /*
         * Parameters
         * 관련정보 : http://www.coolsms.co.kr/SenderID_API#POSTset_default
         */
        HashMap<String, String> set = new HashMap<String, String>();
        set.put("site_user", "hosysy2"); // 등록할 발신번호
        set.put("handle_key", "SID55C4243DADDA2"); // 등록할 발신번호
        
        JSONObject result = coolsms.setDefault(set); // 발신번호 등록요청
        if ((Boolean) result.get("status") == true) {
            // 성공 및 전송결과 출력
            System.out.println("성공");            
        } else {
            // 실패
            System.out.println("실패");
            System.out.println(result.get("code")); // REST API 에러코드
            System.out.println(result.get("message")); // 에러메시지
        }        
    }    
}
```

### 기본발신번호보기

기본발신번호를 가져옵니다.

coolsms.getDefault를 이용합니다.

```text
public class GetDefaultExample {

    public static void main(String[] args) {

        /*

         * 서버에서 받은 API_KEY, API_SECRET를 입력해주세요.

         */

        String api_key = "1CS5588FB7DE511A";

        String api_secret = "4FB5FF8B9AB7D0E0AEB840D404DE0F4";

        Coolsms coolsms = new Coolsms(api_key, api_secret);

        /*

         * Parameters

         * 관련정보 : http://www.coolsms.co.kr/SenderID_API#GETget_default

         */


        JSONObject result = coolsms.getDefault(); // 발신번호 등록요청

        if ((Boolean) result.get("status") == true) {

            // 성공 및 전송결과 출력

            System.out.println("성공");            

            System.out.println(result.get("handle_key"));

            System.out.println(result.get("phone_number"));

        } else {

            // 실패

            System.out.println("실패");

            System.out.println(result.get("code")); // REST API 에러코드

            System.out.println(result.get("message")); // 에러메시지

        }        

    }    

}
```

