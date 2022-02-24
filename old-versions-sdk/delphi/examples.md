# Examples

Coolsms REST-API SDK Delphi 예제파일은 다운받으신 delphi-sdk example 폴더에 들어있습니다.

## 문자관련

### SMS발송

uses에 coolsms.pas를 적용 시켜준뒤 setApiKey를 통해 api\_key와 api\_secret를 설정해 준 뒤 data에 전송정보들을 넣어서 postRequest('send', data, 'sms')로 전송요청을 합니다.

uses

&#x20; System.Json, coolsms in '..\\..\coolsms.pas', https in '..\\..\https.pas', System.SysUtils, Classes;

var

&#x20; coolsms: resource;

&#x20; jsonObject: TJSONObject;

&#x20; data: TStringList;

begin

&#x20; try

&#x20;   // api\_key, api\_secret 설정

&#x20;   coolsms := resource.Create('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74');

&#x20;   // parameters

&#x20;   data := TStringList.create;

&#x20;   data.Values\['to'] := '01000000000'; // 수신번호   &#x20;

&#x20;   **\*** **10월 16일 이후로 발신번호 사전등록제로 인해 등록된 발신번호로만 문자를 보내실 수 있습니다.** [**바로가기** ](https://developer.coolsms.co.kr/SDK\_Delphi\_ko)  &#x20;

&#x20;   data.Values\['from'] := '029302266'; // 발신번호   &#x20;

&#x20;   data.Values\['text'] := 'test'; // 문자내용   &#x20;

&#x20;   data.Values\['type'] := 'mms';  // 문자타입 sms, mms, lms   &#x20;

&#x20;   data.Values\['image'] := '..\\..\test.jpg'; // IMAGE 파일 (MMS일경우)

&#x20;   // 그외 parameters, [https://developer.coolsms.co.kr/SMS\_API#POSTsend](https://developer.coolsms.co.kr/SMS\_API#POSTsend) 참조

&#x20;   {

&#x20;     data.Values\['image\_encoding']

&#x20;         이미지 인코딩 방식 binary(Default), base64

&#x20;     data.Values\['refname']

&#x20;         참조내용(이름)

&#x20;     data.Values\['country']

&#x20;       한국: 82, 일본: 81, 중국: 86, 미국: 1, 기타 등등 (기본 한국)

&#x20;       [http://countrycode.org](http://countrycode.org) 참고

&#x20;     data.Values\['datetime']

&#x20;         예약시간을 YYYYMMDDHHMISS 포맷으로 입력 (입력 없거나 지난날짜를 입력하면 바로 전송) 예) 20131216090510 (2013년 12월 16일 9시 5분 10초에 발송되도록 예약)

&#x20;     data.Values\['subject']

&#x20;         LMS, MMS 일때 제목 (40바이트)

&#x20;     data.Values\['charset']

&#x20;         한글 인코딩 방식 지정 유니코드 UTF-8 일 경우 utf8 완성형 한글(EUC-KR) 일 경우 euckr 으로 입력 입력 없으면 utf8가 기본

&#x20;     data.Values\['srk']

&#x20;         솔루션 제공 수수료를 정산받을 솔루션 등록키

&#x20;     data.Values\['mode']

&#x20;         test로 입력할 경우 CARRIER 시뮬레이터로 시뮬레이션됨 수신번호를 반드시 01000000000 으로 테스트하세요. 예약필드 datetime는 무시됨 결과값은 60 잔액에서 실제 차감되며 다음날 새벽에 재충전됨

&#x20;     data.Values\['delay']

&#x20;         0\~20 사이의 값으로 전송지연 시간을 줄 수 있음, 1은 약 1초 (기본값은 0)

&#x20;     data.Values\['force\_sms']

&#x20;       누리고푸시를 사용하더라도 SMS로 발송되도록 강제

&#x20;       true 혹은 false(기본)

&#x20;     data.Values\['os\_platform']

&#x20;       클라이언트의 OS 및 플랫폼 버전) CentOS 6.6

&#x20;       (v1.5에서 추가됨)

&#x20;     data.Values\['dev\_lang']

&#x20;       개발 프로그래밍 언어 예) PHP 5.3.3

&#x20;       (v1.5에서 추가됨)

&#x20;     data.Values\['sdk\_version']

&#x20;       SDK 버전 예) PHP SDK 1.5

&#x20;       (v1.5에서 추가됨)

&#x20;     data.Values\['app\_version']

&#x20;       어플리케이션 버전 예) Purplebook 4.1

&#x20;       (v1.5에서 추가됨)

&#x20;     data.Values\['extension']

&#x20;         JSON 포맷의 개별 메시지를 담을 수 있음

&#x20;   }

&#x20;   // send Messages

&#x20;   jsonObject := coolsms.send(data);

&#x20;   if strToBool(jsonObject.GetValue('status').ToString) = TRUE then

&#x20;   begin

&#x20;     Writeln('성공');

&#x20;     Writeln('group\_id : ' + jsonObject.Get('group\_id').JsonValue.ToString);

&#x20;     Writeln('success\_count : ' + jsonObject.Get('success\_count').JsonValue.ToString);

&#x20;     Writeln('error\_count : ' + jsonObject.Get('error\_count').JsonValue.ToString);

