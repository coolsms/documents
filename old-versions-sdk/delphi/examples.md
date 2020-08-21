# Examples

Coolsms REST-API SDK Delphi 예제파일은 다운받으신 delphi-sdk example 폴더에 들어있습니다.

## 문자관련

### SMS발송

uses에 coolsms.pas를 적용 시켜준뒤 setApiKey를 통해 api\_key와 api\_secret를 설정해 준 뒤 data에 전송정보들을 넣어서 postRequest\('send', data, 'sms'\)로 전송요청을 합니다.

uses

  System.Json, coolsms in '..\..\coolsms.pas', https in '..\..\https.pas', System.SysUtils, Classes;

var

  coolsms: resource;

  jsonObject: TJSONObject;

  data: TStringList;

begin

  try

    // api\_key, api\_secret 설정

    coolsms := resource.Create\('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74'\);

    // parameters

    data := TStringList.create;

    data.Values\['to'\] := '01000000000'; // 수신번호    

    **\*** **10월 16일 이후로 발신번호 사전등록제로 인해 등록된 발신번호로만 문자를 보내실 수 있습니다.** [**바로가기** ](https://developer.coolsms.co.kr/SDK_Delphi_ko)   

    data.Values\['from'\] := '029302266'; // 발신번호    

    data.Values\['text'\] := 'test'; // 문자내용    

    data.Values\['type'\] := 'mms';  // 문자타입 sms, mms, lms    

    data.Values\['image'\] := '..\..\test.jpg'; // IMAGE 파일 \(MMS일경우\)

    // 그외 parameters, [https://developer.coolsms.co.kr/SMS\_API\#POSTsend](https://developer.coolsms.co.kr/SMS_API#POSTsend) 참조

    {

      data.Values\['image\_encoding'\]

          이미지 인코딩 방식 binary\(Default\), base64

      data.Values\['refname'\]

          참조내용\(이름\)

      data.Values\['country'\]

        한국: 82, 일본: 81, 중국: 86, 미국: 1, 기타 등등 \(기본 한국\)

        [http://countrycode.org](http://countrycode.org/) 참고

      data.Values\['datetime'\]

          예약시간을 YYYYMMDDHHMISS 포맷으로 입력 \(입력 없거나 지난날짜를 입력하면 바로 전송\) 예\) 20131216090510 \(2013년 12월 16일 9시 5분 10초에 발송되도록 예약\)

      data.Values\['subject'\]

          LMS, MMS 일때 제목 \(40바이트\)

      data.Values\['charset'\]

          한글 인코딩 방식 지정 유니코드 UTF-8 일 경우 utf8 완성형 한글\(EUC-KR\) 일 경우 euckr 으로 입력 입력 없으면 utf8가 기본

      data.Values\['srk'\]

          솔루션 제공 수수료를 정산받을 솔루션 등록키

      data.Values\['mode'\]

          test로 입력할 경우 CARRIER 시뮬레이터로 시뮬레이션됨 수신번호를 반드시 01000000000 으로 테스트하세요. 예약필드 datetime는 무시됨 결과값은 60 잔액에서 실제 차감되며 다음날 새벽에 재충전됨

      data.Values\['delay'\]

          0~20 사이의 값으로 전송지연 시간을 줄 수 있음, 1은 약 1초 \(기본값은 0\)

      data.Values\['force\_sms'\]

        누리고푸시를 사용하더라도 SMS로 발송되도록 강제

        true 혹은 false\(기본\)

      data.Values\['os\_platform'\]

        클라이언트의 OS 및 플랫폼 버전\) CentOS 6.6

        \(v1.5에서 추가됨\)

      data.Values\['dev\_lang'\]

        개발 프로그래밍 언어 예\) PHP 5.3.3

        \(v1.5에서 추가됨\)

      data.Values\['sdk\_version'\]

        SDK 버전 예\) PHP SDK 1.5

        \(v1.5에서 추가됨\)

      data.Values\['app\_version'\]

        어플리케이션 버전 예\) Purplebook 4.1

        \(v1.5에서 추가됨\)

      data.Values\['extension'\]

          JSON 포맷의 개별 메시지를 담을 수 있음

    }

    // send Messages

    jsonObject := coolsms.send\(data\);

    if strToBool\(jsonObject.GetValue\('status'\).ToString\) = TRUE then

    begin

      Writeln\('성공'\);

      Writeln\('group\_id : ' + jsonObject.Get\('group\_id'\).JsonValue.ToString\);

      Writeln\('success\_count : ' + jsonObject.Get\('success\_count'\).JsonValue.ToString\);

      Writeln\('error\_count : ' + jsonObject.Get\('error\_count'\).JsonValue.ToString\);

      Writeln\('result\_code : ' + jsonObject.Get\('result\_code'\).JsonValue.ToString\);

      Writeln\('result\_message : ' + jsonObject.Get\('result\_message'\).JsonValue.ToString\);

    end

    else

    begin

      Writeln\('실패'\);

      if jsonObject.Get\('code'\).Equals\(Nil\) = FALSE then Writeln\('code : ' + jsonObject.Get\('code'\).JsonValue.ToString\);

      if jsonObject.Get\('message'\).Equals\(Nil\) = FALSE then Writeln\('message : ' + jsonObject.Get\('message'\).JsonValue.ToString\);

    end;

    jsonObject.Free;

    Writeln\('-----------------------------------------'\);

    Writeln\('Press &lt;enter&gt; to quit...'\);

    Readln;

  except

    on E: Exception do

      Writeln\(E.ClassName, ': ', E.Message\);

  end;

