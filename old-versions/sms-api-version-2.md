# SMS API Version 2



## Overview

이 문서는 REST기반의 문자메시지\(국내,해외문자,알림톡,친구톡\) API로 예약 문자를 포함한 문자전송, 전송된 문자의 상태 확인, 잔액정보 및 예약취소 등의 작업을 요청하는 방법을 기술하고 있습니다. PHP, Java, Python, Delphi, C 등 다양한 언어로 구현된 샘플을 [SDK](https://developer.coolsms.co.kr/SDK_ko) 페이지에서 제공하고 있습니다..

모든 Request 호출에는 API Key를 비롯한 인증정보를 포함하여 서버의 인증을 거쳐야 합니다. 인증에 대한 상세한 내용은 [Authentication](https://developer.coolsms.co.kr/REST_API#Authentication) 을 확인하세요.

인증을 위한 API Key 및 API Secret 코드는 [문자메시지 &gt; 환경설정 &gt; API Key 관리](https://www.coolsms.co.kr/credentials) 메뉴에서 발급 및 관리가 가능합니다. [API Key 관리](https://developer.coolsms.co.kr/Man_Credentials) 문서를 참고하세요.

아래는 각 Resource의 역할을 테이블로 정리하였습니다. 상세한 설명을 보시려면 해당 Resource를 클릭하여 주세요.

| Part | Resource | Description |
| :--- | :--- | :--- |
| 그룹메시지 | [GET new\_group](https://developer.coolsms.co.kr/SMS_API_v2#GETnew_group) | 그룹 생성 |
| [GET group\_list](https://developer.coolsms.co.kr/SMS_API_v2#GETgroup_list) | 그룹 목록 |  |
| [POST delete\_groups](https://developer.coolsms.co.kr/SMS_API_v2#POSTdelete_groups) | 그룹 삭제 |  |
| [GET groups/{group\_id}](https://developer.coolsms.co.kr/SMS_API_v2#GETgroupsgroup_id) | 그룹 정보 리턴 |  |
| [POST groups/{group\_id}/add\_messages](https://developer.coolsms.co.kr/SMS_API_v2#POSTgroupsgroup_idadd_messages) | 메시지 추가 |  |
| [POST groups/{group\_id}/add\_messages.json](https://developer.coolsms.co.kr/SMS_API_v2#POSTgroupsgroup_idadd_messagesjson) | JSON형식으로  메시지 추가 |  |
| [GET groups/{group\_id}/message\_list](https://developer.coolsms.co.kr/SMS_API_v2#GETgroupsgroup_idmessage_list) | 추가된 메시지 목록 |  |
| [GET groups/{group\_id}/delete\_messages](https://developer.coolsms.co.kr/SMS_API_v2#POSTgroupsgroup_iddelete_messages) | 메시지 삭제 |  |
| [POST groups/{group\_id}/send](https://developer.coolsms.co.kr/SMS_API_v2#POSTgroupsgroup_idsend) | 메시지 발송 |  |
| 이미지 | [POST upload\_image](https://developer.coolsms.co.kr/SMS_API_v2#POSTupload_image) | 이미지 업로드 |
| [GET image\_list](https://developer.coolsms.co.kr/SMS_API_v2#GETimage_list) | 이미지 목록 |  |
| [GET images/{image\_id}](https://developer.coolsms.co.kr/SMS_API_v2#GETimagesimage_id) | 이미지 정보 |  |
| [POST delete\_images](https://developer.coolsms.co.kr/SMS_API_v2#POSTdelete_images) | 이미지  |  |
| 기타 | [POST send](https://developer.coolsms.co.kr/SMS_API_v2#POSTsend) | 문자발송 요청 |
| [GET sent](https://developer.coolsms.co.kr/SMS_API_v2#GETsent) | 발송된 문자정보 조회 |  |
| [POST cancel](https://developer.coolsms.co.kr/SMS_API_v2#POSTcancel) | 예약문자 취소 |  |
| [GET balance](https://developer.coolsms.co.kr/SMS_API_v2#GETbalance) | 전액정보 조회 |  |
| [GET status](https://developer.coolsms.co.kr/SMS_API_v2#GETstatus) | 전송채널 상태 조회 |  |

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
      <td style="text-align:left">&#xCE74;&#xCE74;&#xC624; &#xC54C;&#xB9BC;&#xD1A1; &#xAE30;&#xB2A5; &#xCD94;&#xAC00;</td>
    </tr>
    <tr>
      <td style="text-align:left">2.0</td>
      <td style="text-align:left">&#xADF8;&#xB8F9; &#xBA54;&#xC2DC;&#xC9D5; &#xCD94;&#xAC00;</td>
    </tr>
  </tbody>
</table>

## 그룹메시지

대용량의 메시지를 안전하고 빠르게 전송하도록 그룹메시지를 위한 API를 제공합니다.  
아래의 API 호출 흐름으로 대량의 그룹메시지를 보낼 수 있습니다.

```text
new_group  ->  add_messages  ->  send
```

new\_group 호출로 메시지를 담을 그룹을 생성하고 리턴된 그룹아이디를 키로 add\_messages 호출로 메시지를 접수하고 send 호출로 접수된 메시지를 서버단에 전송을 수행합니다. 이로 인해 한번 접수된 메시지는 유실 없이 안정적으로 발송이 보장됩니다. 

### GET new\_group

메시지를 담을 그룹을 생성하여 그룹아이디를 리턴합니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/new\_group](https://api.coolsms.co.kr/sms/2/new_group)

#### Parameters

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
        href="https://developer.coolsms.co.kr/REST_API#Authentication">Authentication</a>&#xCC38;&#xACE0;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">charset</td>
      <td style="text-align:left">&#xD55C;&#xAE00; &#xC778;&#xCF54;&#xB529; &#xBC29;&#xC2DD;&#xC744; &#xC9C0;&#xC815;&#xD569;&#xB2C8;&#xB2E4;.
        <br
        />&#xC720;&#xB2C8;&#xCF54;&#xB4DC; UTF-8 &#xC77C; &#xACBD;&#xC6B0; utf8,
        <br
        />&#xC644;&#xC131;&#xD615; &#xD55C;&#xAE00;(EUC-KR) &#xC77C; &#xACBD;&#xC6B0;
        euckr &#xC73C;&#xB85C; &#xC785;&#xB825;,
        <br />&#xC785;&#xB825; &#xC5C6;&#xC73C;&#xBA74; utf8&#xAC00; &#xAE30;&#xBCF8;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">srk</td>
      <td style="text-align:left">&#xC194;&#xB8E8;&#xC158; &#xC81C;&#xACF5; &#xC218;&#xC218;&#xB8CC;&#xB97C;
        &#xC815;&#xC0B0;&#xBC1B;&#xC744; &#xC194;&#xB8E8;&#xC158; &#xB4F1;&#xB85D;&#xD0A4;
        <br
        />&#xC790;&#xC138;&#xD55C; &#xC548;&#xB0B4;&#xB294; <a href="http://www.coolsms.co.kr/sp">http://www.coolsms.co.kr/sp</a> &#xC744;
        &#xCC38;&#xACE0;&#xD558;&#xC138;&#xC694;.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">mode (&#xD604;&#xC7AC; &#xBBF8;&#xC9C0;&#xC6D0;)</td>
      <td style="text-align:left">
        <p>test&#xB85C; &#xC785;&#xB825;&#xD560; &#xACBD;&#xC6B0; CARRIER &#xC2DC;&#xBBAC;&#xB808;&#xC774;&#xD130;&#xB85C;
          &#xC2DC;&#xBBAC;&#xB808;&#xC774;&#xC158;&#xB429;&#xB2C8;&#xB2E4;.</p>
        <p>** &#xC218;&#xC2E0;&#xBC88;&#xD638;&#xB97C; &#xBC18;&#xB4DC;&#xC2DC; 01000000000
          &#xC73C;&#xB85C; &#xD14C;&#xC2A4;&#xD2B8; **
          <br />&#xC608;&#xC57D;&#xD544;&#xB4DC; datetime&#xB294; &#xBB34;&#xC2DC;&#xB429;&#xB2C8;&#xB2E4;.</p>
        <p>&#xACB0;&#xACFC;&#xAC12;&#xC740; 60 &#xC794;&#xC561;&#xC5D0;&#xC11C; &#xC2E4;&#xC81C;
          &#xCC28;&#xAC10;&#xB418;&#xBA70; &#xB2E4;&#xC74C;&#xB0A0; &#xC0C8;&#xBCBD;&#xC5D0;
          &#xC7AC;&#xCDA9;&#xC804;&#xB429;&#xB2C8;&#xB2E4;.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">force_sms (&#xD604;&#xC7AC; &#xBBF8;&#xC9C0;&#xC6D0;)</td>
      <td style="text-align:left">
        <p>&#xB204;&#xB9AC;&#xACE0;&#xD478;&#xC2DC;&#xB97C; &#xC0AC;&#xC6A9;&#xD558;&#xB354;&#xB77C;&#xB3C4;
          &#xAC15;&#xC81C;&#xB85C; &#xBB38;&#xC790; &#xBC1C;&#xC1A1;.</p>
        <p>true &#xD639;&#xC740; false(&#xAE30;&#xBCF8;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">only_</td>
      <td style="text-align:left">&#xC54C;&#xB9BC;&#xD1A1;&#xC774; &#xC2E4;&#xD328;&#xD574;&#xB3C4; &#xBB38;&#xC790;&#xBA54;&#xC2DC;&#xC9C0;&#xB85C;
        &#xB300;&#xCCB4;&#xD558;&#xC5EC; &#xBC1C;&#xC1A1;&#xD558;&#xC9C0; &#xC54A;&#xC2B5;&#xB2C8;&#xB2E4;.
        <br
        />true &#xD639;&#xC740; false(&#xAE30;&#xBCF8;)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">site_user</td>
      <td style="text-align:left">
        <p>API&#xB97C; &#xD638;&#xCD9C;&#xD558;&#xB294; &#xC0AC;&#xC774;&#xD2B8;&#xC5D0;&#xC11C;
          &#xAD00;&#xB9AC;&#xD558;&#xB294; &#xC720;&#xC800; &#xC544;&#xC774;&#xB514;
          &#xC785;&#xB825;.</p>
        <p>&#xBBF8;&#xC785;&#xB825;&#xC2DC; __private__ &#xC73C;&#xB85C; &#xC785;&#xB825;&#xB429;&#xB2C8;&#xB2E4;.
          <br
          />&#xD574;&#xB2F9; &#xC544;&#xC774;&#xB514; &#xC55E;&#xC73C;&#xB85C; &#xB4F1;&#xB85D;&#xB41C;
          &#xBC1C;&#xC2E0;&#xBC88;&#xD638;&#xB97C; &#xD655;&#xC778;&#xD569;&#xB2C8;&#xB2E4;.
          <br
          />&#xBC1C;&#xC2E0;&#xBC88;&#xD638; &#xB4F1;&#xB85D; API&#xB97C; &#xCC38;&#xACE0;&#xD558;&#xC138;&#xC694;.
          <br
          /><a href="http://developer.coolsms.co.kr/SenderID_API">http://developer.coolsms.co.kr/SenderID_API</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">os_platform</td>
      <td style="text-align:left">
        <p>&#xD074;&#xB77C;&#xC774;&#xC5B8;&#xD2B8;&#xC758; OS &#xBC0F; &#xD50C;&#xB7AB;&#xD3FC;
          &#xBC84;&#xC804;</p>
        <p>&#xC608;) CentOS 6.6</p>
        <p>(v1.5&#xC5D0;&#xC11C; &#xCD94;&#xAC00;&#xB428;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">dev_lang</td>
      <td style="text-align:left">
        <p>&#xAC1C;&#xBC1C; &#xD504;&#xB85C;&#xADF8;&#xB798;&#xBC0D; &#xC5B8;&#xC5B4;</p>
        <p>&#xC608;) PHP 5.3.3</p>
        <p>(v1.5&#xC5D0;&#xC11C; &#xCD94;&#xAC00;&#xB428;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">sdk_version</td>
      <td style="text-align:left">
        <p>SDK &#xBC84;&#xC804;</p>
        <p>&#xC608;) PHP SDK 1.5</p>
        <p>(v1.5&#xC5D0;&#xC11C; &#xCD94;&#xAC00;&#xB428;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">app_version</td>
      <td style="text-align:left">
        <p>&#xC5B4;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158; &#xBC84;&#xC804;</p>
        <p>&#xC608;) Purplebook 4.1</p>
        <p>(v1.5&#xC5D0;&#xC11C; &#xCD94;&#xAC00;&#xB428;)</p>
      </td>
    </tr>
  </tbody>
</table>

#### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| O | group\_id | 그룹 아이디 |

#### Example Request

```text
curl -XGET 'https://api.coolsms.co.kr/sms/2/new_group?api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125'
```

#### Example Response

```text
{
  "group_id":"565ba3d7d216a"
}
```

### GET group\_list

생성된 그룹 목록을 리턴합니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/group\_list](https://api.coolsms.co.kr/sms/2/group_list)

#### Parameters

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| Ο | 인증정보 | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST_API#Authentication) 참고 |

#### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| O | - | array 형식의 그룹아이디 목록 리턴 |

#### Example Request

```text
curl -XGET 'https://api.coolsms.co.kr/sms/2/group_list?api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125'
```

#### Example Response

```text
[
    "565ba3d7d216a",
    "565ba3dea161b"
]
```

### POST delete\_groups

그룹을 삭제합니다. 담겨 있는 메시지도 함께 삭제됩니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/delete\_groups](https://api.coolsms.co.kr/sms/2/delete_groups)

#### Parameters

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
        href="https://developer.coolsms.co.kr/REST_API#Authentication">Authentication</a>&#xCC38;&#xACE0;</td>
    </tr>
    <tr>
      <td style="text-align:left">O</td>
      <td style="text-align:left">group_ids</td>
      <td style="text-align:left">
        <p>&#xC0AD;&#xC81C;&#xD560; &#xADF8;&#xB8F9; &#xC544;&#xC774;&#xB514;</p>
        <p>&#xCF64;&#xB9C8;(,)&#xB85C; &#xAD6C;&#xBD84;&#xB41C; &#xC544;&#xC774;&#xB514;
          &#xBAA9;&#xB85D; &#xC785;&#xB825; &#xAC00;&#xB2A5;</p>
      </td>
    </tr>
  </tbody>
</table>

#### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| O | success\_count | 삭제된 그룹 갯수 |
| O | error\_count | 오류 처리된 그룹 갯수 |
| O | error\_list | 오류 내역 \["{인덱스}": "{오류코드}", ...\] 형식 |

#### Example Request

```text
curl -XPOST 'https://api.coolsms.co.kr/sms/2/delete_groups' -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&group_ids=565ba3d7d216a'
```

#### Example Response

```text
{
  "success_count": 3,
  "error_count": 2,
  "error_list": [
    4: "62",
    5: "54"
  ]
}
```

### GET groups/{group\_id}

그룹 정보를 리턴합니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/groups/{group\_id}](https://api.coolsms.co.kr/sms/2/groups/%7Bgroup_id%7D)

#### Parameters

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| Ο | 인증정보 | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST_API#Authentication) 참고 |
| O | group\_id | 그룹 아이디 |

#### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| O | group\_id | 그룹 아이디 |
| O | message\_count | 그룹에 담긴 메시지 갯수 |

#### Example Request

```text
curl -XGET 'https://api.coolsms.co.kr/sms/2/groups/{group_id}' -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&group_id=565ba3d7d216a'
```

#### Example Response

```text
{
  "group_id":"565ba3d7d216a",
  "message_count":970
}
```

### POST groups/{group\_id}/add\_messages

그룹에 발송할 문자메시지를 추가합니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/groups/{group\_id}/add\_messages](https://api.coolsms.co.kr/sms/2/groups/%7Bgroup_id%7D/add_messages)

#### Parameters

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
        href="https://developer.coolsms.co.kr/REST_API#Authentication">Authentication</a>&#xCC38;&#xACE0;</td>
    </tr>
    <tr>
      <td style="text-align:left">O</td>
      <td style="text-align:left">to</td>
      <td style="text-align:left">&#xC218;&#xC2E0;&#xBC88;&#xD638; &#xC785;&#xB825;
        <br />&#xCF64;&#xB9C8;(,)&#xB85C; &#xAD6C;&#xBD84;&#xB41C; &#xC218;&#xC2E0;&#xBC88;&#xD638;
        &#xC785;&#xB825;&#xAC00;&#xB2A5;
        <br />&#xC608;) 01012345678,01023456789,01034567890</td>
    </tr>
    <tr>
      <td style="text-align:left">O</td>
      <td style="text-align:left">from</td>
      <td style="text-align:left">&#xBC1C;&#xC2E0;&#xBC88;&#xD638; &#xC785;&#xB825;
        <br />2015/10/16 &#xBC1C;&#xC2E0;&#xBC88;&#xD638; &#xC0AC;&#xC804;&#xB4F1;&#xB85D;&#xC81C;&#xC5D0;
        &#xC758;&#xD574; &#xBC18;&#xB4DC;&#xC2DC; &#xB4F1;&#xB85D;&#xB41C; &#xBC88;&#xD638;&#xB9CC;
        &#xD5C8;&#xC6A9;&#xB429;&#xB2C8;&#xB2E4;. (&#xD574;&#xC678;&#xBB38;&#xC790;
        &#xC81C;&#xC678;)
        <br />&#xC608;) 0212345678</td>
    </tr>
    <tr>
      <td style="text-align:left">O</td>
      <td style="text-align:left">text</td>
      <td style="text-align:left">&#xBB38;&#xC790;&#xB0B4;&#xC6A9;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">type</td>
      <td style="text-align:left">CTA(&#xCE5C;&#xAD6C;&#xD1A1;), ATA(&#xC54C;&#xB9BC;&#xD1A1;), SMS(90&#xBC14;&#xC774;&#xD2B8;),
        LMS(&#xC7A5;&#xBB38; 2,000&#xBC14;&#xC774;&#xD2B8;), MMS(&#xC7A5;&#xBB38;+&#xC774;&#xBBF8;&#xC9C0;)
        <br
        />&#xBBF8;&#xC785;&#xB825;&#xC2DC; SMS
        <br />&#xD574;&#xC678;&#xBB38;&#xC790;&#xC778; &#xACBD;&#xC6B0; SMS&#xB9CC;
        &#xAC00;&#xB2A5;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">image_id</td>
      <td style="text-align:left">
        <p>&#xBC1C;&#xC1A1;&#xD560; &#xC774;&#xBBF8;&#xC9C0;&#xC758; &#xC544;&#xC774;&#xB514;</p>
        <p>type&#xC774; MMS&#xC77C; &#xB54C; &#xD544;&#xC218;</p>
      </td>
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
      <td style="text-align:left">&#xC608;&#xC57D;&#xC2DC;&#xAC04;&#xC744; YYYYMMDDHHMISS &#xD3EC;&#xB9F7;&#xC73C;&#xB85C;
        &#xC785;&#xB825; (&#xC785;&#xB825; &#xC5C6;&#xAC70;&#xB098; &#xC9C0;&#xB09C;&#xB0A0;&#xC9DC;&#xB97C;
        &#xC785;&#xB825;&#xD558;&#xBA74; &#xBC14;&#xB85C; &#xC804;&#xC1A1;)
        <br
        />&#xC608;) 20131216090510 (2013&#xB144; 12&#xC6D4; 16&#xC77C; 9&#xC2DC;
        5&#xBD84; 10&#xCD08;&#xC5D0; &#xBC1C;&#xC1A1;&#xB418;&#xB3C4;&#xB85D; &#xC608;&#xC57D;)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">subject</td>
      <td style="text-align:left">LMS, MMS &#xC77C;&#xB54C; &#xC81C;&#xBAA9; (40&#xBC14;&#xC774;&#xD2B8;)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">template_code</td>
      <td style="text-align:left">&#xC54C;&#xB9BC;&#xD1A1; Template Code</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">sender_key</td>
      <td style="text-align:left">&#xC54C;&#xB9BC;&#xD1A1; Sender Key</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">button_name</td>
      <td style="text-align:left">&#xC54C;&#xB9BC;&#xD1A1;&amp;&#xCE5C;&#xAD6C;&#xD1A1; &#xBC84;&#xD2BC;&#xC774;&#xB984;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">button_url</td>
      <td style="text-align:left">&#xC54C;&#xB9BC;&#xD1A1;&amp;&#xCE5C;&#xAD6C;&#xD1A1; &#xBC84;&#xD2BC;URL</td>
    </tr>
  </tbody>
</table>

**제한 사항**

to 필드의 전화번호 수는 최대 1,000개이며 넘을 경우 오류를 발생 \(RecipientsTooMany\)

한번의 Request의 총 데이터 크기는 2MB를 넘을 수 없습니다 \(HTTP ERROR 413 발생\)

**발송형태별 제한사항**

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
        1,000&#xC790;&#xAE4C;&#xC9C0; &#xBC1C;&#xC1A1;, &#xCE5C;&#xAD6C;&#xB4F1;&#xB85D;&#xC774;
        &#xC548;&#xB418;&#xC5B4;&#xC788;&#xB294; &#xACC4;&#xC815;&#xC5D0;&#xAC8C;&#xB3C4;
        &#xBC1C;&#xC1A1;&#xAC00;&#xB2A5;</td>
    </tr>
    <tr>
      <td style="text-align:left">CTA</td>
      <td style="text-align:left">&#xCE74;&#xCE74;&#xC624;&#xD1A1; &#xCC2C;&#xAD6C;&#xD1A1;&#xC73C;&#xB85C;
        1,000&#xC790;&#xAE4C;&#xC9C0; &#xBC1C;&#xC1A1;, &#xCE5C;&#xAD6C;&#xB4F1;&#xB85D;&#xC774;
        &#xB418;&#xC5B4;&#xC788;&#xC5B4;&#xC57C; &#xBC1C;&#xC1A1;&#xAC00;&#xB2A5;</td>
    </tr>
  </tbody>
</table>

#### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| O | success\_count | 접수 성공 갯수 |
| O | error\_count | 접수 오류 갯수 |
|  | error\_list | 오류 발생 문자메시지 아이디 목록 \["{인덱스}": "{오류코드}", ...\] 형식 인덱스값은 0부터 시작 |

#### Example Request

```text
curl -XPOST https://api.coolsms.co.kr/sms/2/groups/GID565bA3D7D216A/add_messages -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&to=01012345678&from=029302266&text=Hello'
```

#### Example Response

```text
{
  "success_count": 3,
  "error_count": 2,
  "error_list": [
    0: "62",
    4: "54"
  ]
}
```

추가하신 메시지의 전체 개수가 success\_count로 리턴되면 정상적으로 서버에 접수 완료된 것이며, 에러가 발생한 메시지는 error count 와 error\_list 가 리턴됩니다.  
리턴된 error\_code의 정보는 [http://developer.coolsms.co.kr/Legacy\_Result\_Codes](http://developer.coolsms.co.kr/Legacy_Result_Codes) 을 참고하시면 됩니다. 여기서 리턴되는 Response의 내용은 서버에 전송 요청한 것에 대한 정보이며 실제 휴대전화로 전송한 것에 대한 정보가 아닙니다.  sent 조회로 실제 전송된 결과를 확인하실 수 있습니다.

### POST groups/{group\_id}/add\_messages.json

그룹에 발송할 문자메시지를 JSON 형식으로 접수합니다. 대량의 문자를 각각 다른 내용과 타입으로 보내고 싶을 때 용이 합니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/groups/{group\_id}/add\_messages.json](https://api.coolsms.co.kr/sms/2/groups/%7Bgroup_id%7D/add_messages.json)

#### Parameters

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| Ο | 인증정보 | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST_API#Authentication) 참고 |
| O | messages | JSON 형식의 메시지 데이터 |

**JSON Fields**

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
      <td style="text-align:left">to</td>
      <td style="text-align:left">&#xC218;&#xC2E0;&#xBC88;&#xD638; &#xC785;&#xB825;
        <br />&#xCF64;&#xB9C8;(,)&#xB85C; &#xAD6C;&#xBD84;&#xB41C; &#xC218;&#xC2E0;&#xBC88;&#xD638;
        &#xC785;&#xB825;&#xAC00;&#xB2A5;
        <br />&#xC608;) 01012345678,01023456789,01034567890</td>
    </tr>
    <tr>
      <td style="text-align:left">O</td>
      <td style="text-align:left">from</td>
      <td style="text-align:left">&#xBC1C;&#xC2E0;&#xBC88;&#xD638; &#xC785;&#xB825;
        <br />2015/10/16 &#xBC1C;&#xC2E0;&#xBC88;&#xD638; &#xC0AC;&#xC804;&#xB4F1;&#xB85D;&#xC81C;&#xC5D0;
        &#xC758;&#xD574; &#xBC18;&#xB4DC;&#xC2DC; &#xB4F1;&#xB85D;&#xB41C; &#xBC88;&#xD638;&#xB9CC;
        &#xD5C8;&#xC6A9;&#xB429;&#xB2C8;&#xB2E4;. (&#xD574;&#xC678;&#xBB38;&#xC790;
        &#xC81C;&#xC678;)
        <br />&#xC608;) 0212345678</td>
    </tr>
    <tr>
      <td style="text-align:left">O</td>
      <td style="text-align:left">text</td>
      <td style="text-align:left">&#xBB38;&#xC790;&#xB0B4;&#xC6A9;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">type</td>
      <td style="text-align:left">ATA(&#xC54C;&#xB9BC;&#xD1A1;), CTA(&#xCE5C;&#xAD6C;&#xD1A1;), SMS(90&#xBC14;&#xC774;&#xD2B8;),
        LMS(&#xC7A5;&#xBB38; 2,000&#xBC14;&#xC774;&#xD2B8;), MMS(&#xC7A5;&#xBB38;+&#xC774;&#xBBF8;&#xC9C0;)
        <br
        />&#xBBF8;&#xC785;&#xB825;&#xC2DC; SMS
        <br />&#xD574;&#xC678;&#xBB38;&#xC790;&#xC778; &#xACBD;&#xC6B0; SMS&#xB9CC;
        &#xAC00;&#xB2A5;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">image_id</td>
      <td style="text-align:left">
        <p>&#xBC1C;&#xC1A1;&#xD560; &#xC774;&#xBBF8;&#xC9C0;&#xC758; &#xC544;&#xC774;&#xB514;</p>
        <p>type&#xC774; MMS&#xC77C; &#xB54C; &#xD544;&#xC218;</p>
      </td>
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
      <td style="text-align:left">&#xC608;&#xC57D;&#xC2DC;&#xAC04;&#xC744; YYYYMMDDHHMISS &#xD3EC;&#xB9F7;&#xC73C;&#xB85C;
        &#xC785;&#xB825; (&#xC785;&#xB825; &#xC5C6;&#xAC70;&#xB098; &#xC9C0;&#xB09C;&#xB0A0;&#xC9DC;&#xB97C;
        &#xC785;&#xB825;&#xD558;&#xBA74; &#xBC14;&#xB85C; &#xC804;&#xC1A1;)
        <br
        />&#xC608;) 20131216090510 (2013&#xB144; 12&#xC6D4; 16&#xC77C; 9&#xC2DC;
        5&#xBD84; 10&#xCD08;&#xC5D0; &#xBC1C;&#xC1A1;&#xB418;&#xB3C4;&#xB85D; &#xC608;&#xC57D;)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">subject</td>
      <td style="text-align:left">LMS, MMS &#xC77C;&#xB54C; &#xC81C;&#xBAA9; (40&#xBC14;&#xC774;&#xD2B8;)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">template_code</td>
      <td style="text-align:left">&#xC54C;&#xB9BC;&#xD1A1; Template Code</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">sender_key</td>
      <td style="text-align:left">&#xC54C;&#xB9BC;&#xD1A1; Sender Key</td>
    </tr>
  </tbody>
</table>

#### messages 포맷

\[ \] 안에 { } 가 여러 개 들어 갈 수 있는 구조로 되어있으며 각각의 { } 안에는 to, from, text 필드가 필수요소입니다.

```text
[
  {
    "type": "SMS",
    "to": "01000000000,01011111111,01022222222",
    "from": "021234567",
    "text": "Hello A"
  },
  {
    "type": "LMS",
    "to": "01000000000,01011111111,01022222222",
    "from": "021234567",
    "text": "Hello B"
    "subject": "LMS Subject",
  },
  {
    "type": "MMS",
    "to": "01000000000,01011111111,01022222222",
    "from": "021234567",
    "text": "Hello C",
    "subject": "MMS Subject",
    "image_id": "abcdefg"
  }
]
```

**제한 사항**

수신받을 전화번호 총 수\(to 필드 전화번호 합계\)는 최대 1,000개이며 넘을 경우 오류 발생. \(RecipientsTooMany\)

한번의 Request의 총 데이터 크기는 2MB를 넘을 수 없습니다 \(HTTP ERROR 413 발생\)

**발송형태에 따른 제한사항**

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
        1,000&#xC790;&#xAE4C;&#xC9C0; &#xBC1C;&#xC1A1;, &#xCE5C;&#xAD6C;&#xB4F1;&#xB85D;&#xC774;
        &#xC548;&#xB418;&#xC5B4;&#xC788;&#xB294; &#xACC4;&#xC815;&#xC5D0;&#xAC8C;&#xB3C4;
        &#xBC1C;&#xC1A1;&#xAC00;&#xB2A5;</td>
    </tr>
    <tr>
      <td style="text-align:left">CTA</td>
      <td style="text-align:left">&#xCE74;&#xCE74;&#xC624;&#xD1A1; &#xCC2C;&#xAD6C;&#xD1A1;&#xC73C;&#xB85C;
        1,000&#xC790;&#xAE4C;&#xC9C0; &#xBC1C;&#xC1A1;, &#xCE5C;&#xAD6C;&#xB4F1;&#xB85D;&#xC774;
        &#xB418;&#xC5B4;&#xC788;&#xC5B4;&#xC57C; &#xBC1C;&#xC1A1;&#xAC00;&#xB2A5;</td>
    </tr>
  </tbody>
</table>

####  JSON 포맷으로 리턴 됩니다.Response

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| O | success\_count | 접수 성공 갯수 |
| O | error\_count | 접수 오류 갯수 |
|  | error\_list | 오류 발생 문자메시지 아이디 목록 \["{인덱스}": "{오류코드}", ...\] 형식 인덱스값은 0부터 시작 |

#### Example Request

```text
curl -XPOST https://api.coolsms.co.kr/sms/2/groups/565ba3d7d216a/add_messages -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&messages=JSONArray
```

#### Example Response

```text
[
  {
    "success_count": 3,
    "error_count": 0,
  },
  {
    "success_count": 1,
    "error_count": 2,
    "error_list": [
      0: "62",
      1: "54"
    ]
  },
  {
    "success_count": 3,
    "error_count": 0,
  }
]
```

추가하신 메시지의 전체 개수가 success\_count로 리턴되면 정상적으로 서버에 접수 완료된 것이며, 에러가 발생한 메시지는 error count 와 error\_list 가 리턴됩니다.  
리턴된 error\_code의 정보는 [http://www.coolsms.co.kr/Legacy\_Result\_Codes](http://www.coolsms.co.kr/Legacy_Result_Codes) 을 참고하시면 됩니다. 여기서 리턴되는 Response의 내용은 서버에 전송 요청한 것에 대한 정보이며 실제 휴대전화로 전송한 것에 대한 정보가 아닙니다.  sent 조회로 실제 전송된 결과를 확인하실 수 있습니다.

### GET groups/{group\_id}/message\_list

문자메시지 목록을 리턴합니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/groups/{group\_id}/message\_list](https://api.coolsms.co.kr/sms/2/groups/%7Bgroup_id%7D/message_list)

#### Parameters

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
        href="https://developer.coolsms.co.kr/REST_API#Authentication">Authentication</a>&#xCC38;&#xACE0;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">offset</td>
      <td style="text-align:left">
        <p>&#xC870;&#xD68C;&#xD560; &#xBAA9;&#xB85D;&#xC758; &#xC2DC;&#xC791; &#xC704;&#xCE58;</p>
        <p>Default) 0</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">limit</td>
      <td style="text-align:left">
        <p>&#xAC00;&#xC838;&#xC62C; &#xBA54;&#xC2DC;&#xC9C0;&#xC758; &#xAC2F;&#xC218;</p>
        <p>Default) 20</p>
      </td>
    </tr>
  </tbody>
</table>

#### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| O | total\_count | 전체 메시지 갯수 |
| O | offset | 조회 목록의 시작 위치 |
| O | limit | 가져올 메시지의 갯수 |
| O | list | Array 형식의 메시지 목록 |

#### Example Request

```text
curl -XGET 'https://api.coolsms.co.kr/sms/2/groups/{group_id}/message_list' -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125'
```

#### Example Response

```text
{
  "total_count":2,
  "offset":0,
  "limit":20,
  "list":[
     "565ba4e7d316b",
     "565ab383dabcd"
  ]
}
```

### POST groups/{group\_id}/delete\_messages

그룹에 추가된 메시지를 삭제합니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/groups/{group\_id}/delete\_messages](https://api.coolsms.co.kr/sms/2/groups/%7Bgroup_id%7D/delete_messages)

#### Parameters

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
        href="https://developer.coolsms.co.kr/REST_API#Authentication">Authentication</a>&#xCC38;&#xACE0;</td>
    </tr>
    <tr>
      <td style="text-align:left">O</td>
      <td style="text-align:left">message_ids</td>
      <td style="text-align:left">
        <p>&#xCF64;&#xB9C8;&#xB85C; &#xAD6C;&#xBD84;&#xB41C; &#xC0AD;&#xC81C;&#xD560;
          &#xBA54;&#xC2DC;&#xC9C0; &#xC544;&#xC774;&#xB514; &#xBAA9;&#xB85D;</p>
        <p>ex) MID565BA6D7E325C,MID565433E7D233A</p>
      </td>
    </tr>
  </tbody>
</table>

#### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| O | success\_count | 삭제 성공 갯수 |
| O | error\_count |  오류 갯수 |
|  | error\_list | 오류 발생 코드 목록 \["{인덱스}": "{오류코드}", ...\] 형식 인덱스값은 0부터 시작 |

#### Example Request

```text
curl -XPOST 'https://api.coolsms.co.kr/sms/2/groups/{group_id}/delete_messages' -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&message_ids=MID565BA6D7E325C,MID565433E7D233A,MID565643A66AB21'
```

#### Example Response

서버는 json 포맷으로 삭제된 갯수를 리턴합니다.

```text
{
  "success_count": 1,
  "error_count": 2,
  "error_list": [
    0: "1021",
    2: "1021"
  ]
}
```

### POST groups/{group\_id}/send

그룹메시지를 전송 요청합니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/groups/{group\_id}/send](https://api.coolsms.co.kr/sms/2/groups/%7Bgroup_id%7D/send)

#### Parameters

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| Ο | 인증정보 | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST_API#Authentication) 참고 |

#### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| O | group\_id | 전송 요청된 그룹 아이디 |

#### Example Request

```text
curl -XPOST 'https://api.coolsms.co.kr/sms/2/groups/{group_id}/send' -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125'
```

#### Example Response

```text
{
  "group_id": "565ba3d7d216a"
}
```

## 이미지

이미지를 서버에 안전하게 미리 업로드하여 문자발송 때 사용할 수 있어 더욱 안정적인 발송을 보장합니다.

### POST upload\_image

MMS 발송에 필요한 이미지 파일을 업로드 합니다.

MMS 발송 때 미리 업로드 된 이미지 파일을 사용하므로 발송과정에서 발생하는 오류률 현저히 줄어듭니다.

이미지 보관 기간은 7일입니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/upload\_image](https://api.coolsms.co.kr/sms/2/upload_image)

#### Parameters

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| Ο | 인증정보 | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST_API#Authentication) 참고 |
| O | image | 이미지 내용 \(파일명이 아니라 내용입니다.\) Form Submit 옵션 : method=POST enc-type=multipart/form 제한사항\) 300KB, 2048x2048 이하, JPEG, PNG, GIF |
|  | image\_encoding | 이미지 인코딩 방식 binary\(Default\), base64 |

#### Response

JSON 포맷으로 리턴 됩니다.  
리턴되는 image\_id를 MMS 발송 시 {group\_id}/add\_messages 파라메터로 입력하셔야 합니다.

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| O | image\_id | 이미지 아이디 |

#### Example Request

```text
curl -XPOST 'https://api.coolsms.co.kr/sms/2/upload_image' -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125' -F 'image=@/path/to/my/file'
```

#### Example Response

```text
{
  "image_id": IMG565BA2D9E4239"
}
```

### GET image\_list

서버에 업로드 되어 있는 이미지 목록을 리턴합니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/image\_list](https://api.coolsms.co.kr/sms/2/image_list)

#### Parameters

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| Ο | 인증정보 | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST_API#Authentication) 참고 |
|  | offset | 조회할 목록의 시작 위치 Default\) 0 |
|  | limit | 가져올 이미지 아이디의 갯수 Default\) 20 |

#### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| O | total\_count | 전체 메시지 갯수 |
| O | offset | 조회 목록의 시작 위치 |
| O | limit | 가져올 이미지 아이디의 갯수 |
| O | list | Array 형식의 이미지 아이디 목록 |

#### Example Request

```text
curl -XGET 'https://api.coolsms.co.kr/sms/2/image_list' -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125'
```

#### Example Response

```text
{
  "total_count":3,
  "offset":0,
  "limit":20,
  "list":[
    "IMG565BA6D7D327C",
    "IMG565BA7ABD338B",
    "IMG565BB9D7D21C7"
  ]
}
```

### GET images/{image\_id}

업로드된 이미지 정보를 리턴합니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/images/{image\_id}](https://api.coolsms.co.kr/sms/2/images/%7Bimage_id%7D)

#### Parameters

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| Ο | 인증정보 | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST_API#Authentication) 참고 |

#### Response

해당 이미지의 정보가 JSON 포맷으로 리턴 됩니다.

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| O | image\_id | 이미지 아이디 |
| O | file\_name | 파일 명 |
| O | original\_name | 원본 파일 명 |
| O | file\_size | 파일 크기 \(Byte 단위\) |
| O | width | 이미지 가로 픽셀 |
| O | height | 이미지 세로 픽셀 |

#### Example Request

```text
curl -XGET 'https://api.coolsms.co.kr/sms/2/images/{image_id}' -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125'
```

#### Example Response

```text
{
  "image_id":"566fb2266316f",
  "file_name","566fb2266316f.jpg",
  "original_name":"nurigo-200x100.jpg",
  "file_size":"4990",
  "width":"200",
  "height":"100"
}
```

### POST delete\_images

이미지 파일을 삭제합니다.

#### Resource URL

[https://api.coolsms.co.kr/sms/2/delete\_images](https://api.coolsms.co.kr/sms/2/delete_images)

#### Parameters

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| Ο | 인증정보 | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST_API#Authentication) 참고 |
| O | image\_ids | 콤마로 구분된 삭제 할 이미지 ID 목록 예\) IMG565BA6D7E325C,IMG565433E7D233A |

#### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| O | success\_count | 삭제 성공 갯수 |
| O | error\_count | 삭제 오류 갯수 |
|  | error\_list | 오류 발생 문자메시지 아이디 목록 \["{인덱스}": "{오류코드}", ...\] 형식 인덱스값은 0부터 시작 |

#### Example Request

```text
curl -XPOST 'https://api.coolsms.co.kr/sms/2/delete_images' -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&image_ids=IMG565BA2D9E4239,IMG565AB2E4A5134,IMG565BB3A4B4342'
```

#### Example Response

```text
{
  "success_count": 1,
  "error_count": 2,
  "error_list": [
    0: "1023",
    2: "1024"
  ]
}
```

## POST send

문자메시지를 전송 요청합니다. 전송 요청에 대한 Response는 휴대전화까지 전송된 결과가 아닙니다.

### Resource URL

[https://api.coolsms.co.kr/sms/2/send](https://api.coolsms.co.kr/sms/2/send)

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
        href="https://developer.coolsms.co.kr/REST_API#Authentication">Authentication</a>&#xCC38;&#xACE0;</td>
    </tr>
    <tr>
      <td style="text-align:left">O</td>
      <td style="text-align:left">to</td>
      <td style="text-align:left">&#xC218;&#xC2E0;&#xBC88;&#xD638; &#xC785;&#xB825; &#xCF64;&#xB9C8;(,)&#xB85C;
        &#xAD6C;&#xBD84;&#xB41C; &#xC218;&#xC2E0;&#xBC88;&#xD638; &#xC785;&#xB825;&#xAC00;&#xB2A5;
        &#xC608;) 01012345678,01023456789,01034567890</td>
    </tr>
    <tr>
      <td style="text-align:left">O</td>
      <td style="text-align:left">from</td>
      <td style="text-align:left">&#xBC1C;&#xC2E0;&#xBC88;&#xD638; &#xC608;) 0212345678
        <br />2015/10/16 &#xBC1C;&#xC2E0;&#xBC88;&#xD638; &#xC0AC;&#xC804;&#xB4F1;&#xB85D;&#xC81C;&#xC5D0;
        &#xC758;&#xD574; &#xBC18;&#xB4DC;&#xC2DC; &#xB4F1;&#xB85D;&#xB41C; &#xBC88;&#xD638;&#xB9CC;
        &#xD5C8;&#xC6A9;&#xB429;&#xB2C8;&#xB2E4;. (&#xD574;&#xC678;&#xBB38;&#xC790;
        &#xC81C;&#xC678;)</td>
    </tr>
    <tr>
      <td style="text-align:left">O</td>
      <td style="text-align:left">text</td>
      <td style="text-align:left">&#xBB38;&#xC790;&#xB0B4;&#xC6A9;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">type</td>
      <td style="text-align:left">CTA(&#xCE5C;&#xAD6C;&#xD1A1;), ATA(&#xC54C;&#xB9BC;&#xD1A1;), SMS(80&#xBC14;&#xC774;&#xD2B8;),
        LMS(&#xC7A5;&#xBB38; 2,000&#xBC14;&#xC774;&#xD2B8;), MMS(&#xC7A5;&#xBB38;+&#xC774;&#xBBF8;&#xC9C0;)
        &#xC785;&#xB825; &#xC5C6;&#xC73C;&#xBA74; SMS&#xAC00; &#xAE30;&#xBCF8;
        &#xAD6D;&#xAC00;&#xCF54;&#xB4DC;&#xAC00; KR&#xC774; &#xC544;&#xB2C8;&#xBA74;
        SMS&#xB85C; &#xAC15;&#xC81C;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">template_code</td>
      <td style="text-align:left">&#xC54C;&#xB9BC;&#xD1A1; Template Code</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">sender_key</td>
      <td style="text-align:left">&#xC54C;&#xB9BC;&#xD1A1; Sender Key</td>
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
      <td style="text-align:left">&#xC608;&#xC57D;&#xC2DC;&#xAC04;&#xC744; YYYYMMDDHHMISS &#xD3EC;&#xB9F7;&#xC73C;&#xB85C;
        &#xC785;&#xB825; (&#xC785;&#xB825; &#xC5C6;&#xAC70;&#xB098; &#xC9C0;&#xB09C;&#xB0A0;&#xC9DC;&#xB97C;
        &#xC785;&#xB825;&#xD558;&#xBA74; &#xBC14;&#xB85C; &#xC804;&#xC1A1;) &#xC608;)
        20131216090510 (2013&#xB144; 12&#xC6D4; 16&#xC77C; 9&#xC2DC; 5&#xBD84;
        10&#xCD08;&#xC5D0; &#xBC1C;&#xC1A1;&#xB418;&#xB3C4;&#xB85D; &#xC608;&#xC57D;)</td>
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
        &#xC785;&#xB825; &#xC785;&#xB825; &#xC5C6;&#xC73C;&#xBA74; utf8&#xAC00;
        &#xAE30;&#xBCF8;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">srk</td>
      <td style="text-align:left">&#xC194;&#xB8E8;&#xC158; &#xC81C;&#xACF5; &#xC218;&#xC218;&#xB8CC;&#xB97C;
        &#xC815;&#xC0B0;&#xBC1B;&#xC744; &#xC194;&#xB8E8;&#xC158; &#xB4F1;&#xB85D;&#xD0A4;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">mode (&#xD604;&#xC7AC; &#xBBF8;&#xC9C0;&#xC6D0;)</td>
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
      <td style="text-align:left">force_sms (&#xD604;&#xC7AC; &#xBBF8;&#xC9C0;&#xC6D0;)</td>
      <td style="text-align:left">
        <p>&#xB204;&#xB9AC;&#xACE0;&#xD478;&#xC2DC;&#xB97C; &#xC0AC;&#xC6A9;&#xD558;&#xB354;&#xB77C;&#xB3C4;
          SMS&#xB85C; &#xBC1C;&#xC1A1;&#xB418;&#xB3C4;&#xB85D; &#xAC15;&#xC81C;</p>
        <p>true &#xD639;&#xC740; false(&#xAE30;&#xBCF8;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">only_ata</td>
      <td style="text-align:left">
        <p>&#xC54C;&#xB9BC;&#xD1A1;&#xC774; &#xC2E4;&#xD328;&#xD574;&#xB3C4; &#xBB38;&#xC790;&#xBA54;&#xC2DC;&#xC9C0;&#xB85C;
          &#xB300;&#xCCB4;&#xD558;&#xC5EC; &#xBC1C;&#xC1A1;&#xD558;&#xC9C0; &#xC54A;&#xC2B5;&#xB2C8;&#xB2E4;.</p>
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
      <td style="text-align:left">button_name</td>
      <td style="text-align:left">&#xC54C;&#xB9BC;&#xD1A1;&amp;&#xCE5C;&#xAD6C;&#xD1A1; &#xBC84;&#xD2BC;&#xC774;&#xB984;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">button_url</td>
      <td style="text-align:left">&#xC54C;&#xB9BC;&#xD1A1;&amp;&#xCE5C;&#xAD6C;&#xD1A1; &#xBC84;&#xD2BC;URL</td>
    </tr>
  </tbody>
</table>

Mandatory가 Ο 인 필드는 반드시 입력하여야 합니다.

srk 는 앱아이디를 말하는 것으로 [https://www.coolsms.co.kr/me/apps](https://www.coolsms.co.kr/me/apps) 을 참고하세요.

한번의 Request에 extension을 포함하여 총 받는사람\(to\) 수는 1000개 까지가 제한이며 1000개가 넘을 경우 오류를 발생시킵니다. \(RecipientsTooMany\)

한번의 Request의 총 크기는 2MB를 넘을 수 없습니다. \(HTTP ERROR 413 발생\)

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
        <p>2,000&#xBC14;&#xC774;&#xD2B8; &#xD14D;&#xC2A4;&#xD2B8;(&#xD55C;&#xAE00;
          1,000&#xC790;)</p>
        <p>1&#xAC1C;&#xC758; &#xC774;&#xBBF8;&#xC9C0; &#xC804;&#xC1A1;(300KB &#xC774;&#xD558;&#xC758;
          JPEG, PNG, GIF &#xD615;&#xC2DD;&#xC758; &#xD30C;&#xC77C; 2048x2048 &#xD53D;&#xC140;&#xC774;&#xD558;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">ATA</td>
      <td style="text-align:left">&#xCE74;&#xCE74;&#xC624;&#xD1A1; &#xC54C;&#xB9BC;&#xD1A1;&#xC73C;&#xB85C;
        1,000&#xC790;&#xAE4C;&#xC9C0; &#xBC1C;&#xC1A1;, &#xCE5C;&#xAD6C;&#xB4F1;&#xB85D;&#xC774;
        &#xC548;&#xB418;&#xC5B4; &#xC788;&#xC5B4;&#xB3C4; &#xBC1C;&#xC1A1;&#xAC00;&#xB2A5;</td>
    </tr>
    <tr>
      <td style="text-align:left">CTA</td>
      <td style="text-align:left">&#xCE74;&#xCE74;&#xC624;&#xD1A1; &#xCE5C;&#xAD6C;&#xD1A1;&#xC73C;&#xB85C;
        1,000&#xC790;&#xAE4C;&#xC9C0; &#xBC1C;&#xC1A1;, &#xCE5C;&#xAD6C;&#xB4F1;&#xB85D;&#xB41C;
        &#xACC4;&#xC815;&#xC5D0;&#xAC8C;&#xB9CC; &#xBC1C;&#xC1A1;&#xAC00;&#xB2A5;</td>
    </tr>
  </tbody>
</table>

### Response

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| O | group\_id | 그룹아이디 |
| O | success\_count | 성공 건수 |
| O | error\_count | 오류 건수 |
| O | result\_code | 마지막 오류 코드 |
| O | result\_message | 마지막 오류 메시지 |

result\_code 가 00 이면 정상적인 접수이며 이 외의 코드는 [http://www.coolsms.co.kr/Legacy\_Result\_Codes](http://www.coolsms.co.kr/Legacy_Result_Codes) 을 참고하세요. 여기서 리턴되는 Response의 내용은 서버에게 전송을 요청한 것에 대한 정보이지 실제 휴대전화로 전송한 것에 대한 정보가 아닙니다. 예를 들어 요청 건수 중 success\_count가 10개라면 서버의 DB에 안전하게 INSERT된 건이 10개라는 의미이며, 나중 sent 리소스를 통해 조회시 이통사를 통해 실제 전송성공된 건수는 8개이고 올바르지 못한 수신번호로 2개로 실패라는 결과가 나올 수 있습니다.

메시지그룹ID\(group\_id\)는 Request된 메시지들의대표하는 아이디값으로 메시지상태 및 예약취소할 때 키값으로 사용될 수 있습니다. 10건의 문자메시지를 발송할 경우 그 10건의 문자메시지를 대표하는 group\_id 가 리턴되며 sent 리소스를 통해서 10건에 대한 전송상태를 조회할 수 있습니다.

### **Example Request**

```text
curl -XPOST https://api.coolsms.co.kr/sms/2/send -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&to=01012345678,01023456789,01034567890&from=029302266&text=Hello'
```

### **Example Response**

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

## GET sent

발송된 문자메시지의 목록을 가져옵니다. 

### Resource URL

[https://api.coolsms.co.kr/sms/2/sent](https://api.coolsms.co.kr/sms/2/sent)

### Parameters

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| Ο | 인증정보 | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST_API#Authentication) 참고 |
|  | offset | 가져올 목록의 시작 위치 |
|  | limit | 기본값 20이며 20개의 목록을 받을 수 있음. 40입력시 40개의 목록이 리턴 |
|  | rcpt | 수신번호로 검색 |
|  | start | 검색 시작일시 접수 날짜와 시간으로 검색 YYYY-MM-DD HH:MI:SS 포맷의 날짜와 시간 |
|  | end | 검색 종료일시 접수 날짜와 시간으로 검색 YYYY-MM-DD HH:MI:SS 포맷의 날짜와 시간 |
|  | status | 메시지 상태 값으로 검색 |
|  | resultcode | 전송결과 값으로 검색 |
|  | notin\_resultcode | 입력된 전송결과 값 이외의 건들만 조회 |
|  | message\_id | 메시지ID |
|  | group\_id |  ID |

검색 옵션이 없는 경우 가장 최신의 발송건부터 20일 전까지 내림차순으로 페이지 단위의 목록을 리턴합니다.

### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| O | total\_count | 전체 카운트 |
| O | list\_count | ... |

### Example Request

```text
curl -XGET https://api.coolsms.co.kr/sms/2/sent -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&salt=abc&offset=0&limit=20'
```

### **Example Response**

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
      "sent_time":"L",
      "text":"Test Message",
      "carrier":"SKT",
      "scheduled_time":"201401071814"
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
      "scheduled_time":"201401071814"
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
      "scheduled_time":"201401071814"
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
      "scheduled_time":"201401071814"
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

result\_code 는 [http://www.coolsms.co.kr/Legacy\_Result\_Codes](https://developer.coolsms.co.kr/Legacy_Result_Codes) 페이지를 참고 하세요.

## POST cancel

예약된 문자메시지를 취소합니다. 예약되지 않았거나, 예약되었으나 이미 발송된 문자메시지는 취소 할 수 없습니다.

### Resource URL

[https://api.coolsms.co.kr/sms/2/cancel](https://api.coolsms.co.kr/sms/2/cancel)

### Parameters

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| Ο | 인증정보 | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST_API#Authentication) 참고 |
|  | message\_id | 메시지ID |
|  | group\_id | 그룹ID |

message\_id 혹은 group\_id 중 하나는 반드시 입력하세요.

### Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| O | total\_count | 전체 카운트 |
| O | list\_count | ... |

## GET balance

잔액을 확인합니다.

### Resource URL

[https://api.coolsms.co.kr/sms/2/balance](https://api.coolsms.co.kr/sms/2/balance)

### Parameters

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| Ο | 인증정보 | 인증데이터는 필수입니다. [Authentication](https://developer.coolsms.co.kr/REST_API#Authentication) 참고 |

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

### Resource URL

[https://api.coolsms.co.kr/sms/2/status](https://api.coolsms.co.kr/sms/2/status)

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
        href="https://developer.coolsms.co.kr/REST_API#Authentication">Authentication</a>&#xCC38;&#xACE0;</td>
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

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field | Description |
| :--- | :--- | :--- |
| O | registdate | 입력일 |
| O | sms\_average | ... |

모든 항목의 값은 초단위\(seconds\)값입니다. sms\_average와 mms\_average는 각각 SMS채널과 MMS채널의 문자가 접수된 때부터 실제 수신되기까지 걸린 시간으로 계산된 평균값으로 리포트가 오지않은 대기중인 메시지를 합산한 값이므로 다소 높게 나와도 정상입니다. sk, kt, lg 의 경우 수신시각이 분단위로만 제공되어서 약간의 차이가 날 수 있습니다.

### Response Example

```text
[
  {
    "registdate": "2014-02-25 10:34:01",
    "sms_average": "23",
    "sms_sk_average": "9",
    "sms_kt_average": "10",
    "sms_lg_average": "11",
    "mms_average": "52",
    "mms_sk_average": "20",
    "mms_kt_average": "25",
    "mms_lg_average": "36"
  }
]
```

## 메시지상태코드

숫자 4자리로 구성된 메시지의 상태를 나타내는 코드입니다. 코드 첫번째 자리 숫자의 의미는 아래와 같습니다.

Message API 호출시에는 앞에 두자리와 뒤 두자리가 구분되어 리턴됩니다.

예\) 1010 -&gt; status = '1', result\_code = '10'

| 코드 | 내용 |
| :--- | :--- |
| 1xxx | 접수\(전\) 상태 코드 |
| 2xxx | 쿨에스엠에스 게이트웨이 내에서 발송중 상태 코드 |
| 3xxx | 연동망에서 발송 상태 코드 |
| 4xxx | 발송완료 상태 코드 |

### 코드 목록

| 코드 | 내용 |
| :--- | :--- |
| 1010 | 필수 입력 값 미입력 |
| 1013 | 필수 입력 값 미입력\(2\) |
| 1020 | 등록된 계정이 아니거나 패스워드가 틀림 |
| 1021 | 해당 메시지가 없음 |
| 1022 | 해당 그룹이 없음 |
| 1023 | 해당 이미지가 없음 |
| 1024 | 서버 오류 |
| 1025 | 이미지 입력되었으나 타입이 MMS가 아님 |
| 1026 | 중복 수신번호 |
| 1030 | 잔액 부족 |
| 1061 | 사용자에 의해 수신거부 됨\(080무료수신거부\) |
| 1062 | 발신번호 미등록 |
| 2000 | 정상 접수 |
| 2100 | \(예약\) 대기중 |
| 2160 | 예약 취소 |
| 2230 | 잔액 부족 |
| 2254 | 스팸처리\(쿨에스엠에스 게이트웨이\) |
| 3000 | 이통사로 접수 완료\(정상\) |
| 3054 | 스팸처리\(이통사\) |
| 3032 | 미가입자 |
| 3040 | 전송시간 초과 |
| 3041 | 단말기 busy |
| 3042 | 음영지역 |
| 3043 | 단말기 Power off |
| 3044 | 단말기 메시지 저장갯수 초과 |
| 3045 | 단말기 일시 서비스 정지 |
| 3046 | 기타 단말기 문제 |
| 3047 | 착신거절 |
| 3049 | Format Error |
| 3050 | SMS서비스 불가 단말기 |
| 3051 | 착신측의 호불가 상태 |
| 3052 | 이통사 서버 운영자 삭제 |
| 3053 | 서버 메시지 Que Full |
| 3054 | SPAM |
| 3055 | SPAM, nospam.or.kr 에 등록된 번호 |
| 3056 | 전송실패\(무선망단\) |
| 3057 | 전송실패\(무선망-&gt;단말기단\) |
| 3058 | 전송경로 없음 |
| 3059 | 변작된 발신번호. |
| 4000 | 수신완료 |