&#x20;     Writeln('result\_code : ' + jsonObject.Get('result\_code').JsonValue.ToString);

&#x20;     Writeln('result\_message : ' + jsonObject.Get('result\_message').JsonValue.ToString);

&#x20;   end

&#x20;   else

&#x20;   begin

&#x20;     Writeln('실패');

&#x20;     if jsonObject.Get('code').Equals(Nil) = FALSE then Writeln('code : ' + jsonObject.Get('code').JsonValue.ToString);

&#x20;     if jsonObject.Get('message').Equals(Nil) = FALSE then Writeln('message : ' + jsonObject.Get('message').JsonValue.ToString);

&#x20;   end;

&#x20;   jsonObject.Free;

&#x20;   Writeln('-----------------------------------------');

&#x20;   Writeln('Press \<enter> to quit...');

&#x20;   Readln;

&#x20; except

&#x20;   on E: Exception do

&#x20;     Writeln(E.ClassName, ': ', E.Message);

&#x20; end;

end.

### SMS발송(개별)

SMS발송(개별)은 여러명의 사용자에게 각가 다른 내용이 들어간 문자를 보내고 싶을때 사용합니다.

TStringlist data에 각각의 TJSONObject들이 들어간 TJSONArray를 ToString으로 parameter extension에 넣어주시면됩니다.

uses\
&#x20; System.Json, coolsms in '..\\..\coolsms.pas', https in '..\\..\https.pas', System.SysUtils, Classes;

var\
&#x20; coolsms: resource;\
&#x20; jsonObject: TJSONObject;\
&#x20; extensionObject: TJSONObject;\
&#x20; extensionArray: TJSONArray;\
&#x20; data: TStringList;

begin\
&#x20; try\
&#x20;   // api\_key, api\_secret 설정\
&#x20;   coolsms := resource.Create('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74');

&#x20;   // 개별 메시지 보내기\
&#x20;   extensionObject := TJSONObject.Create;\
&#x20;   extensionArray := TJSONArray.Create;

&#x20;   // message 1 parameters\
&#x20;   extensionObject.AddPair('type', 'sms');\
&#x20;   extensionObject.AddPair('to', '01000000003');\
&#x20;   extensionObject.AddPair('text', 'sms\_test');\
&#x20;   extensionArray.Add(extensionObject);

&#x20;   // message 2 parameters\
&#x20;   extensionObject := TJSONObject.Create;\
&#x20;   extensionObject.AddPair('type', 'sms');\
&#x20;   extensionObject.AddPair('to', '01000000000, 010000000001');\
&#x20;   extensionObject.AddPair('text', 'sms\_test2');\
&#x20;   extensionArray.Add(extensionObject);

&#x20;   // input extension\_data into string\_list\
&#x20;   data := TStringList.create;\
&#x20;   data.Values\['extension'] := extensionArray.ToString;  &#x20;

&#x20;   **\*** **10월 16일 이후로 발신번호 사전등록제로 인해 등록된 발신번호로만 문자를 보내실 수 있습니다.** [**바로가기** ](https://developer.coolsms.co.kr/SDK\_Delphi\_ko)  &#x20;

&#x20;   data.Values\['from'] := '029302266'; // 발신번호

&#x20;   // send Messages\
&#x20;   jsonObject := coolsms.send(data);\
&#x20;   if strToBool(jsonObject.GetValue('status').ToString) = TRUE then\
&#x20;   begin\
&#x20;     Writeln('성공');\
&#x20;     Writeln('group\_id : ' + jsonObject.Get('group\_id').JsonValue.ToString);\
&#x20;     Writeln('success\_count : ' + jsonObject.Get('success\_count').JsonValue.ToString);\
&#x20;     Writeln('error\_count : ' + jsonObject.Get('error\_count').JsonValue.ToString);\
&#x20;     Writeln('result\_code : ' + jsonObject.Get('result\_code').JsonValue.ToString);\
&#x20;     Writeln('result\_message : ' + jsonObject.Get('result\_message').JsonValue.ToString);\
&#x20;   end\
&#x20;   else\
&#x20;   begin\
&#x20;     Writeln('실패');\
&#x20;     if jsonObject.Get('code').Equals(Nil) = FALSE then Writeln('code : ' + jsonObject.Get('code').JsonValue.ToString);\
&#x20;     if jsonObject.Get('message').Equals(Nil) = FALSE then Writeln('message : ' + jsonObject.Get('message').JsonValue.ToString);\
&#x20;   end;

&#x20;   jsonObject.Free;

&#x20;   Writeln('-----------------------------------------');\
&#x20;   Writeln('Press \<enter> to quit...');\
&#x20;   Readln;\
&#x20; except\
&#x20;   on E: Exception do\
&#x20;     Writeln(E.ClassName, ': ', E.Message);\
&#x20; end;\
end.

### LMS발송

type 을 lms로 바꿔주시기만하면됩니다.

uses

&#x20; System.Json, coolsms in '..\\..\coolsms.pas', https in '..\\..\https.pas', System.SysUtils, Classes;

var

&#x20; coolsms: resource;

&#x20; jsonObject: TJSONObject;

&#x20; data: TStringList;

begin

&#x20; try

