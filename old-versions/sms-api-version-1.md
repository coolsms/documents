# SMS API Version 1



## Overview

[REST API 1.0](https://developer.coolsms.co.kr/REST_API_Global) 에 비해 달라진 점은 아래와 같습니다.

1. 누리고 푸시 앱 전송을 지원합니다.
2. 1만건 메시지 전송을 2분에서 20초 이하로 단축.
3. 후불제 회원 지원.
4. 알림톡 지원.

이 문서는 쿨에스엠에스의 REST API를 통하여 문자전송에서부터 전송된 문자의 상태값을 비롯하여 잔액정보 및 예약취소 등의 작업을 요청하는 방법을 기술하고 있습니다. REST API를 기반으로 PHP, Java, Python, Delphi, C 등 다양한 언어로 구현된 SDK 및 예제를  [SDK](https://developer.coolsms.co.kr/SDK_ko) 에서 확인하세요.

모든 Request 호출에는 API Key를 비롯한 인증정보를 포함하여 서버의 인증을 거쳐야 합니다. 인증에 대한 상세한 내용은 [Authentication](https://developer.coolsms.co.kr/REST_API#Authentication) 을 확인하세요.

인증을 위한 API Key 및 API Secret 코드는 [문자메시지 &gt; 환경설정 &gt; API Key 관리](https://www.coolsms.co.kr/credentials) 메뉴에서 발급 및 관리가 가능합니다. [API Key 관리](https://developer.coolsms.co.kr/Man_Credentials) 문서를 참고하세요.

아래는 Resource Url과 간단한 설명을 테이블로 정리하였습니다. 상세한 설명을 보시려면 해당 Resource Url을 클릭하여 주세요.

| Resource | Description |
| :--- | :--- |
| [POST send](https://developer.coolsms.co.kr/SMS_API#POSTsend) | 문자전송 요청 |
| [GET sent](https://developer.coolsms.co.kr/SMS_API#GETsent) | 발송된 문자정보 읽어오기 |
| [POST cancel](https://developer.coolsms.co.kr/SMS_API#POSTcancel) | 예약문자 취소 |
| [GET balance](https://developer.coolsms.co.kr/SMS_API#GETbalance) | 잔액정보 읽어오기 |
| [GET status](https://developer.coolsms.co.kr/SMS_API#GETstatus) | 전송채널 상태 조회 |

※ Request Parameters 입력시 JSON 포맷의 데이터가 아니라 폼데이터임을 유의해 주세요. Response Body의 데이터가 JSON 형식입니다.

요청에 대한 응답의 상세는 [Response](https://developer.coolsms.co.kr/REST_API#Response) 를 확인하세요.

REST API 관련 질의 응답 및 정보 공유는 [개발자포럼](https://developer.coolsms.co.kr/devforum)을 이용해주세요.

## Change Log

<table>
  <thead>
    <tr>
      <th style="text-align:left">Version</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">1.1</td>
      <td style="text-align:left">
        <p>Android &#xB204;&#xB9AC;&#xACE0; &#xD478;&#xC2DC; &#xC9C0;&#xC6D0;
          <br
          />1&#xB9CC;&#xAC74; &#xC804;&#xC1A1;&#xC744; 40&#xCD08; &#xC774;&#xD558;&#xB85C;
          &#xB2E8;&#xCD95;</p>
        <p>&#xD6C4;&#xBD88;&#xC81C; &#xD68C;&#xC6D0; &#xC9C0;&#xC6D0;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">1.2</td>
      <td style="text-align:left">iOS &#xB204;&#xB9AC;&#xACE0; &#xD478;&#xC2DC; &#xC9C0;&#xC6D0;
        <br />1&#xB9CC;&#xAC74; &#xC804;&#xC1A1;&#xC744; 20&#xCD08; &#xC774;&#xD558;&#xB85C;
        &#xB2E8;&#xCD95;</td>
    </tr>
    <tr>
      <td style="text-align:left">1.3</td>
      <td style="text-align:left">&#xCFE8;&#xC11C;&#xD3EC;&#xD130;&#xC988; &#xC815;&#xCC45; &#xC9C0;&#xC6D0;
        &#xBC18;&#xC601;</td>
    </tr>
    <tr>
      <td style="text-align:left">1.4</td>
      <td style="text-align:left">status &#xB9AC;&#xC18C;&#xC2A4;&#xC5D0; &#xC2DC;&#xAC04;&#xBCC4;, &#xC77C;&#xBCC4;
        &#xC804;&#xC1A1;&#xD604;&#xD669;&#xC744; &#xC704;&#xD55C; date, unit &#xD544;&#xB4DC;
        &#xCD94;&#xAC00;</td>
    </tr>
    <tr>
      <td style="text-align:left">1.5</td>
      <td style="text-align:left">Agent &#xC815;&#xBCF4; &#xC804;&#xC1A1;</td>
    </tr>
    <tr>
      <td style="text-align:left">1.6</td>
      <td style="text-align:left">&#xCE74;&#xCE74;&#xC624;&#xD1A1; &#xC54C;&#xB9BC;&#xD1A1; &#xCD94;&#xAC00;(beta)</td>
    </tr>
  </tbody>
</table>

## POST send

문자메시지를 전송 요청합니다. 전송 요청에 대한 Response는 휴대전화까지 전송된 결과가 아닙니다.

### Resource URL

[https://api.coolsms.co.kr/sms/1.5/send](https://api.coolsms.co.kr/sms/1.5/send)

### **Parameters**

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
      <td style="text-align:left">&#xC218;&#xC2E0;&#xBC88;&#xD638; &#xC785;&#xB825; &#xCF64;&#xB9C8;(,)&#xB85C;
        &#xAD6C;&#xBD84;&#xB41C; &#xC218;&#xC2E0;&#xBC88;&#xD638; &#xC785;&#xB825;&#xAC00;&#xB2A5;
        &#xC608;) 01012345678,01023456789,01034567890</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">from</td>
      <td style="text-align:left">&#xBC1C;&#xC2E0;&#xBC88;&#xD638; &#xC608;) 0212345678
        <br />2015/10/16 &#xBC1C;&#xC2E0;&#xBC88;&#xD638; &#xC0AC;&#xC804;&#xB4F1;&#xB85D;&#xC81C;&#xC5D0;
        &#xC758;&#xD574; &#xBC18;&#xB4DC;&#xC2DC; &#xB4F1;&#xB85D;&#xB41C; &#xBC88;&#xD638;&#xB9CC;
        &#xD5C8;&#xC6A9;&#xB429;&#xB2C8;&#xB2E4;. (&#xD574;&#xC678;&#xBB38;&#xC790;
        &#xC81C;&#xC678;)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">text</td>
      <td style="text-align:left">&#xBB38;&#xC790;&#xB0B4;&#xC6A9;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">type</td>
      <td style="text-align:left">SMS(90&#xBC14;&#xC774;&#xD2B8;), LMS(&#xC7A5;&#xBB38; 2,000&#xBC14;&#xC774;&#xD2B8;),
        MMS(&#xC7A5;&#xBB38;+&#xC774;&#xBBF8;&#xC9C0;), ATA(&#xC54C;&#xB9BC;&#xD1A1;)
        <br
        />&#xC785;&#xB825; &#xC5C6;&#xC73C;&#xBA74; SMS&#xAC00; &#xAE30;&#xBCF8;
        <br
        />&#xAD6D;&#xAC00;&#xCF54;&#xB4DC;&#xAC00; 82&#xAC00; &#xC544;&#xB2C8;&#xBA74;
        SMS&#xB85C; &#xAC15;&#xC81C;</td>
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
        <p>&#xC785;&#xB825; &#xC5C6;&#xAC70;&#xB098; &#xC9C0;&#xB09C;&#xB0A0;&#xC9DC;&#xB97C;
          &#xC785;&#xB825;&#xD558;&#xBA74; &#xBC14;&#xB85C; &#xC804;&#xC1A1;
          <br />&#xC608;) 20131216090510 (2013&#xB144; 12&#xC6D4; 16&#xC77C; 9&#xC2DC;
          5&#xBD84; 10&#xCD08;&#xC5D0; &#xBC1C;&#xC1A1;&#xB418;&#xB3C4;&#xB85D; &#xC608;&#xC57D;)</p>
        <p>( &#xC54C;&#xB9BC;&#xD1A1;, &#xCE5C;&#xAD6C;&#xD1A1;&#xC740; &#xC9C0;&#xC6D0;&#xC774;
          &#xC548;, API v2&#xC774;&#xC0C1;&#xC5D0;&#xC11C; &#xC0AC;&#xC6A9; &#xAC00;&#xB2A5;&#xD569;&#xB2C8;&#xB2E4;.
          )</p>
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
      <td style="text-align:left">&#xD55C;&#xAE00; &#xC778;&#xCF54;&#xB529; &#xBC29;&#xC2DD; &#xC9C0;&#xC815;
        &#xC720;&#xB2C8;&#xCF54;&#xB4DC; UTF-8 &#xC77C; &#xACBD;&#xC6B0; utf8 &#xC644;&#xC131;&#xD615;
        &#xD55C;&#xAE00;(EUC-KR) &#xC77C; &#xACBD;&#xC6B0; euckr &#xC73C;&#xB85C;
        &#xC785;&#xB825;
        <br />&#xC785;&#xB825; &#xC5C6;&#xC73C;&#xBA74; utf8&#xAC00; &#xAE30;&#xBCF8;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">srk</td>
      <td style="text-align:left">&#xC194;&#xB8E8;&#xC158; &#xC81C;&#xACF5; &#xC218;&#xC218;&#xB8CC;&#xB97C;
        &#xC815;&#xC0B0;&#xBC1B;&#xC744; &#xC194;&#xB8E8;&#xC158; &#xB4F1;&#xB85D;&#xD0A4;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">mode</td>
      <td style="text-align:left">test&#xB85C; &#xC785;&#xB825;&#xD560; &#xACBD;&#xC6B0; CARRIER &#xC2DC;&#xBBAC;&#xB808;&#xC774;&#xD130;&#xB85C;
        &#xC2DC;&#xBBAC;&#xB808;&#xC774;&#xC158;&#xB428; &#xC218;&#xC2E0;&#xBC88;&#xD638;&#xB97C;
        &#xBC18;&#xB4DC;&#xC2DC; 01000000000 &#xC73C;&#xB85C; &#xD14C;&#xC2A4;&#xD2B8;&#xD558;&#xC138;&#xC694;.
        &#xC608;&#xC57D;&#xD544;&#xB4DC; datetime&#xB294; &#xBB34;&#xC2DC;&#xB428;
        &#xACB0;&#xACFC;&#xAC12;&#xC740; 60 &#xC794;&#xC561;&#xC5D0;&#xC11C; &#xC2E4;&#xC81C;
        &#xCC28;&#xAC10;&#xB418;&#xBA70; &#xB2E4;&#xC74C;&#xB0A0; &#xC0C8;&#xBCBD;&#xC5D0;
        &#xC7AC;&#xCDA9;&#xC804;&#xB428;</td>
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
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">sender_key</td>
      <td style="text-align:left">&#xC54C;&#xB9BC;&#xD1A1; Sender Key &#xC785;&#xB825;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">template_code</td>
      <td style="text-align:left">&#xC54C;&#xB9BC;&#xD1A1; &#xD15C;&#xD50C;&#xB9BF; &#xCF54;&#xB4DC; &#xC785;&#xB825;</td>
    </tr>
  </tbody>
</table>

Mandatory가 Ο 인 필드는 반드시 입력하여야 합니다.

srk 는 앱아이디를 말하는 것으로 [https://www.coolsms.co.kr/my\_app\_list](https://www.coolsms.co.kr/my_app_list) 을 참고하세요.

type, to, from, text, subject 등의 필드값을 개별적으로 다른 값으로 발송하고자 할 때 JSON형식으로 extension 포맷을 사용할 수 있습니다.

한번의 Request에 extension을 포함하여 총 받는사람\(to\) 수는 1000개 까지가 제한이며 1000개가 넘을 경우 오류를 발생시킵니다. \(RecipientsTooMany\)

한번의 Request의 총 크기는 2MB를 넘을 수 없습니다. \(오류코드 미정\)

#### extension 포맷

```text
[
	{
		"type": "SMS",
		"to": "01000000000,01011111111,01022222222",
		"text": "Hello A"
	},
	{
		"type": "LMS",
		"to": "01000000000,01011111111,01022222222",
		"subject": "LMS Subject",
		"text": "Hello B"
	},
	{
		"type": "MMS",
		"to": "01000000000,01011111111,01022222222",
		"subject": "MMS Subject",
		"text": "Hello C",
	}
]
```

type, country, to, from, datetime, text, subject, delay 가 올 수 있고 입력하지 않는 필드는 상위\(기본 필드\) 값을 상속 받아 사용됩니다. 단, to는 상속받지 아니하고 필수 입력 사항입니다.

#### 발송형태에 따른 제한사항

이동통신사 내부적으로 완성형한글로 변환되므로 영어 1바이트, 한글 2바이트로 취급됩니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xAD6C;&#xBD84;</th>
      <th style="text-align:left">&#xC81C;&#xD55C;&#xC0AC;&#xD56D;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">SMS</td>
      <td style="text-align:left">90&#xBC14;&#xC774;&#xD2B8; &#xAE4C;&#xC9C0; &#xC804;&#xC1A1;&#xAC00;&#xB2A5;
        (&#xD55C;&#xAE00; 45&#xC790;)</td>
    </tr>
    <tr>
      <td style="text-align:left">LMS</td>
      <td style="text-align:left">2,000&#xBC14;&#xC774;&#xD2B8; &#xAE4C;&#xC9C0; &#xC804;&#xC1A1;&#xAC00;&#xB2A5;
        (&#xD55C;&#xAE00; 1,000&#xC790;)</td>
    </tr>
    <tr>
      <td style="text-align:left">MMS</td>
      <td style="text-align:left">
        <p>2,000&#xBC14;&#xC774;&#xD2B8; &#xD14D;&#xC2A4;&#xD2B8; (&#xD55C;&#xAE00;
          1,000&#xC790;)</p>
        <p>1&#xAC1C;&#xC758; &#xC774;&#xBBF8;&#xC9C0; &#xC804;&#xC1A1; (300KB. 2048x2048&#xD53D;&#xC140;
          &#xC774;&#xD558;&#xC778; JPEG, PNG, GIF &#xD615;&#xC2DD; &#xD30C;&#xC77C;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">ATA</td>
      <td style="text-align:left">&#xCE74;&#xCE74;&#xC624;&#xD1A1; &#xC54C;&#xB9BC;&#xD1A1;&#xC73C;&#xB85C;
        1,000&#xC790;&#xAE4C;&#xC9C0; &#xBC1C;&#xC1A1;
        <br />&#xC774;&#xBBF8;&#xC9C0; &#xCCA8;&#xBD80; &#xBD88;&#xAC00;</td>
    </tr>
  </tbody>
</table>

###  

### **Example**

```text
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<?php
$api_key = 'NCS52A57F48C3D32';
$api_secret = '5AC44E03CE8E7212D9D1AD9091FA9966';
$timestamp = time();
$salt = uniqid();
$data = strval($timestamp) . $salt;
$signature = hash_hmac('md5', $data, $api_secret);
?>
<html lang="ko" xml:lang="ko" xmlns="http://www.w3.org/1999/xhtml">
	<head>
    	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
	</head>
	<body>
		<form method="post" action="https://api.coolsms.co.kr/sms/1.5/send" enctype="multipart/form-data">
			API Key: <input type="text" name="api_key" value="<?php echo $api_key ?>" /><br />
			Timestame: <input type="text" name="timestamp" value="<?php echo $timestamp ?>" /><br />
			Salt: <input type="text" name="salt" value="<?php echo $salt ?>" /><br />
			Signature: <input type="text" name="signature" value="<?php echo $signature ?>" /><br />
			To: <input type="text" name="to" value="01000000000" /><br />
			From: <input type="text" name="from" value="01000000000" /><br />
			Subject: <input type="text" name="subject" value="TEST" /><br />
			Text: <textarea name="text">HELLO COOLSMS~!</textarea><br />
			Type: <select name="type"><option value="SMS">SMS</option><option value="LMS">LMS</option><option value="MMS">MMS</option></select><br />
			Image: <input type="file" name="image" /><br />
			<input type="submit" value="Submit" />
		</form>
	</body>
</html>
```

### **Response**

서버는 json 포맷으로 접수결과를 리턴합니다.

```text
{
  "group_id": "20120217103829612403761364",
  "success_count": 2,
  "error_count": 0,
  "result_code": "00",
  "result_message": "Success"
}
```

result\_code 가 00 이면 정상적인 접수이며 이 외의 코드는 [http://www.coolsms.co.kr/Legacy\_Result\_Codes](http://www.coolsms.co.kr/Legacy_Result_Codes) 을 참고하세요. 여기서 리턴되는 Response의 내용은 서버에게 전송을 요청한 것에 대한 정보이지 실제 휴대전화로 전송한 것에 대한 정보가 아닙니다. 예를 들어 요청 건수 중 success\_count가 10개라면 서버의 DB에 안전하게 INSERT된 건이 10개라는 의미이며, 나중 sent 리소스를 통해 조회시 이통사를 통해 실제 전송성공된 건수는 8개이고 올바르지 못한 수신번호로 2개로 실패라는 결과가 나올 수 있습니다.

메시지그룹ID\(group\_id\)는 Request된 메시지들의대표하는 아이디값으로 메시지상태 및 예약취소할 때 키값으로 사용될 수 있습니다. 10건의 문자메시지를 발송할 경우 그 10건의 문자메시지를 대표하는 group\_id 가 리턴되며 sent 리소스를 통해서 10건에 대한 전송상태를 조회할 수 있습니다.

## GET sent

발송된 문자메시지의 목록을 가져옵니다. 

### Resource Url

[https://api.coolsms.co.kr/sms/1.5/sent](https://api.coolsms.co.kr/sms/1.5/sent)

### Parameters

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| Ο | 인증정보 | 인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고 |
|  | count | 기본값 20이며 20개의 목록을 받을 수 있음. 40입력시 40개의 목록이 리턴 |
|  | page | 1부터 시작하는 페이지값 |
|  | rcpt | 수신번호로 검색 |
|  | start | 검색 시작일시 접수 날짜와 시간으로 검색 YYYY-MM-DD HH:MI:SS 포맷의 날짜와 시간 |
|  | end | 검색 종료일시 접수 날짜와 시간으로 검색 YYYY-MM-DD HH:MI:SS 포맷의 날짜와 시간 |
|  | status | 메시지 상태 값으로 검색 |
|  | resultcode | 전송결과 값으로 검색 |
|  | notin\_resultcode | 입력된 전송결과 값 이외의 건들만 조회 |
|  | mid | 메시지ID |
|  | gid | 그룹ID |

검색 옵션이 없는 경우 가장 최신의 발송건부터 20일 전까지 내림차순으로 페이지 단위의 목록을 리턴합니다.

### Example

```text
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<?php
$api_key = 'NCS52A57F48C3D32';
$api_secret = '5AC44E03CE8E7212D9D1AD9091FA9966';
$timestamp = time();
$salt = uniqid();
$data = strval($timestamp) . $salt;
$signature = hash_hmac('md5', $data, $api_secret);
?>
<html lang="ko" xml:lang="ko" xmlns="http://www.w3.org/1999/xhtml">
	<head>
    	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
	</head>
	<body>
		<form method="get" action="https://api.coolsms.co.kr/sms/1.5/sent" enctype="multipart/form-data">
			API Key: <input type="text" name="api_key" value="<?php echo $api_key ?>" /><br />
			Timestame: <input type="text" name="timestamp" value="<?php echo $timestamp ?>" /><br />
			Salt: <input type="text" name="salt" value="<?php echo $salt ?>" /><br />
			Signature: <input type="text" name="signature" value="<?php echo $signature ?>" /><br />
			List Count : <input type="text" name="count" value="20" /><br />
			Page: <input type="text" name="page" value="1" /><br />
			<input type="submit" value="Submit" />
		</form>
	</body>
</html>
```

### **Response**

Response Format은 json을 사용합니다.

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
      "text":"Test Message",
      "carrier":"SKT",
      "scheduled_time":""
    },
    {
      "type":"SMS",
      "accepted_time":"2014-01-07 18:14:41",
      "recipient_number":"01000000000",
      "group_id":"G52CBC5897645A",
      "message_id":"M52CBC58976A64",
      "status":"2",
      "result_code":"58",
      "result_message":"\uc804\uc1a1\uacbd\ub85c \uc5c6\uc74c",
      "sent_time":"201401071814",
      "text":"message\nhere",
      "carrier":"KTF",
      "scheduled_time":"20160401000000"
    },
    {
      "type":"SMS",
      "accepted_time":"2014-01-07 18:11:23",
      "recipient_number":"01000000000",
      "group_id":"G52CBC4C35B3A8",
      "message_id":"M52CBC4C35BA70",
      "status":"2",
      "result_code":"58",
      "result_message":"\uc804\uc1a1\uacbd\ub85c \uc5c6\uc74c",
      "sent_time":"201401071811",
      "text":"message\nhere",
      "carrier":"LGT",
      "scheduled_time":""
    },
    {
      "type":"SMS",
      "accepted_time":"2014-01-06 12:42:32",
      "recipient_number":"01012345678",
      "group_id":"G52CA262EC447D",
      "message_id":"M52CA262EC49D8",
      "status":"2",
      "result_code":"00",
      "result_message":"\uc815\uc0c1",
      "sent_time":"201401061257",
      "text":"\ud14c\uc2a4\ud305hi there~",
      "carrier":"KTF",
      "scheduled_time":""
    }
  ]
}
```

#### status

| Status Code | Description |
| :--- | :--- |
| 0 | 대기중 |
| 1 | 이통사로 전송중 |
| 2 | 이통사로부터 리포트 도착 |

result\_code 는 [http://www.coolsms.co.kr/Legacy\_Result\_Codes](http://www.coolsms.co.kr/Legacy_Result_Codes) 페이지를 참고 하세요.

## POST cancel

예약된 문자메시지를 취소합니다. 예약되지 않았거나, 예약되었으나 이미 발송된 문자메시지는 취소 할 수 없습니다.

### **Resource URL**

[https://api.coolsms.co.kr/sms/1.5/cancel](https://api.coolsms.co.kr/sms/1.5/cancel)

### **Parameters**

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| Ο | 인증정보 | 인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고 |
|  | mid | 메시지ID |
|  | gid | 그룹ID |

mid 혹은 gid 중 하나는 반드시 입력하세요.

## GET balance

잔액을 확인합니다.

### Resource URL

[https://api.coolsms.co.kr/sms/1.5/balance](https://api.coolsms.co.kr/sms/1.5/balance)

### **Parameters**

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| Ο | 인증정보 | 인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고 |

### Response

Response Format은 json을 사용합니다.

```text
{
  "cash": "23900",
  "point": "890"
}
```

## GET status

전송채널의 상태를 조회합니다.

### Resource Url

[https://api.coolsms.co.kr/sms/1.5/status](https://api.coolsms.co.kr/sms/1.5/status)

### Parameters

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
      <td style="text-align:left">count</td>
      <td style="text-align:left">&#xAE30;&#xBCF8;&#xAC12; 1&#xC774;&#xBA70; 1&#xAC1C;&#xC758; &#xCD5C;&#xC2E0;&#xC758;
        &#xB808;&#xCF54;&#xB4DC;&#xB97C; &#xBC1B;&#xC744; &#xC218; &#xC788;&#xC74C;,
        10&#xC785;&#xB825;&#xC2DC; 10&#xBD84; &#xB3D9;&#xC548;&#xC758; &#xB808;&#xCF54;&#xB4DC;
        &#xBAA9;&#xB85D;&#xC744; &#xB9AC;&#xD134;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">unit</td>
      <td style="text-align:left">minute(default), hour, day &#xC911; &#xD558;&#xB098;
        <br />minute : &#xBD84; &#xB2E8;&#xC704;&#xC758; &#xD604;&#xD669;
        <br />hour : &#xC2DC;&#xAC04; &#xB2E8;&#xC704;&#xC758; &#xD3C9;&#xADE0;
        <br />day : &#xC77C; &#xB2E8;&#xC704;&#xC758; &#xD3C9;&#xADE0;
        <br />(v1.4&#xC5D0;&#xC11C; &#xCD94;&#xAC00;)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">date</td>
      <td style="text-align:left">
        <p>&#xB370;&#xC774;&#xD130;&#xB97C; &#xC77D;&#xC5B4;&#xC624;&#xB294; &#xAE30;&#xC900;
          &#xC2DC;&#xAC01;&#xC73C;&#xB85C; YYYYMMDDHHMISS &#xD615;&#xC2DD;&#xC758;
          14&#xC790;&#xB9AC; &#xAC12;
          <br />&#xC608;) 20150331095101 (2015&#xB144; 3&#xC6D4; 31&#xC77C; &#xC624;&#xC804;
          9&#xC2DC; 51&#xBD84; 1&#xCD08;)
          <br />&#xAE30;&#xBCF8;&#xAC12; : &#xD604;&#xC7AC;&#xC2DC;&#xAC01;</p>
        <p>(v1.4&#xC5D0;&#xC11C; &#xCD94;&#xAC00;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">channel</td>
      <td style="text-align:left">
        <p>1: 1&#xAC74; &#xBC1C;&#xC1A1; &#xCC44;&#xB110; (&#xAE30;&#xBCF8; &#xAC12;)</p>
        <p>2: &#xB300;&#xB7C9; &#xBC1C;&#xC1A1; &#xCC44;&#xB110;
          <br />(v1.4&#xC5D0;&#xC11C; &#xCD94;&#xAC00;)</p>
      </td>
    </tr>
  </tbody>
</table>

### Response

모든 항목의 값은 초단위\(seconds\)값입니다. sms\_average와 mms\_average는 각각 SMS채널과 MMS채널의 문자가 접수된 때부터 실제 수신되기까지 걸린 시간으로 계산된 평균값으로 리포트가 오지않은 대기중인 메시지를 합산한 값이므로 다소 높게 나와도 정상입니다. sk, kt, lg 의 경우 수신시각이 분단위로만 제공되어서 약간의 차이가 날 수 있습니다.

```text
[
  {
    'registdate': '2014-02-25 10:34:01',
    'sms_average': '23',
    'sms_sk_average': '9',
    'sms_kt_average': '10',
    'sms_lg_average': '11',
    'mms_average': '52',
    'mms_sk_average': '20',
    'mms_kt_average': '25',
    'mms_lg_average': '36'
  }
]
```

## [메시지 상태 코드](https://support.coolsms.co.kr/hc/ko/articles/115009267167-%EA%B2%B0%EA%B3%BC-%EC%BD%94%EB%93%9C-%EB%B0%8F-%EC%83%81%ED%83%9C-%EC%BD%94%EB%93%9C)

| CODE | 설 명 |
| :--- | :--- |
| 00 | 정상\(전송완료\) |
| 10 | 잘못된 번호 |
| 11 | 상위 서비스망 스팸 인식됨 |
| 12 | 상위 서버 오류 |
| 13 | 잘못된 필드값 |
| 20 | 등록된 계정이 아니거나 패스워드가 틀림 |
| 21 | 존재하지 않는 메시지 ID |
| 30 | 가능한 전송 잔량이 없음 |
| 31 | 전송할 수 없음 |
| 32 | 가입자 없음 |
| 40 | 전송시간 초과 |
| 41 | 단말기 busy |
| 42 | 음영지역 |
| 43 | 단말기 Power off |
| 44 | 단말기 메시지 저장갯수 초과 |
| 45 | 단말기 일시 서비스 정지 |
| 46 | 기타 단말기 문제 |
| 47 | 착신거절 |
| 48 | Unkown error |
| 49 | Format Error |
| 50 | SMS서비스 불가 단말기 |
| 51 | 착신측의 호불가 상태 |
| 52 | 이통사 서버 운영자 삭제 |
| 53 | 서버 메시지 Que Full |
| 54 | SPAM |
| 55 | SPAM, nospam.or.kr 에 등록된 번호 |
| 56 | 전송실패\(무선망단\) |
| 57 | 전송실패\(무선망-&gt;단말기단\) |
| 58 | 전송경로 없음 |
| 60 | 예약취소 |
| 70 | 허가되지 않은 IP주소 |
| 81 | 게이트웨이 연결 실패 |
| 82 | 이미지 미입력 |
| 83 | 수신번호 미입력 |
| 84 | 발신번호 미입력 |
| 85 | 메시지 내용 미입력 |
| 86 | 미지원 이미지 타입 |
| 99 | 전송대기 |

