# API Reference



### coolsms.php

coolsms.php 의 rest 클래스를 생성합니다. 아래와 같은 형태로 객체를 생성할 수 있습니다.

```text
<?php
include "coolsms.php"
$rest = new rest($api_key, $api_secret);
$response = $rest->send($options);
$result = $response->getResult()
```

#### send \(stdClass $options\)

$options\(stdClass object\) 설정에 따른 문자를 발송합니다.

**Parameters:**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Mandatory</th>
      <th style="text-align:left">Field</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#x39F;</td>
      <td style="text-align:left">&#xC778;&#xC99D;&#xC815;&#xBCF4;</td>
      <td style="text-align:left">&#xC778;&#xC99D;&#xB370;&#xC774;&#xD130;&#xB294; &#xD544;&#xC218;&#xC785;&#xB2C8;&#xB2E4;.
        <a
        href="http://www.coolsms.co.kr/REST_API#Authentication">Authentication</a>&#xCC38;&#xACE0;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">to</td>
      <td style="text-align:left">
        <p>&#xC218;&#xC2E0;&#xBC88;&#xD638; &#xC785;&#xB825; &#xCF64;&#xB9C8;(,)&#xB85C;
          &#xAD6C;&#xBD84;&#xB41C; &#xC218;&#xC2E0;&#xBC88;&#xD638; &#xC785;&#xB825;&#xAC00;&#xB2A5;</p>
        <p>&#xC608;) 01012345678,01023456789,01034567890</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">from</td>
      <td style="text-align:left">&#xBC1C;&#xC2E0;&#xBC88;&#xD638; &#xC608;) 0212345678</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">text</td>
      <td style="text-align:left">&#xBB38;&#xC790;&#xB0B4;&#xC6A9;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">type</td>
      <td style="text-align:left">
        <p>SMS(80&#xBC14;&#xC774;&#xD2B8;), LMS(&#xC7A5;&#xBB38; 2,000&#xBC14;&#xC774;&#xD2B8;),
          MMS(&#xC7A5;&#xBB38;+&#xC774;&#xBBF8;&#xC9C0;) &#xC785;&#xB825; &#xC5C6;&#xC73C;&#xBA74;
          SMS&#xAC00;</p>
        <p>&#xAE30;&#xBCF8; &#xAD6D;&#xAC00;&#xCF54;&#xB4DC;&#xAC00; KR&#xC774; &#xC544;&#xB2C8;&#xBA74;
          SMS&#xB85C; &#xAC15;&#xC81C;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">image</td>
      <td style="text-align:left">&#xC9C0;&#xC6D0;&#xD615;&#xC2DD; : 300KB &#xC774;&#xD558;&#xC758; JPEG,
        PNG, GIF &#xD615;&#xC2DD;&#xC758; &#xD30C;&#xC77C; 2048x2048 &#xD53D;&#xC140;&#xC774;&#xD558;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">image_encoding</td>
      <td style="text-align:left">&#xC774;&#xBBF8;&#xC9C0; &#xC778;&#xCF54;&#xB529; &#xBC29;&#xC2DD; binary(Default),
        base64</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">refname</td>
      <td style="text-align:left">&#xCC38;&#xC870;&#xB0B4;&#xC6A9;(&#xC774;&#xB984;)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">country</td>
      <td style="text-align:left">
        <p>&#xD55C;&#xAD6D;: 82, &#xC77C;&#xBCF8;: 81, &#xC911;&#xAD6D;: 86, &#xBBF8;&#xAD6D;:
          1, &#xAE30;&#xD0C0; &#xB4F1;&#xB4F1; (&#xAE30;&#xBCF8; &#xD55C;&#xAD6D;)</p>
        <p><a href="http://countrycode.org/">http://countrycode.org</a> &#xCC38;&#xACE0;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">datetime</td>
      <td style="text-align:left">
        <p>&#xC608;&#xC57D;&#xC2DC;&#xAC04;&#xC744; YYYYMMDDHHMISS &#xD3EC;&#xB9F7;&#xC73C;&#xB85C;
          &#xC785;&#xB825;</p>
        <p>(&#xC785;&#xB825; &#xC5C6;&#xAC70;&#xB098; &#xC9C0;&#xB09C;&#xB0A0;&#xC9DC;&#xB97C;
          &#xC785;&#xB825;&#xD558;&#xBA74; &#xBC14;&#xB85C; &#xC804;&#xC1A1;)</p>
        <p>&#xC608;) 20131216090510 (2013&#xB144; 12&#xC6D4; 16&#xC77C; 9&#xC2DC;
          5&#xBD84; 10&#xCD08;&#xC5D0; &#xBC1C;&#xC1A1;&#xB418;&#xB3C4;&#xB85D; &#xC608;&#xC57D;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">subject</td>
      <td style="text-align:left">LMS, MMS &#xC77C;&#xB54C; &#xC81C;&#xBAA9; (40&#xBC14;&#xC774;&#xD2B8;)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">charset</td>
      <td style="text-align:left">
        <p>&#xD55C;&#xAE00; &#xC778;&#xCF54;&#xB529; &#xBC29;&#xC2DD; &#xC9C0;&#xC815;
          &#xC720;&#xB2C8;&#xCF54;&#xB4DC; UTF-8 &#xC77C; &#xACBD;&#xC6B0; utf8 &#xC644;&#xC131;&#xD615;
          &#xD55C;&#xAE00;(EUC-KR) &#xC77C; &#xACBD;&#xC6B0;</p>
        <p>euckr &#xC73C;&#xB85C; &#xC785;&#xB825; &#xC785;&#xB825; &#xC5C6;&#xC73C;&#xBA74;
          utf8&#xAC00; &#xAE30;&#xBCF8;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">srk</td>
      <td style="text-align:left">
        <p>&#xC194;&#xB8E8;&#xC158; &#xC81C;&#xACF5; &#xC218;&#xC218;&#xB8CC;&#xB97C;
          &#xC815;&#xC0B0;&#xBC1B;&#xC744; &#xC194;&#xB8E8;&#xC158; &#xB4F1;&#xB85D;&#xD0A4;</p>
        <p>Solution Registration Key(<a href="http://www.coolsms.co.kr/sp">&#xC218;&#xC775; &#xBC30;&#xBD84;&#xD504;&#xB85C;&#xADF8;&#xB7A8; &#xCC38;&#xACE0;</a>)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">mode</td>
      <td style="text-align:left">
        <p>test&#xB85C; &#xC785;&#xB825;&#xD560; &#xACBD;&#xC6B0; CARRIER &#xC2DC;&#xBBAC;&#xB808;&#xC774;&#xD130;&#xB85C;
          &#xC2DC;&#xBBAC;&#xB808;&#xC774;&#xC158;&#xB428; &#xC218;&#xC2E0;&#xBC88;&#xD638;&#xB97C;
          &#xBC18;&#xB4DC;&#xC2DC;</p>
        <p>01000000000 &#xC73C;&#xB85C; &#xD14C;&#xC2A4;&#xD2B8;&#xD558;&#xC138;&#xC694;.
          &#xC608;&#xC57D;&#xD544;&#xB4DC; datetime&#xB294; &#xBB34;&#xC2DC;&#xB428;
          &#xACB0;&#xACFC;&#xAC12;&#xC740;</p>
        <p>60 &#xC794;&#xC561;&#xC5D0;&#xC11C; &#xC2E4;&#xC81C; &#xCC28;&#xAC10;&#xB418;&#xBA70;
          &#xB2E4;&#xC74C;&#xB0A0; &#xC0C8;&#xBCBD;&#xC5D0; &#xC7AC;&#xCDA9;&#xC804;&#xB428;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">extension</td>
      <td style="text-align:left">JSON &#xD3EC;&#xB9F7;&#xC758; &#xAC1C;&#xBCC4; &#xBA54;&#xC2DC;&#xC9C0;&#xB97C;
        &#xB2F4;&#xC744; &#xC218; &#xC788;&#xC74C;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">delay</td>
      <td style="text-align:left">0~20 &#xC0AC;&#xC774;&#xC758; &#xAC12;&#xC73C;&#xB85C; &#xC804;&#xC1A1;&#xC9C0;&#xC5F0;
        &#xC2DC;&#xAC04;&#xC744; &#xC904; &#xC218; &#xC788;&#xC74C;, 1&#xC740;
        &#xC57D; 1&#xCD08; (&#xAE30;&#xBCF8;&#xAC12;&#xC740; 0)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">force_sms</td>
      <td style="text-align:left">
        <p>&#xB204;&#xB9AC;&#xACE0;&#xD478;&#xC2DC;&#xB97C; &#xC0AC;&#xC6A9;&#xD558;&#xB354;&#xB77C;&#xB3C4;
          SMS&#xB85C; &#xBC1C;&#xC1A1;&#xB418;&#xB3C4;&#xB85D; &#xAC15;&#xC81C;</p>
        <p>true &#xD639;&#xC740; false(&#xAE30;&#xBCF8;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">os_platform</td>
      <td style="text-align:left">
        <p>&#xD074;&#xB77C;&#xC774;&#xC5B8;&#xD2B8;&#xC758; OS &#xBC0F; &#xD50C;&#xB7AB;&#xD3FC;
          &#xBC84;&#xC804;) CentOS 6.6</p>
        <p>(v1.5&#xC5D0;&#xC11C; &#xCD94;&#xAC00;&#xB428;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">dev_lang</td>
      <td style="text-align:left">
        <p>&#xAC1C;&#xBC1C; &#xD504;&#xB85C;&#xADF8;&#xB798;&#xBC0D; &#xC5B8;&#xC5B4;
          &#xC608;) PHP 5.3.3</p>
        <p>(v1.5&#xC5D0;&#xC11C; &#xCD94;&#xAC00;&#xB428;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">sdk_version</td>
      <td style="text-align:left">
        <p>SDK &#xBC84;&#xC804; &#xC608;) PHP SDK 1.5</p>
        <p>(v1.5&#xC5D0;&#xC11C; &#xCD94;&#xAC00;&#xB428;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">app_version</td>
      <td style="text-align:left">
        <p>&#xC5B4;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158; &#xBC84;&#xC804; &#xC608;)
          Purplebook 4.1</p>
        <p>(v1.5&#xC5D0;&#xC11C; &#xCD94;&#xAC00;&#xB428;)</p>
      </td>
    </tr>
  </tbody>
</table>

**Returns:**

```text
{
  "recipient_number": "01012345678",
  "group_id": "20120217103829612403761364",
  "result_code": "00",
  "result_message": "Success"
}
```

#### sent \(stdClass $options\)

발송 되었던 문자에 대한 정보를 가져옵니다.

**Parameters:**

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| O | 인증정보 | 인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고 |
|  | count | 문자수 \(기본값 20개\) |
|  | page | 페이지 값 |
|  | s\_rcpt | 발송된 전화번호로 검색 |
|  | s\_start | 보낸 날짜 범위검색할때 시작 일시 설정 |
|  | s\_end | 보낸 날짜 범위검색할때 끝나는 일시 설정 |
|  | s\_status | 메시지상태로 검색 |
|  | s\_resultcode | 전송결과값으로 검색 |
|  | mid | Message ID 로 검색 |
|  | gid | Group ID 로 검색 |

**Returns:**

```text
{
  "total_count":"169",
  "list_count":4,
  "page":1,
  "data":[
    {
      "type":"SMS",
      "accepted_time":"2014-01-07 18:14:54",
      "recipient_number":"01000000000",
      "group_id":"G52CBC596955F0",
      "message_id":"M52CBC59695B31",
      "status":"2",
      "result_code":"58",
      "result_message":"\uc804\uc1a1\uacbd\ub85c \uc5c6\uc74c",
      "sent_time":"201401071814",
      "text":"Test Message"
    }
   ]
}
```

#### balance \(  \)

자신의 계정의 남은 잔액과 포인트를 가져옵니다.

**Parameters: None**

**Returns:**

```text
{
   "cash" : "10000",
   "point" : "4145"
}
```

#### cancel \(stdClass $options\)

예약문자를 취소한다.

**Parameters:**

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| O | mid | Message ID 나 Group ID 둘중에 하나를 넣어야합니다. |
|  | gid |  |

**Returns: None**

#### 발신번호 관련 리소스

#### register \(stdClass $options\)

\* 보안상 문제로 현재는 제공하지 않습니다. 쿨에스엠에스 사이트에서 발신번호를 등록해 주세요

새로운 발신번호를 등록

**Parameters:**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Mandatory</th>
      <th style="text-align:left">Field</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">O</td>
      <td style="text-align:left">phone</td>
      <td style="text-align:left">
        <p>&#xBC1C;&#xC2E0;&#xBC88;&#xD638;</p>
        <p>&#xC608;) 021234567</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">site_user</td>
      <td style="text-align:left">
        <p>&#xC0AC;&#xC774;&#xD2B8; &#xC720;&#xC800; &#xC544;&#xC774;&#xB514; &#xC785;&#xB825;,
          &#xBBF8;&#xC785;&#xB825;&#xC2DC; __private__ &#xC73C;&#xB85C; &#xC124;&#xC815;&#xB429;&#xB2C8;&#xB2E4;.</p>
        <p>&#xC608;) admin</p>
      </td>
    </tr>
  </tbody>
</table>

**Returns:**

```text
{
    "handle_key":"SID55DAD88A7E4EC",
    "ars_number":"01021382269"
}
```

####  

#### verify \(stdClass $options\)

\* 보안상 문제로 현재는 제공하지 않습니다. 쿨에스엠에스 사이트에서 발신번호를 등록해 주세요

발신번호가 제대로 인증되었는지 확인한다.

**Parameters:**

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| O | handle\_key | register 호출 후 리턴받은 핸들값 |

**Returns: None**

#### delete \(stdClass $options\)

발신번호가 제대로 인증되었는지 확인한다.

**Parameters:**

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| O | handle\_key | 발신번호 핸들값 |

**Returns:None** 

#### get\_senderid\_list \(stdClass $options\)

발신번호가 제대로 인증되었는지 확인한다.

**Parameters:**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Mandatory</th>
      <th style="text-align:left">Field</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">site_user</td>
      <td style="text-align:left">
        <p>&#xC0AC;&#xC774;&#xD2B8; &#xC720;&#xC800; &#xC544;&#xC774;&#xB514; &#xC785;&#xB825;,
          &#xBBF8;&#xC785;&#xB825;&#xC2DC; __private__ &#xC73C;&#xB85C; &#xC785;&#xB825;&#xB429;&#xB2C8;&#xB2E4;.</p>
        <p>&#xC608;) admin</p>
      </td>
    </tr>
  </tbody>
</table>

**Returns:**

```text
[
    {"idno":"SID555C89C49627D","phone_number":"0809302266","flag_default":"Y","updatetime":"2015-06-12 10:21:06","regdate":"2015-05-20 22:19:00"},
    {"idno":"SID5568347CC1518","phone_number":"01012345678","flag_default":"N","updatetime":"2015-05-29 18:42:58","regdate":"2015-05-29 18:42:20"}
]
```

####  

#### set\_default \(stdClass $options\)

기본 발신번호를 지정한다.

**Parameters:**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Mandatory</th>
      <th style="text-align:left">Field</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">O</td>
      <td style="text-align:left">handle_key</td>
      <td style="text-align:left">&#xBC1C;&#xC2E0;&#xBC88;&#xD638; &#xD578;&#xB4E4;&#xAC12;&#xC744; &#xC785;&#xB825;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">site_user</td>
      <td style="text-align:left">
        <p>&#xC0AC;&#xC774;&#xD2B8; &#xC720;&#xC800; &#xC544;&#xC774;&#xB514; &#xC785;&#xB825;,
          &#xBBF8;&#xC785;&#xB825;&#xC2DC; __private__ &#xC73C;&#xB85C; &#xC785;&#xB825;&#xB429;&#xB2C8;&#xB2E4;.</p>
        <p>&#xC608;) admin</p>
      </td>
    </tr>
  </tbody>
</table>

**Returns:** 

#### get\_default \(stdClass $options\)

기본 발신번호로 설정된 번호를 가져온다.

**Parameters:**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Mandatory</th>
      <th style="text-align:left">Field</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">site_user</td>
      <td style="text-align:left">
        <p>&#xC0AC;&#xC774;&#xD2B8; &#xC720;&#xC800; &#xC544;&#xC774;&#xB514; &#xC785;&#xB825;,
          &#xBBF8;&#xC785;&#xB825;&#xC2DC; __private__ &#xC73C;&#xB85C; &#xC785;&#xB825;&#xB429;&#xB2C8;&#xB2E4;.</p>
        <p>&#xC608;) admin</p>
      </td>
    </tr>
  </tbody>
</table>

**Returns:**

```text
{
    "handle_key":"SID555C89C49627D",
    "phone_number":"0809302266"
}
```