&#x20;   // api\_key, api\_secret 설정

&#x20;   coolsms := resource.Create('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74');

&#x20;   // parameters

&#x20;   data := TStringList.create;

&#x20;   data.Values\['to'] := '01000000000'; // 수신번호    **\*** **10월 16일 이후로 발신번호 사전등록제로 인해 등록된 발신번호로만 문자를 보내실 수 있습니다.** [**바로가기**](https://developer.coolsms.co.kr/SDK\_Delphi\_ko)

&#x20;   data.Values\['from'] := '029302266'; // 발신번호

&#x20;   data.Values\['text'] := 'test'; // 문자내용

&#x20;   data.Values\['type'] := 'lms';  // 문자타입 sms, mms, lms

&#x20;   // send Messages

&#x20;   jsonObject := coolsms.send(data);

&#x20;   if strToBool(jsonObject.GetValue('status').ToString) = TRUE then

&#x20;   begin

&#x20;     Writeln('성공');

&#x20;     Writeln('group\_id : ' + jsonObject.Get('group\_id').JsonValue.ToString);

&#x20;     Writeln('success\_count : ' + jsonObject.Get('success\_count').JsonValue.ToString);

&#x20;     Writeln('error\_count : ' + jsonObject.Get('error\_count').JsonValue.ToString);

&#x20;     Writeln('result\_code : ' + jsonObject.Get('result\_code').JsonValue.ToString);

&#x20;     Writeln('result\_message : ' + jsonObject.Get('result\_message').JsonValue.ToString);

&#x20;   end

&#x20;   else

&#x20;   begin

&#x20;     Writeln('실패');

&#x20;     if jsonObject.Get('code').Equals(Nil) = FALSE then Writeln('code : ' + jsonObject.Get('code').JsonValue.ToString);

&#x20;     if jsonObject.Get('message').Equals(Nil) = FALSE then Writeln('message : ' + jsonObject.Get('message').JsonValue.ToString);

&#x20;   end;

&#x20;   jsonObject.Free;

&#x20;   Writeln('-----------------------------------------');

&#x20;   Writeln('Press \<enter> to quit...');

&#x20;   Readln;

&#x20; except

&#x20;   on E: Exception do

&#x20;     Writeln(E.ClassName, ': ', E.Message);

&#x20; end;

end.

### MMS발송

type을 mms로 바꿔준뒤 전송할 이미지 파일 정보를 입력합니다.&#x20;

uses

&#x20; System.Json, coolsms in '..\\..\coolsms.pas', https in '..\\..\https.pas', System.SysUtils, Classes;

var

&#x20; coolsms: resource;

&#x20; jsonObject: TJSONObject;

&#x20; data: TStringList;

begin

&#x20; try

&#x20;   // api\_key, api\_secret 설정

&#x20;   coolsms := resource.Create('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74');

&#x20;   // parameters

&#x20;   data := TStringList.create;

&#x20;   data.Values\['to'] := '01000000000'; // 수신번호    **\*** **10월 16일 이후로 발신번호 사전등록제로 인해 등록된 발신번호로만 문자를 보내실 수 있습니다.** [**바로가기**](https://developer.coolsms.co.kr/SDK\_Delphi\_ko)

&#x20;   data.Values\['from'] := '029302266'; // 발신번호

&#x20;   data.Values\['text'] := 'test'; // 문자내용

&#x20;   data.Values\['type'] := 'mms';  // 문자타입 sms, mms, lms

&#x20;   data.Values\['image'] := '..\\..\test.jpg'; // IMAGE 파일 (MMS일경우)

&#x20;   // send Messages

&#x20;   jsonObject := coolsms.send(data);

&#x20;   if strToBool(jsonObject.GetValue('status').ToString) = TRUE then

&#x20;   begin

&#x20;     Writeln('성공');

&#x20;     Writeln('group\_id : ' + jsonObject.Get('group\_id').JsonValue.ToString);

&#x20;     Writeln('success\_count : ' + jsonObject.Get('success\_count').JsonValue.ToString);

&#x20;     Writeln('error\_count : ' + jsonObject.Get('error\_count').JsonValue.ToString);

&#x20;     Writeln('result\_code : ' + jsonObject.Get('result\_code').JsonValue.ToString);

&#x20;     Writeln('result\_message : ' + jsonObject.Get('result\_message').JsonValue.ToString);

&#x20;   end

&#x20;   else

&#x20;   begin

&#x20;     Writeln('실패');

&#x20;     if jsonObject.Get('code').Equals(Nil) = FALSE then Writeln('code : ' + jsonObject.Get('code').JsonValue.ToString);

&#x20;     if jsonObject.Get('message').Equals(Nil) = FALSE then Writeln('message : ' + jsonObject.Get('message').JsonValue.ToString);

&#x20;   end;

&#x20;   jsonObject.Free;

&#x20;   Writeln('-----------------------------------------');

&#x20;   Writeln('Press \<enter> to quit...');

&#x20;   Readln;

&#x20; except

&#x20;   on E: Exception do

&#x20;     Writeln(E.ClassName, ': ', E.Message);

&#x20; end;

end.

### 예약발송

data에 datetime을 추가해주시면 됩니다.

uses