end.

### SMS발송\(개별\)

SMS발송\(개별\)은 여러명의 사용자에게 각가 다른 내용이 들어간 문자를 보내고 싶을때 사용합니다.

TStringlist data에 각각의 TJSONObject들이 들어간 TJSONArray를 ToString으로 parameter extension에 넣어주시면됩니다.

uses  
  System.Json, coolsms in '..\..\coolsms.pas', https in '..\..\https.pas', System.SysUtils, Classes;

var  
  coolsms: resource;  
  jsonObject: TJSONObject;  
  extensionObject: TJSONObject;  
  extensionArray: TJSONArray;  
  data: TStringList;

begin  
  try  
    // api\_key, api\_secret 설정  
    coolsms := resource.Create\('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74'\);

    // 개별 메시지 보내기  
    extensionObject := TJSONObject.Create;  
    extensionArray := TJSONArray.Create;

    // message 1 parameters  
    extensionObject.AddPair\('type', 'sms'\);  
    extensionObject.AddPair\('to', '01000000003'\);  
    extensionObject.AddPair\('text', 'sms\_test'\);  
    extensionArray.Add\(extensionObject\);

    // message 2 parameters  
    extensionObject := TJSONObject.Create;  
    extensionObject.AddPair\('type', 'sms'\);  
    extensionObject.AddPair\('to', '01000000000, 010000000001'\);  
    extensionObject.AddPair\('text', 'sms\_test2'\);  
    extensionArray.Add\(extensionObject\);

    // input extension\_data into string\_list  
    data := TStringList.create;  
    data.Values\['extension'\] := extensionArray.ToString;   

    **\*** **10월 16일 이후로 발신번호 사전등록제로 인해 등록된 발신번호로만 문자를 보내실 수 있습니다.** [**바로가기** ](https://developer.coolsms.co.kr/SDK_Delphi_ko)   

    data.Values\['from'\] := '029302266'; // 발신번호

    // send Messages  
    jsonObject := coolsms.send\(data\);  
    if strToBool\(jsonObject.GetValue\('status'\).ToString\) = TRUE then  
    begin  
      Writeln\('성공'\);  
      Writeln\('group\_id : ' + jsonObject.Get\('group\_id'\).JsonValue.ToString\);  
      Writeln\('success\_count : ' + jsonObject.Get\('success\_count'\).JsonValue.ToString\);  
      Writeln\('error\_count : ' + jsonObject.Get\('error\_count'\).JsonValue.ToString\);  
      Writeln\('result\_code : ' + jsonObject.Get\('result\_code'\).JsonValue.ToString\);  
      Writeln\('result\_message : ' + jsonObject.Get\('result\_message'\).JsonValue.ToString\);  
    end  
    else  
    begin  
      Writeln\('실패'\);  
      if jsonObject.Get\('code'\).Equals\(Nil\) = FALSE then Writeln\('code : ' + jsonObject.Get\('code'\).JsonValue.ToString\);  
      if jsonObject.Get\('message'\).Equals\(Nil\) = FALSE then Writeln\('message : ' + jsonObject.Get\('message'\).JsonValue.ToString\);  
    end;

    jsonObject.Free;

    Writeln\('-----------------------------------------'\);  
    Writeln\('Press &lt;enter&gt; to quit...'\);  
    Readln;  
  except  
    on E: Exception do  
      Writeln\(E.ClassName, ': ', E.Message\);  
  end;  
end.

### LMS발송

type 을 lms로 바꿔주시기만하면됩니다.

uses

  System.Json, coolsms in '..\..\coolsms.pas', https in '..\..\https.pas', System.SysUtils, Classes;

var

  coolsms: resource;

  jsonObject: TJSONObject;

  data: TStringList;

begin

  try

    // api\_key, api\_secret 설정

    coolsms := resource.Create\('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74'\);

    // parameters

    data := TStringList.create;

    data.Values\['to'\] := '01000000000'; // 수신번호        **\*** **10월 16일 이후로 발신번호 사전등록제로 인해 등록된 발신번호로만 문자를 보내실 수 있습니다.** [**바로가기**](https://developer.coolsms.co.kr/SDK_Delphi_ko)

    data.Values\['from'\] := '029302266'; // 발신번호

    data.Values\['text'\] := 'test'; // 문자내용

    data.Values\['type'\] := 'lms';  // 문자타입 sms, mms, lms

    // send Messages

    jsonObject := coolsms.send\(data\);

    if strToBool\(jsonObject.GetValue\('status'\).ToString\) = TRUE then

    begin

      Writeln\('성공'\);

      Writeln\('group\_id : ' + jsonObject.Get\('group\_id'\).JsonValue.ToString\);

      Writeln\('success\_count : ' + jsonObject.Get\('success\_count'\).JsonValue.ToString\);

      Writeln\('error\_count : ' + jsonObject.Get\('error\_count'\).JsonValue.ToString\);

      Writeln\('result\_code : ' + jsonObject.Get\('result\_code'\).JsonValue.ToString\);

      Writeln\('result\_message : ' + jsonObject.Get\('result\_message'\).JsonValue.ToString\);

    end

    else

    begin

      Writeln\('실패'\);

      if jsonObject.Get\('code'\).Equals\(Nil\) = FALSE then Writeln\('code : ' + jsonObject.Get\('code'\).JsonValue.ToString\);

      if jsonObject.Get\('message'\).Equals\(Nil\) = FALSE then Writeln\('message : ' + jsonObject.Get\('message'\).JsonValue.ToString\);

    end;

    jsonObject.Free;

    Writeln\('-----------------------------------------'\);

    Writeln\('Press &lt;enter&gt; to quit...'\);

    Readln;

  except

    on E: Exception do

      Writeln\(E.ClassName, ': ', E.Message\);

  end;

end.

### MMS발송

type을 mms로 바꿔준뒤 전송할 이미지 파일 정보를 입력합니다. 

uses

  System.Json, coolsms in '..\..\coolsms.pas', https in '..\..\https.pas', System.SysUtils, Classes;

var

  coolsms: resource;

  jsonObject: TJSONObject;

  data: TStringList;

begin

  try

    // api\_key, api\_secret 설정

    coolsms := resource.Create\('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74'\);

    // parameters

    data := TStringList.create;

    data.Values\['to'\] := '01000000000'; // 수신번호    **\*** **10월 16일 이후로 발신번호 사전등록제로 인해 등록된 발신번호로만 문자를 보내실 수 있습니다.** [**바로가기**](https://developer.coolsms.co.kr/SDK_Delphi_ko)

    data.Values\['from'\] := '029302266'; // 발신번호

    data.Values\['text'\] := 'test'; // 문자내용

    data.Values\['type'\] := 'mms';  // 문자타입 sms, mms, lms

    data.Values\['image'\] := '..\..\test.jpg'; // IMAGE 파일 \(MMS일경우\)

    // send Messages

    jsonObject := coolsms.send\(data\);

    if strToBool\(jsonObject.GetValue\('status'\).ToString\) = TRUE then

    begin

      Writeln\('성공'\);

      Writeln\('group\_id : ' + jsonObject.Get\('group\_id'\).JsonValue.ToString\);

      Writeln\('success\_count : ' + jsonObject.Get\('success\_count'\).JsonValue.ToString\);

      Writeln\('error\_count : ' + jsonObject.Get\('error\_count'\).JsonValue.ToString\);

      Writeln\('result\_code : ' + jsonObject.Get\('result\_code'\).JsonValue.ToString\);

      Writeln\('result\_message : ' + jsonObject.Get\('result\_message'\).JsonValue.ToString\);

    end

    else

    begin

      Writeln\('실패'\);

      if jsonObject.Get\('code'\).Equals\(Nil\) = FALSE then Writeln\('code : ' + jsonObject.Get\('code'\).JsonValue.ToString\);

      if jsonObject.Get\('message'\).Equals\(Nil\) = FALSE then Writeln\('message : ' + jsonObject.Get\('message'\).JsonValue.ToString\);

    end;

    jsonObject.Free;

    Writeln\('-----------------------------------------'\);

    Writeln\('Press &lt;enter&gt; to quit...'\);

    Readln;

  except

    on E: Exception do

      Writeln\(E.ClassName, ': ', E.Message\);

  end;

end.

### 예약발송

data에 datetime을 추가해주시면 됩니다.

uses

  System.Json, coolsms in '..\..\coolsms.pas', https in '..\..\https.pas', System.SysUtils, Classes;

var

  coolsms: resource;

  jsonObject: TJSONObject;

  data: TStringList;

begin

  try

    // api\_key, api\_secret 설정

    coolsms := resource.Create\('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74'\);

    // parameters

    data := TStringList.create;

    data.Values\['to'\] := '01000000000'; // 수신번호    **\*** **10월 16일 이후로 발신번호 사전등록제로 인해 등록된 발신번호로만 문자를 보내실 수 있습니다.** [**바로가기**](https://developer.coolsms.co.kr/SDK_Delphi_ko)

    data.Values\['from'\] := '029302266'; // 발신번호

    data.Values\['text'\] := 'test'; // 문자내용

    data.Values\['datetime'\] := '20131216090510'; // 예약시간을 YYYYMMDDHHMISS 포맷으로 입력 \(입력 없거나 지난날짜를 입력하면 바로 전송\) 예\) 20131216090510 \(2013년 12월 16일 9시 5분 10초에 발송되도록 예약\)

    // send Messages

    jsonObject := coolsms.send\(data\);

    if strToBool\(jsonObject.GetValue\('status'\).ToString\) = TRUE then

    begin

      Writeln\('성공'\);

      Writeln\('group\_id : ' + jsonObject.Get\('group\_id'\).JsonValue.ToString\);

      Writeln\('success\_count : ' + jsonObject.Get\('success\_count'\).JsonValue.ToString\);

      Writeln\('error\_count : ' + jsonObject.Get\('error\_count'\).JsonValue.ToString\);

      Writeln\('result\_code : ' + jsonObject.Get\('result\_code'\).JsonValue.ToString\);

      Writeln\('result\_message : ' + jsonObject.Get\('result\_message'\).JsonValue.ToString\);

    end

    else

    begin

      Writeln\('실패'\);

      if jsonObject.Get\('code'\).Equals\(Nil\) = FALSE then Writeln\('code : ' + jsonObject.Get\('code'\).JsonValue.ToString\);

      if jsonObject.Get\('message'\).Equals\(Nil\) = FALSE then Writeln\('message : ' + jsonObject.Get\('message'\).JsonValue.ToString\);

    end;

    jsonObject.Free;

    Writeln\('-----------------------------------------'\);

    Writeln\('Press &lt;enter&gt; to quit...'\);

    Readln;

  except

    on E: Exception do

      Writeln\(E.ClassName, ': ', E.Message\);

  end;

end.

### 예약취소

data에 mid나 gid를 입력하신뒤 postRequest\('cancel', data, 'sms'\)를 호출합니다.

uses  
  System.Json, coolsms in '..\..\coolsms.pas', https in '..\..\https.pas', System.SysUtils, Classes;

var  
  coolsms: resource;  
  jsonObject: TJSONObject;  
  data: TStringList;

begin  
  try  
    // api\_key, api\_secret 설정  
    coolsms := resource.Create\('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74'\);

    // parameters, [http://www.coolsms.co.kr/SMS\_API\#POSTcancel](http://www.coolsms.co.kr/SMS_API#POSTcancel) 참조  
    data := TStringList.create;  
    data.Values\['mid'\] := 'R1M55D585C2CE9E9'; // 메시지ID  
    // data.Values\['gid'\] := ''; // 그룹ID

    // 예약취소 요청  
    jsonObject := coolsms.cancel\(data\);  
    if strToBool\(jsonObject.GetValue\('status'\).ToString\) = TRUE then  
    begin  
      Writeln\('성공'\);  
    end  
    else  
    begin  
      Writeln\('실패'\);  
      if jsonObject.Get\('code'\).Equals\(Nil\) = FALSE then Writeln\('code : ' + jsonObject.Get\('code'\).JsonValue.ToString\);  
      if jsonObject.Get\('message'\).Equals\(Nil\) = FALSE then Writeln\('message : ' + jsonObject.Get\('message'\).JsonValue.ToString\);  
    end;

    jsonObject.Free;

    Writeln\('-----------------------------------------'\);  
    Writeln\('Press &lt;enter&gt; to quit...'\);  
    Readln;  
  except  
    on E: Exception do  
      Writeln\(E.ClassName, ': ', E.Message\);  
  end;  
end.

### 발송내역

data에 mid나 gid를 입력하신후 request\('sent', data, 'sms'\)를 통해 발송내역을 가져옵니다.

Return 값은 jsonObject 안에 jsonArray로 받습니다.

uses  
  System.Json, coolsms in '..\..\coolsms.pas', https in '..\..\https.pas', System.SysUtils, Classes;

var  
  coolsms: resource;  
  data: TStringList;  
  jsonObject: TJSONObject;  
  jsonArray: TJSONArray;  
  jsonObjectData: TJSONObject;  
  i: integer;

begin  
  try  
    // api\_key, api\_secret 설정  
    coolsms := resource.Create\('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74'\);  
    //https.create\('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74'\);

    // parameters, data 설정 mid나 gid 둘 중 하나는 들어가야 합니다.  
    data := TStringList.create;  
    data.Values\['mid'\] := 'R1M55B1FFB27E5308'; // 메시지ID

    // 그외 parameters, [http://www.https.co.kr/SMS\_API\#GETsent](http://www.https.co.kr/SMS_API#GETsent) 참조  
    {  
        data.Values\['count'\]  
          기본값 20이며 20개의 목록을 받을 수 있음. 40입력시 40개의 목록이 리턴  
      data.Values\['page'\]  
          1부터 시작하는 페이지값  
      data.Values\['rcpt'\]  
          수신번호로 검색  
      data.Values\['start'\]  
          검색 시작일시 접수 날짜와 시간으로 검색 YYYY-MM-DD HH:MI:SS 포맷의 날짜와 시간  
      data.Values\['end'\]  
          검색 종료일시 접수 날짜와 시간으로 검색 YYYY-MM-DD HH:MI:SS 포맷의 날짜와 시간  
      data.Values\['status'\]  
          메시지 상태 값으로 검색  
      data.Values\['resultcode'\]  
          전송결과 값으로 검색  
      data.Values\['notin\_resultcode'\]  
          입력된 전송결과 값 이외의 건들만 조회  
      data.Values\['gid'\]  
          그룹ID  
    }

    // sent Messages  
    jsonObject := coolsms.sent\(data\);  
    if strToBool\(jsonObject.GetValue\('status'\).ToString\) = TRUE then  
    begin  
      Writeln\('성공'\);  
      jsonArray := JsonObject.Get\('data'\).JsonValue as TJSONArray;

      Writeln\('total\_count : ' + jsonObject.Get\('total\_count'\).JsonValue.ToString\);  
      Writeln\('list\_count : ' + jsonObject.Get\('list\_count'\).JsonValue.ToString\);  
      Writeln\('page : ' + jsonObject.Get\('page'\).JsonValue.ToString\);

      for i := 0 to jsonArray.Size - 1 do  
      begin  
          jsonObjectData := TJSONObject.Create;  
          jsonObjectData := jsonArray.Get\(i\) as TJSONObject;

          Writeln\('-----------------------------------------'\);  
          Writeln\('type : ' + jsonObjectData.Get\('type'\).JsonValue.ToString\);  
          Writeln\('recipient\_number : ' + jsonObjectData.Get\('recipient\_number'\).JsonValue.ToString\);  
          Writeln\('text : ' + jsonObjectData.Get\('text'\).JsonValue.ToString\);  
          Writeln\('carrier : ' + jsonObjectData.Get\('carrier'\).JsonValue.ToString\);  
          Writeln\('status : ' + jsonObjectData.Get\('status'\).JsonValue.ToString\);  
          Writeln\('result\_code : ' + jsonObjectData.Get\('result\_code'\).JsonValue.ToString\);  
          Writeln\('result\_message : ' + jsonObjectData.Get\('result\_message'\).JsonValue.ToString\);  
          Writeln\('message\_id : ' + jsonObjectData.Get\('message\_id'\).JsonValue.ToString\);  
          Writeln\('group\_id : ' + jsonObjectData.Get\('group\_id'\).JsonValue.ToString\);  
          Writeln\('sent\_time : ' + jsonObjectData.Get\('sent\_time'\).JsonValue.ToString\);  
          Writeln\('accepted\_time : ' + jsonObjectData.Get\('accepted\_time'\).JsonValue.ToString\);  
      end;  
    end  
    else  
    begin  
      Writeln\('실패'\);  
      if jsonObject.Get\('code'\).Equals\(Nil\) = FALSE then Writeln\('code : ' + jsonObject.Get\('code'\).JsonValue.ToString\);  
      if jsonObject.Get\('message'\).Equals\(Nil\) = FALSE then Writeln\('message : ' + jsonObject.Get\('message'\).JsonValue.ToString\);  
    end;

    jsonObject.Free;

    Writeln\('-----------------------------------------'\);  
    Writeln\('Press &lt;enter&gt; to quit...'\);  
    Readln;  
  except  
    on E: Exception do  
      Writeln\(E.ClassName, ': ', E.Message\);  
  end;  
end.

### 잔액정보

request\('balance', Nil, 'sms'\)를 통해 잔액정보를 가져옵니다.

uses  
  System.Json, coolsms in '..\..\coolsms.pas', https in '..\..\https.pas', System.SysUtils;

var  
  coolsms: resource;  
  jsonObject: TJSONObject;

begin  
  try  
    // api\_key, api\_secret 설정  
    coolsms := resource.Create\('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74'\);

    // 남은잔액 요청, [http://www.coolsms.co.kr/SMS\_API\#GETbalance](http://www.coolsms.co.kr/SMS_API#GETbalance) 참조  
    jsonObject := coolsms.balance\(\);  
    if strToBool\(jsonObject.GetValue\('status'\).ToString\) = TRUE then  
    begin  
      Writeln\('성공'\);  
      Writeln\('cash : ' + jsonObject.Get\('cash'\).JsonValue.ToString\);  
      Writeln\('point : ' + jsonObject.Get\('point'\).JsonValue.ToString\);  
    end  
    else  
    begin  
      Writeln\('실패'\);  
      if jsonObject.Get\('code'\).Equals\(Nil\) = FALSE then Writeln\('code : ' + jsonObject.Get\('code'\).JsonValue.ToString\);  
      if jsonObject.Get\('message'\).Equals\(Nil\) = FALSE then Writeln\('message : ' + jsonObject.Get\('message'\).JsonValue.ToString\);  
    end;

    jsonObject.Free;

    Writeln\('-----------------------------------------'\);  
    Writeln\('Press &lt;enter&gt; to quit...'\);  
    Readln;  
  except  
    on E: Exception do  
      Writeln\(E.ClassName, ': ', E.Message\);  
  end;  
end.

## 발신번호등록

### 발신번호 등록 요청

\* 보안상 문제로 현재는 제공하지 않습니다. 쿨에스엠에스 사이트에서 발신번호를 등록해 주세요

관련 정보는 [http://www.coolsms.co.kr/SenderID\_API](http://www.coolsms.co.kr/SenderID_API)를 참고해주세요.

postRequest\('register', data, 'senderid'\)로 요청을 해서 넘어오는 ars\_number로 전화를 걸어주시면 됩니다.

uses  
  System.Json, coolsms in '..\..\coolsms.pas', https in '..\..\https.pas', System.SysUtils, Classes;

var  
  coolsms: resource;  
  data: TStringList;  
  jsonObject: TJSONObject;

begin  
  try  
    // [http://www.coolsms.co.kr/SenderID\_API\#POSTregister](http://www.coolsms.co.kr/SenderID_API#POSTregister) 참조

    // api\_key, api\_secret 설정  
    coolsms := resource.Create\('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74'\);

    // parameters  
    data := TStringList.create;  
    data.Values\['phone'\] := '01090683469'; // 발신번호로 등록할 전화번호를 입력해주세요.

    // 발신번호등록 요청  
    jsonObject := coolsms.register\(data\);  
    if strToBool\(jsonObject.GetValue\('status'\).ToString\) = TRUE then  
    begin  
      Writeln\('성공'\);  
      Writeln\('handle\_key : ' + jsonObject.Get\('handle\_key'\).JsonValue.ToString\);  
      Writeln\('ars\_number : ' + jsonObject.Get\('ars\_number'\).JsonValue.ToString\);  
    end  
    else  
    begin  
      Writeln\('실패'\);  
      if jsonObject.Get\('code'\).Equals\(Nil\) = FALSE then Writeln\('code : ' + jsonObject.Get\('code'\).JsonValue.ToString\);  
      if jsonObject.Get\('message'\).Equals\(Nil\) = FALSE then Writeln\('message : ' + jsonObject.Get\('message'\).JsonValue.ToString\);  
    end;

    jsonObject.Free;

    Writeln\('-----------------------------------------'\);  
    Writeln\('Press &lt;enter&gt; to quit...'\);  
    Readln;  
  except  
    on E: Exception do  
      Writeln\(E.ClassName, ': ', E.Message\);  
  end;  
end.

### 발신번호 등록 확인

\* 보안상 문제로 현재는 제공하지 않습니다. 쿨에스엠에스 사이트에서 발신번호를 등록해 주세요

register에서 받은 ars\_number로 전화를 거신후 handle\_key로 postRequest\('verify', data, 'senderid'\)를 호출하시면 발신번호 등록이 완료됩니다.

uses  
  System.Json, coolsms in '..\..\coolsms.pas', https in '..\..\https.pas', System.SysUtils, Classes;

var  
  coolsms: resource;  
  data: TStringList;  
  jsonObject: TJSONObject;

begin  
  try  
    // [http://www.coolsms.co.kr/SenderID\_API\#POSTverify](http://www.coolsms.co.kr/SenderID_API#POSTverify) 참조

    // api\_key, api\_secret 설정  
    coolsms := resource.Create\('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74'\);

    // parameters  
    data := TStringList.create;  
    data.Values\['handle\_key'\] := 'SID5FFFF7614ED3'; // register 호출 후 리턴받은 핸들값

    // 발신번호등록확인 요청  
    jsonObject := coolsms.verify\(data\);  
    if strToBool\(jsonObject.GetValue\('status'\).ToString\) = TRUE then  
    begin  
      Writeln\('성공'\);  
    end  
    else  
    begin  
      Writeln\('실패'\);  
      if jsonObject.Get\('code'\).Equals\(Nil\) = FALSE then Writeln\('code : ' + jsonObject.Get\('code'\).JsonValue.ToString\);  
      if jsonObject.Get\('message'\).Equals\(Nil\) = FALSE then Writeln\('message : ' + jsonObject.Get\('message'\).JsonValue.ToString\);  
    end;

    jsonObject.Free;

    Writeln\('-----------------------------------------'\);  
    Writeln\('Press &lt;enter&gt; to quit...'\);  
    Readln;  
  except  
    on E: Exception do  
      Writeln\(E.ClassName, ': ', E.Message\);  
  end;  
end.

### 발신번호 삭제

data에 해당 발신번호릐 handle\_key를 입력하시고 postRequest\('delete', data, 'sendid'\)를 호출하시면 됩니다.

uses  
  System.Json, coolsms in '..\..\coolsms.pas', https in '..\..\https.pas', System.SysUtils, Classes;

var  
  coolsms: resource;  
  data: TStringList;  
  jsonObject: TJSONObject;

begin  
  try  
    // [http://www.coolsms.co.kr/SenderID\_API\#POSTdelete](http://www.coolsms.co.kr/SenderID_API#POSTdelete) 참조

    // api\_key, api\_secret 설정  
    coolsms := resource.Create\('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74'\);

    // parameters  
    data := TStringList.create;  
    data.Values\['handle\_key'\] := 'SFFFFFFF7E1D7'; // 삭제할 발신번호의 handle\_key

    // 발신번호삭제 요청  
    jsonObject := coolsms.delete\(data\);  
    if strToBool\(jsonObject.GetValue\('status'\).ToString\) = TRUE then  
    begin  
      Writeln\('성공'\);  
    end  
    else  
    begin  
      Writeln\('실패'\);  
      if jsonObject.Get\('code'\).Equals\(Nil\) = FALSE then Writeln\('code : ' + jsonObject.Get\('code'\).JsonValue.ToString\);  
      if jsonObject.Get\('message'\).Equals\(Nil\) = FALSE then Writeln\('message : ' + jsonObject.Get\('message'\).JsonValue.ToString\);  
    end;

    jsonObject.Free;

    Writeln\('-----------------------------------------'\);  
    Writeln\('Press &lt;enter&gt; to quit...'\);  
    Readln;  
  except  
    on E: Exception do  
      Writeln\(E.ClassName, ': ', E.Message\);  
  end;  
end.

### 발신번호 목록 보기

request\('list', Nil, 'senderid'\)를 요청하시면 됩니다.

Return값은 jsonObject안에 jsonArray로 처리해주세요.

uses  
  System.Json, coolsms in '..\..\coolsms.pas', https in '..\..\https.pas', System.SysUtils, Classes;

var  
  coolsms: resource;  
  data: TStringList;  
  jsonObject: TJSONObject;  
  jsonArray: TJSONArray;  
  jsonObjectData: TJSONObject;  
  i: integer;

begin  
  try  
    // [http://www.coolsms.co.kr/SenderID\_API\#GETlist](http://www.coolsms.co.kr/SenderID_API#GETlist) 참조

    // api\_key, api\_secret 설정  
    coolsms := resource.Create\('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74'\);

    // 발신번호 리스트 요청  
    jsonObject := coolsms.list\(\);

    if strToBool\(jsonObject.GetValue\('status'\).ToString\) = TRUE then  
    begin  
      Writeln\('성공'\);  
      jsonArray := JsonObject.Get\('data'\).JsonValue as TJSONArray;  
      for i := 0 to jsonArray.Size - 1 do  
      begin  
          jsonObjectData := TJSONObject.Create;  
          jsonObjectData := jsonArray.Get\(i\) as TJSONObject;

          Writeln\('-----------------------------------------'\);  
          Writeln\('idno : ' + jsonObjectData.Get\('idno'\).JsonValue.ToString\);  
          Writeln\('phone\_number : ' + jsonObjectData.Get\('phone\_number'\).JsonValue.ToString\);  
          Writeln\('flag\_default : ' + jsonObjectData.Get\('flag\_default'\).JsonValue.ToString\);  
          Writeln\('updatetime : ' + jsonObjectData.Get\('updatetime'\).JsonValue.ToString\);  
          Writeln\('regdate : ' + jsonObjectData.Get\('regdate'\).JsonValue.ToString\);  
      end;  
    end  
    else  
    begin  
      Writeln\('실패'\);  
      if jsonObject.Get\('code'\).Equals\(Nil\) = FALSE then Writeln\('code : ' + jsonObject.Get\('code'\).JsonValue.ToString\);  
      if jsonObject.Get\('message'\).Equals\(Nil\) = FALSE then Writeln\('message : ' + jsonObject.Get\('message'\).JsonValue.ToString\);  
    end;

    jsonObject.Free;

  
    Writeln\('-----------------------------------------'\);  
    Writeln\('Press &lt;enter&gt; to quit...'\);  
    Readln;  
  except  
    on E: Exception do  
      Writeln\(E.ClassName, ': ', E.Message\);  
  end;  
end.

### 기본 발신번호 설정

해당 발신번호의 handle\_key를 data에 넣으신후 postRequest\('set\_default', data, 'senderid'\)를 요청하시면 됩니다.

uses  
  System.Json, coolsms in '..\..\coolsms.pas', https in '..\..\https.pas', System.SysUtils, Classes;

var  
  coolsms: resource;  
  data: TStringList;  
  jsonObject: TJSONObject;

begin  
  try  
    // [http://www.coolsms.co.kr/SenderID\_API\#POSTset\_default](http://www.coolsms.co.kr/SenderID_API#POSTset_default) 참조

    // api\_key, api\_secret 설정  
    coolsms := resource.Create\('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74'\);

    // parameters  
    data := TStringList.create;  
    data.Values\['handle\_key'\] := 'SIDFFFFF614ED3'; // register 호출 후 리턴받은 핸들값

    // default 발신번호등록 요청  
    jsonObject := coolsms.setDefault\(data\);  
    if strToBool\(jsonObject.GetValue\('status'\).ToString\) = TRUE then  
    begin  
      Writeln\('성공'\);  
    end  
    else  
    begin  
      Writeln\('실패'\);  
      if jsonObject.Get\('code'\).Equals\(Nil\) = FALSE then Writeln\('code : ' + jsonObject.Get\('code'\).JsonValue.ToString\);  
      if jsonObject.Get\('message'\).Equals\(Nil\) = FALSE then Writeln\('message : ' + jsonObject.Get\('message'\).JsonValue.ToString\);  
    end;

    jsonObject.Free;

    Writeln\('-----------------------------------------'\);  
    Writeln\('Press &lt;enter&gt; to quit...'\);  
    Readln;  
  except  
    on E: Exception do  
      Writeln\(E.ClassName, ': ', E.Message\);  
  end;  
end.

### 기본 발신번호 보기

request\('get\_default', Nil, 'senderid'\)로 요청하시면 됩니다.

uses  
  System.Json, coolsms in '..\..\coolsms.pas', https in '..\..\https.pas', System.SysUtils, Classes;

var  
  coolsms: resource;  
  data: TStringList;  
  jsonObject: TJSONObject;

begin  
  try  
    // [http://www.coolsms.co.kr/SenderID\_API\#POSTset\_default](http://www.coolsms.co.kr/SenderID_API#POSTset_default) 참조

    // api\_key, api\_secret 설정  
    coolsms := resource.Create\('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74'\);

    // default 발신번호 요청  
    jsonObject := coolsms.getDefault\(\);  
    if strToBool\(jsonObject.GetValue\('status'\).ToString\) = TRUE then  
    begin  
      Writeln\('성공'\);  
      Writeln\('handle\_key : ' + jsonObject.Get\('handle\_key'\).JsonValue.ToString\);  
      Writeln\('phone\_number : ' + jsonObject.Get\('phone\_number'\).JsonValue.ToString\);  
    end  
    else  
    begin  
      Writeln\('실패'\);  
      if jsonObject.Get\('code'\).Equals\(Nil\) = FALSE then Writeln\('code : ' + jsonObject.Get\('code'\).JsonValue.ToString\);  
      if jsonObject.Get\('message'\).Equals\(Nil\) = FALSE then Writeln\('message : ' + jsonObject.Get\('message'\).JsonValue.ToString\);  
    end;

    jsonObject.Free;

    Writeln\('-----------------------------------------'\);  
    Writeln\('Press &lt;enter&gt; to quit...'\);  
    Readln;  
  except  
    on E: Exception do  
      Writeln\(E.ClassName, ': ', E.Message\);  
  end;  
end.

