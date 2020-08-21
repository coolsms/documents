# 발신번호



#### 발신번호 관련

\* 발신번호 \(SenderID\) API 문서  [바로가기](https://developer.coolsms.co.kr/SenderID_API)

\* 웹에서 발신번호 등록하러가기 [바로가기](http://www.coolsms.co.kr/senderids)

\(coolsms.co.kr 메뉴에서 문자보내기 -&gt; 환경설정 -&gt; 발신번호 설정 탭\)

#### 등록하기     POST register

\* 보안상 문제로 현재는 제공하지 않습니다. 쿨에스엠에스 사이트에서 발신번호를 등록해 주세요

발신번호를 등록합니다. 하지만 verify 리소스를 호출하여 인증확인 절차를 거쳐야 활성화 됩니다.

```text
$options->phone = "021231234";                       //등록하려고 하는 발신번호
$rest = new coolsms($apikey, $apisecret);
$result = $rest->register($options)->getResult();
```

#### Response Format

```text
{
    "handle_key":"SID55DAD88A7E4EC",
    "ars_number":"01021382269"
}
```

####  

#### 발신번호 가져오기      GET list

등록된 발신번호 목록을 조회합니다.

1\) 등록된 발신번호 전부 가져오기

```text
$rest = new coolsms($apikey, $apisecret); 
$senderid = $rest->get_senderid_list($options);
```

2\) default 로 설정된 발신번호 가져오기

```text
$rest = new coolsms($apikey, $apisecret);
$senderid = $rest->get_default($options);
```

#### Response Format

```text
[
    {"idno":"SID555C89C49627D","phone_number":"0809302266","flag_default":"Y","updatetime":"2015-06-12 10:21:06","regdate":"2015-05-20 22:19:00"},
    {"idno":"SID5568347CC1518","phone_number":"01012345678","flag_default":"N","updatetime":"2015-05-29 18:42:58","regdate":"2015-05-29 18:42:20"}
]
```

####  

#### 활성화 시키기      POST verify

\* 보안상 문제로 현재는 제공하지 않습니다. 쿨에스엠에스 사이트에서 발신번호를 등록해 주세요

해당 발신번호의 인증결과를 확인 후 활성화 시킵니다.

```text
$options->handle_key = "SID111111111";
$rest = new coolsms($apikey, $apisecret);
$result = $rest->verify($options)->getResult();
```

####  

#### default 발신번호 설정하기    POST set \_default

기본으로 사용될 발신번호를 지정합니다.

```text
$options->handle_key = "SID11111111";
$rest = new coolsms($apikey, $apisecret);
$result = $rest->set_default($options)->getResult();
```

####  

#### default 발신번호 가져오기   GET get\_default

기본으로 사용될 발신번호를 리턴합니다.

```text
$rest = new coolsms($apikey, $apisecret);
$result = $rest->get_default()->getResult();
```

####  

#### 발신번호 삭제하기       POST delete

발신번호를 삭제합니다. 

```text
$options->handle_key = "SID111111111";
$rest = new coolsms($apikey, $apisecret);
$result = $rest->delete($options);
```