&#x20; System.Json, coolsms in '..\\..\coolsms.pas', https in '..\\..\https.pas', System.SysUtils, Classes;

var

&#x20; coolsms: resource;

&#x20; jsonObject: TJSONObject;

&#x20; data: TStringList;

begin

&#x20; try

&#x20;   // api\_key, api\_secret 설정

&#x20;   coolsms := resource.Create('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74');

&#x20;   // parameters

&#x20;   data := TStringList.create;

&#x20;   data.Values\['to'] := '01000000000'; // 수신번호    **\*** **10월 16일 이후로 발신번호 사전등록제로 인해 등록된 발신번호로만 문자를 보내실 수 있습니다.** [**바로가기**](https://developer.coolsms.co.kr/SDK\_Delphi\_ko)

&#x20;   data.Values\['from'] := '029302266'; // 발신번호

&#x20;   data.Values\['text'] := 'test'; // 문자내용

&#x20;   data.Values\['datetime'] := '20131216090510'; // 예약시간을 YYYYMMDDHHMISS 포맷으로 입력 (입력 없거나 지난날짜를 입력하면 바로 전송) 예) 20131216090510 (2013년 12월 16일 9시 5분 10초에 발송되도록 예약)

&#x20;   // send Messages

&#x20;   jsonObject := coolsms.send(data);

&#x20;   if strToBool(jsonObject.GetValue('status').ToString) = TRUE then

&#x20;   begin

&#x20;     Writeln('성공');

&#x20;     Writeln('group\_id : ' + jsonObject.Get('group\_id').JsonValue.ToString);

&#x20;     Writeln('success\_count : ' + jsonObject.Get('success\_count').JsonValue.ToString);

&#x20;     Writeln('error\_count : ' + jsonObject.Get('error\_count').JsonValue.ToString);

&#x20;     Writeln('result\_code : ' + jsonObject.Get('result\_code').JsonValue.ToString);

&#x20;     Writeln('result\_message : ' + jsonObject.Get('result\_message').JsonValue.ToString);

&#x20;   end

&#x20;   else

&#x20;   begin

&#x20;     Writeln('실패');

&#x20;     if jsonObject.Get('code').Equals(Nil) = FALSE then Writeln('code : ' + jsonObject.Get('code').JsonValue.ToString);

&#x20;     if jsonObject.Get('message').Equals(Nil) = FALSE then Writeln('message : ' + jsonObject.Get('message').JsonValue.ToString);

&#x20;   end;

&#x20;   jsonObject.Free;

&#x20;   Writeln('-----------------------------------------');

&#x20;   Writeln('Press \<enter> to quit...');

&#x20;   Readln;

&#x20; except

&#x20;   on E: Exception do

&#x20;     Writeln(E.ClassName, ': ', E.Message);

&#x20; end;

end.

### 예약취소

data에 mid나 gid를 입력하신뒤 postRequest('cancel', data, 'sms')를 호출합니다.

uses\
&#x20; System.Json, coolsms in '..\\..\coolsms.pas', https in '..\\..\https.pas', System.SysUtils, Classes;

var\
&#x20; coolsms: resource;\
&#x20; jsonObject: TJSONObject;\
&#x20; data: TStringList;

begin\
&#x20; try\
&#x20;   // api\_key, api\_secret 설정\
&#x20;   coolsms := resource.Create('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74');

&#x20;   // parameters, [http://www.coolsms.co.kr/SMS\_API#POSTcancel](http://www.coolsms.co.kr/SMS\_API#POSTcancel) 참조\
&#x20;   data := TStringList.create;\
&#x20;   data.Values\['mid'] := 'R1M55D585C2CE9E9'; // 메시지ID\
&#x20;   // data.Values\['gid'] := ''; // 그룹ID

&#x20;   // 예약취소 요청\
&#x20;   jsonObject := coolsms.cancel(data);\
&#x20;   if strToBool(jsonObject.GetValue('status').ToString) = TRUE then\
&#x20;   begin\
&#x20;     Writeln('성공');\
&#x20;   end\
&#x20;   else\
&#x20;   begin\
&#x20;     Writeln('실패');\
&#x20;     if jsonObject.Get('code').Equals(Nil) = FALSE then Writeln('code : ' + jsonObject.Get('code').JsonValue.ToString);\
&#x20;     if jsonObject.Get('message').Equals(Nil) = FALSE then Writeln('message : ' + jsonObject.Get('message').JsonValue.ToString);\
&#x20;   end;

&#x20;   jsonObject.Free;

&#x20;   Writeln('-----------------------------------------');\
&#x20;   Writeln('Press \<enter> to quit...');\
&#x20;   Readln;\
&#x20; except\
&#x20;   on E: Exception do\
&#x20;     Writeln(E.ClassName, ': ', E.Message);\
&#x20; end;\
end.

### 발송내역

data에 mid나 gid를 입력하신후 request('sent', data, 'sms')를 통해 발송내역을 가져옵니다.

Return 값은 jsonObject 안에 jsonArray로 받습니다.

uses\
&#x20; System.Json, coolsms in '..\\..\coolsms.pas', https in '..\\..\https.pas', System.SysUtils, Classes;

var\
&#x20; coolsms: resource;\
&#x20; data: TStringList;\
&#x20; jsonObject: TJSONObject;\
&#x20; jsonArray: TJSONArray;\
&#x20; jsonObjectData: TJSONObject;\
&#x20; i: integer;

begin\
&#x20; try\
&#x20;   // api\_key, api\_secret 설정\
&#x20;   coolsms := resource.Create('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74');\
&#x20;   //https.create('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74');

&#x20;   // parameters, data 설정 mid나 gid 둘 중 하나는 들어가야 합니다.\
&#x20;   data := TStringList.create;\
&#x20;   data.Values\['mid'] := 'R1M55B1FFB27E5308'; // 메시지ID

&#x20;   // 그외 parameters, [http://www.https.co.kr/SMS\_API#GETsent](http://www.https.co.kr/SMS\_API#GETsent) 참조\
&#x20;   {\
&#x20;       data.Values\['count']\
&#x20;         기본값 20이며 20개의 목록을 받을 수 있음. 40입력시 40개의 목록이 리턴\
&#x20;     data.Values\['page']\
&#x20;         1부터 시작하는 페이지값\
&#x20;     data.Values\['rcpt']\
&#x20;         수신번호로 검색\
&#x20;     data.Values\['start']\
&#x20;         검색 시작일시 접수 날짜와 시간으로 검색 YYYY-MM-DD HH:MI:SS 포맷의 날짜와 시간\
&#x20;     data.Values\['end']\
&#x20;         검색 종료일시 접수 날짜와 시간으로 검색 YYYY-MM-DD HH:MI:SS 포맷의 날짜와 시간\
&#x20;     data.Values\['status']\
&#x20;         메시지 상태 값으로 검색\
&#x20;     data.Values\['resultcode']\
&#x20;         전송결과 값으로 검색\
&#x20;     data.Values\['notin\_resultcode']\
&#x20;         입력된 전송결과 값 이외의 건들만 조회\
&#x20;     data.Values\['gid']\
&#x20;         그룹ID\
&#x20;   }

&#x20;   // sent Messages\
&#x20;   jsonObject := coolsms.sent(data);\
&#x20;   if strToBool(jsonObject.GetValue('status').ToString) = TRUE then\
&#x20;   begin\
&#x20;     Writeln('성공');\
&#x20;     jsonArray := JsonObject.Get('data').JsonValue as TJSONArray;

&#x20;     Writeln('total\_count : ' + jsonObject.Get('total\_count').JsonValue.ToString);\
&#x20;     Writeln('list\_count : ' + jsonObject.Get('list\_count').JsonValue.ToString);\
&#x20;     Writeln('page : ' + jsonObject.Get('page').JsonValue.ToString);

&#x20;     for i := 0 to jsonArray.Size - 1 do\
&#x20;     begin\
&#x20;         jsonObjectData := TJSONObject.Create;\
&#x20;         jsonObjectData := jsonArray.Get(i) as TJSONObject;

&#x20;         Writeln('-----------------------------------------');\
&#x20;         Writeln('type : ' + jsonObjectData.Get('type').JsonValue.ToString);\
&#x20;         Writeln('recipient\_number : ' + jsonObjectData.Get('recipient\_number').JsonValue.ToString);\
&#x20;         Writeln('text : ' + jsonObjectData.Get('text').JsonValue.ToString);\
&#x20;         Writeln('carrier : ' + jsonObjectData.Get('carrier').JsonValue.ToString);\
&#x20;         Writeln('status : ' + jsonObjectData.Get('status').JsonValue.ToString);\
&#x20;         Writeln('result\_code : ' + jsonObjectData.Get('result\_code').JsonValue.ToString);\
&#x20;         Writeln('result\_message : ' + jsonObjectData.Get('result\_message').JsonValue.ToString);\
&#x20;         Writeln('message\_id : ' + jsonObjectData.Get('message\_id').JsonValue.ToString);\
&#x20;         Writeln('group\_id : ' + jsonObjectData.Get('group\_id').JsonValue.ToString);\
&#x20;         Writeln('sent\_time : ' + jsonObjectData.Get('sent\_time').JsonValue.ToString);\
&#x20;         Writeln('accepted\_time : ' + jsonObjectData.Get('accepted\_time').JsonValue.ToString);\
&#x20;     end;\
&#x20;   end\
&#x20;   else\
&#x20;   begin\
&#x20;     Writeln('실패');\
&#x20;     if jsonObject.Get('code').Equals(Nil) = FALSE then Writeln('code : ' + jsonObject.Get('code').JsonValue.ToString);\
&#x20;     if jsonObject.Get('message').Equals(Nil) = FALSE then Writeln('message : ' + jsonObject.Get('message').JsonValue.ToString);\
&#x20;   end;

&#x20;   jsonObject.Free;

&#x20;   Writeln('-----------------------------------------');\
&#x20;   Writeln('Press \<enter> to quit...');\
&#x20;   Readln;\
&#x20; except\
&#x20;   on E: Exception do\
&#x20;     Writeln(E.ClassName, ': ', E.Message);\
&#x20; end;\
end.

### 잔액정보

request('balance', Nil, 'sms')를 통해 잔액정보를 가져옵니다.

uses\
&#x20; System.Json, coolsms in '..\\..\coolsms.pas', https in '..\\..\https.pas', System.SysUtils;

var\
&#x20; coolsms: resource;\
&#x20; jsonObject: TJSONObject;

begin\
&#x20; try\
&#x20;   // api\_key, api\_secret 설정\
&#x20;   coolsms := resource.Create('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74');

&#x20;   // 남은잔액 요청, [http://www.coolsms.co.kr/SMS\_API#GETbalance](http://www.coolsms.co.kr/SMS\_API#GETbalance) 참조\
&#x20;   jsonObject := coolsms.balance();\
&#x20;   if strToBool(jsonObject.GetValue('status').ToString) = TRUE then\
&#x20;   begin\
&#x20;     Writeln('성공');\
&#x20;     Writeln('cash : ' + jsonObject.Get('cash').JsonValue.ToString);\
&#x20;     Writeln('point : ' + jsonObject.Get('point').JsonValue.ToString);\
&#x20;   end\
&#x20;   else\
&#x20;   begin\
&#x20;     Writeln('실패');\
&#x20;     if jsonObject.Get('code').Equals(Nil) = FALSE then Writeln('code : ' + jsonObject.Get('code').JsonValue.ToString);\
&#x20;     if jsonObject.Get('message').Equals(Nil) = FALSE then Writeln('message : ' + jsonObject.Get('message').JsonValue.ToString);\
&#x20;   end;

&#x20;   jsonObject.Free;

&#x20;   Writeln('-----------------------------------------');\
&#x20;   Writeln('Press \<enter> to quit...');\
&#x20;   Readln;\
&#x20; except\
&#x20;   on E: Exception do\
&#x20;     Writeln(E.ClassName, ': ', E.Message);\
&#x20; end;\
end.

## 발신번호등록

### 발신번호 등록 요청

\* 보안상 문제로 현재는 제공하지 않습니다. 쿨에스엠에스 사이트에서 발신번호를 등록해 주세요

관련 정보는 [http://www.coolsms.co.kr/SenderID\_API](http://www.coolsms.co.kr/SenderID\_API)를 참고해주세요.

postRequest('register', data, 'senderid')로 요청을 해서 넘어오는 ars\_number로 전화를 걸어주시면 됩니다.

uses\
&#x20; System.Json, coolsms in '..\\..\coolsms.pas', https in '..\\..\https.pas', System.SysUtils, Classes;

var\
&#x20; coolsms: resource;\
&#x20; data: TStringList;\
&#x20; jsonObject: TJSONObject;

begin\
&#x20; try\
&#x20;   // [http://www.coolsms.co.kr/SenderID\_API#POSTregister](http://www.coolsms.co.kr/SenderID\_API#POSTregister) 참조

&#x20;   // api\_key, api\_secret 설정\
&#x20;   coolsms := resource.Create('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74');

&#x20;   // parameters\
&#x20;   data := TStringList.create;\
&#x20;   data.Values\['phone'] := '01090683469'; // 발신번호로 등록할 전화번호를 입력해주세요.

&#x20;   // 발신번호등록 요청\
&#x20;   jsonObject := coolsms.register(data);\
&#x20;   if strToBool(jsonObject.GetValue('status').ToString) = TRUE then\
&#x20;   begin\
&#x20;     Writeln('성공');\
&#x20;     Writeln('handle\_key : ' + jsonObject.Get('handle\_key').JsonValue.ToString);\
&#x20;     Writeln('ars\_number : ' + jsonObject.Get('ars\_number').JsonValue.ToString);\
&#x20;   end\
&#x20;   else\
&#x20;   begin\
&#x20;     Writeln('실패');\
&#x20;     if jsonObject.Get('code').Equals(Nil) = FALSE then Writeln('code : ' + jsonObject.Get('code').JsonValue.ToString);\
&#x20;     if jsonObject.Get('message').Equals(Nil) = FALSE then Writeln('message : ' + jsonObject.Get('message').JsonValue.ToString);\
&#x20;   end;

&#x20;   jsonObject.Free;

&#x20;   Writeln('-----------------------------------------');\
&#x20;   Writeln('Press \<enter> to quit...');\
&#x20;   Readln;\
&#x20; except\
&#x20;   on E: Exception do\
&#x20;     Writeln(E.ClassName, ': ', E.Message);\
&#x20; end;\
end.

### 발신번호 등록 확인

\* 보안상 문제로 현재는 제공하지 않습니다. 쿨에스엠에스 사이트에서 발신번호를 등록해 주세요

register에서 받은 ars\_number로 전화를 거신후 handle\_key로 postRequest('verify', data, 'senderid')를 호출하시면 발신번호 등록이 완료됩니다.

uses\
&#x20; System.Json, coolsms in '..\\..\coolsms.pas', https in '..\\..\https.pas', System.SysUtils, Classes;

var\
&#x20; coolsms: resource;\
&#x20; data: TStringList;\
&#x20; jsonObject: TJSONObject;

begin\
&#x20; try\
&#x20;   // [http://www.coolsms.co.kr/SenderID\_API#POSTverify](http://www.coolsms.co.kr/SenderID\_API#POSTverify) 참조

&#x20;   // api\_key, api\_secret 설정\
&#x20;   coolsms := resource.Create('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74');

&#x20;   // parameters\
&#x20;   data := TStringList.create;\
&#x20;   data.Values\['handle\_key'] := 'SID5FFFF7614ED3'; // register 호출 후 리턴받은 핸들값

&#x20;   // 발신번호등록확인 요청\
&#x20;   jsonObject := coolsms.verify(data);\
&#x20;   if strToBool(jsonObject.GetValue('status').ToString) = TRUE then\
&#x20;   begin\
&#x20;     Writeln('성공');\
&#x20;   end\
&#x20;   else\
&#x20;   begin\
&#x20;     Writeln('실패');\
&#x20;     if jsonObject.Get('code').Equals(Nil) = FALSE then Writeln('code : ' + jsonObject.Get('code').JsonValue.ToString);\
&#x20;     if jsonObject.Get('message').Equals(Nil) = FALSE then Writeln('message : ' + jsonObject.Get('message').JsonValue.ToString);\
&#x20;   end;

&#x20;   jsonObject.Free;

&#x20;   Writeln('-----------------------------------------');\
&#x20;   Writeln('Press \<enter> to quit...');\
&#x20;   Readln;\
&#x20; except\
&#x20;   on E: Exception do\
&#x20;     Writeln(E.ClassName, ': ', E.Message);\
&#x20; end;\
end.

### 발신번호 삭제

data에 해당 발신번호릐 handle\_key를 입력하시고 postRequest('delete', data, 'sendid')를 호출하시면 됩니다.

uses\
&#x20; System.Json, coolsms in '..\\..\coolsms.pas', https in '..\\..\https.pas', System.SysUtils, Classes;

var\
&#x20; coolsms: resource;\
&#x20; data: TStringList;\
&#x20; jsonObject: TJSONObject;

begin\
&#x20; try\
&#x20;   // [http://www.coolsms.co.kr/SenderID\_API#POSTdelete](http://www.coolsms.co.kr/SenderID\_API#POSTdelete) 참조

&#x20;   // api\_key, api\_secret 설정\
&#x20;   coolsms := resource.Create('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74');

&#x20;   // parameters\
&#x20;   data := TStringList.create;\
&#x20;   data.Values\['handle\_key'] := 'SFFFFFFF7E1D7'; // 삭제할 발신번호의 handle\_key

&#x20;   // 발신번호삭제 요청\
&#x20;   jsonObject := coolsms.delete(data);\
&#x20;   if strToBool(jsonObject.GetValue('status').ToString) = TRUE then\
&#x20;   begin\
&#x20;     Writeln('성공');\
&#x20;   end\
&#x20;   else\
&#x20;   begin\
&#x20;     Writeln('실패');\
&#x20;     if jsonObject.Get('code').Equals(Nil) = FALSE then Writeln('code : ' + jsonObject.Get('code').JsonValue.ToString);\
&#x20;     if jsonObject.Get('message').Equals(Nil) = FALSE then Writeln('message : ' + jsonObject.Get('message').JsonValue.ToString);\
&#x20;   end;

&#x20;   jsonObject.Free;

&#x20;   Writeln('-----------------------------------------');\
&#x20;   Writeln('Press \<enter> to quit...');\
&#x20;   Readln;\
&#x20; except\
&#x20;   on E: Exception do\
&#x20;     Writeln(E.ClassName, ': ', E.Message);\
&#x20; end;\
end.

### 발신번호 목록 보기

request('list', Nil, 'senderid')를 요청하시면 됩니다.

Return값은 jsonObject안에 jsonArray로 처리해주세요.

uses\
&#x20; System.Json, coolsms in '..\\..\coolsms.pas', https in '..\\..\https.pas', System.SysUtils, Classes;

var\
&#x20; coolsms: resource;\
&#x20; data: TStringList;\
&#x20; jsonObject: TJSONObject;\
&#x20; jsonArray: TJSONArray;\
&#x20; jsonObjectData: TJSONObject;\
&#x20; i: integer;

begin\
&#x20; try\
&#x20;   // [http://www.coolsms.co.kr/SenderID\_API#GETlist](http://www.coolsms.co.kr/SenderID\_API#GETlist) 참조

&#x20;   // api\_key, api\_secret 설정\
&#x20;   coolsms := resource.Create('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74');

&#x20;   // 발신번호 리스트 요청\
&#x20;   jsonObject := coolsms.list();

&#x20;   if strToBool(jsonObject.GetValue('status').ToString) = TRUE then\
&#x20;   begin\
&#x20;     Writeln('성공');\
&#x20;     jsonArray := JsonObject.Get('data').JsonValue as TJSONArray;\
&#x20;     for i := 0 to jsonArray.Size - 1 do\
&#x20;     begin\
&#x20;         jsonObjectData := TJSONObject.Create;\
&#x20;         jsonObjectData := jsonArray.Get(i) as TJSONObject;

&#x20;         Writeln('-----------------------------------------');\
&#x20;         Writeln('idno : ' + jsonObjectData.Get('idno').JsonValue.ToString);\
&#x20;         Writeln('phone\_number : ' + jsonObjectData.Get('phone\_number').JsonValue.ToString);\
&#x20;         Writeln('flag\_default : ' + jsonObjectData.Get('flag\_default').JsonValue.ToString);\
&#x20;         Writeln('updatetime : ' + jsonObjectData.Get('updatetime').JsonValue.ToString);\
&#x20;         Writeln('regdate : ' + jsonObjectData.Get('regdate').JsonValue.ToString);\
&#x20;     end;\
&#x20;   end\
&#x20;   else\
&#x20;   begin\
&#x20;     Writeln('실패');\
&#x20;     if jsonObject.Get('code').Equals(Nil) = FALSE then Writeln('code : ' + jsonObject.Get('code').JsonValue.ToString);\
&#x20;     if jsonObject.Get('message').Equals(Nil) = FALSE then Writeln('message : ' + jsonObject.Get('message').JsonValue.ToString);\
&#x20;   end;

&#x20;   jsonObject.Free;

\
&#x20;   Writeln('-----------------------------------------');\
&#x20;   Writeln('Press \<enter> to quit...');\
&#x20;   Readln;\
&#x20; except\
&#x20;   on E: Exception do\
&#x20;     Writeln(E.ClassName, ': ', E.Message);\
&#x20; end;\
end.

### 기본 발신번호 설정

해당 발신번호의 handle\_key를 data에 넣으신후 postRequest('set\_default', data, 'senderid')를 요청하시면 됩니다.

uses\
&#x20; System.Json, coolsms in '..\\..\coolsms.pas', https in '..\\..\https.pas', System.SysUtils, Classes;

var\
&#x20; coolsms: resource;\
&#x20; data: TStringList;\
&#x20; jsonObject: TJSONObject;

begin\
&#x20; try\
&#x20;   // [http://www.coolsms.co.kr/SenderID\_API#POSTset\_default](http://www.coolsms.co.kr/SenderID\_API#POSTset\_default) 참조

&#x20;   // api\_key, api\_secret 설정\
&#x20;   coolsms := resource.Create('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74');

&#x20;   // parameters\
&#x20;   data := TStringList.create;\
&#x20;   data.Values\['handle\_key'] := 'SIDFFFFF614ED3'; // register 호출 후 리턴받은 핸들값

&#x20;   // default 발신번호등록 요청\
&#x20;   jsonObject := coolsms.setDefault(data);\
&#x20;   if strToBool(jsonObject.GetValue('status').ToString) = TRUE then\
&#x20;   begin\
&#x20;     Writeln('성공');\
&#x20;   end\
&#x20;   else\
&#x20;   begin\
&#x20;     Writeln('실패');\
&#x20;     if jsonObject.Get('code').Equals(Nil) = FALSE then Writeln('code : ' + jsonObject.Get('code').JsonValue.ToString);\
&#x20;     if jsonObject.Get('message').Equals(Nil) = FALSE then Writeln('message : ' + jsonObject.Get('message').JsonValue.ToString);\
&#x20;   end;

&#x20;   jsonObject.Free;

&#x20;   Writeln('-----------------------------------------');\
&#x20;   Writeln('Press \<enter> to quit...');\
&#x20;   Readln;\
&#x20; except\
&#x20;   on E: Exception do\
&#x20;     Writeln(E.ClassName, ': ', E.Message);\
&#x20; end;\
end.

### 기본 발신번호 보기

request('get\_default', Nil, 'senderid')로 요청하시면 됩니다.

uses\
&#x20; System.Json, coolsms in '..\\..\coolsms.pas', https in '..\\..\https.pas', System.SysUtils, Classes;

var\
&#x20; coolsms: resource;\
&#x20; data: TStringList;\
&#x20; jsonObject: TJSONObject;

begin\
&#x20; try\
&#x20;   // [http://www.coolsms.co.kr/SenderID\_API#POSTset\_default](http://www.coolsms.co.kr/SenderID\_API#POSTset\_default) 참조

&#x20;   // api\_key, api\_secret 설정\
&#x20;   coolsms := resource.Create('NCS55882FB7DE511A', '4FB5FF82B9AB7D0E0AEB840D403DE0F74');

&#x20;   // default 발신번호 요청\
&#x20;   jsonObject := coolsms.getDefault();\
&#x20;   if strToBool(jsonObject.GetValue('status').ToString) = TRUE then\
&#x20;   begin\
&#x20;     Writeln('성공');\
&#x20;     Writeln('handle\_key : ' + jsonObject.Get('handle\_key').JsonValue.ToString);\
&#x20;     Writeln('phone\_number : ' + jsonObject.Get('phone\_number').JsonValue.ToString);\
&#x20;   end\
&#x20;   else\
&#x20;   begin\
&#x20;     Writeln('실패');\
&#x20;     if jsonObject.Get('code').Equals(Nil) = FALSE then Writeln('code : ' + jsonObject.Get('code').JsonValue.ToString);\
&#x20;     if jsonObject.Get('message').Equals(Nil) = FALSE then Writeln('message : ' + jsonObject.Get('message').JsonValue.ToString);\
&#x20;   end;

&#x20;   jsonObject.Free;

&#x20;   Writeln('-----------------------------------------');\
&#x20;   Writeln('Press \<enter> to quit...');\
&#x20;   Readln;\
&#x20; except\
&#x20;   on E: Exception do\
&#x20;     Writeln(E.ClassName, ': ', E.Message);\
&#x20; end;\
end.
