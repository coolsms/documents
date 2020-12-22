# 메시지 목록 엑셀다운로드

## Request
```
GET https://api.coolsms.co.kr/messages/v4/list/excel
```

메시지의 목록을 다운로드합니다.

### Authorization 인증 필요 [[?]](https://docs.coolsms.co.kr/authentication/overview#authorization)

| 계정 권한 | 회원 권한 | 계정 상태 | 회원 상태 | 계정 인증 |
| :- | :- | :- | :- | :-: |
| `message:read` | `role-message:read` | `ACTIVE` | `ACTIVE` |  |

### Query Params
| Name | Type | Required | Allowed Operator [[?]](https://docs.coolsms.co.kr/api-reference/overview#operator) | Description |
| :--- | :--: | :------: | :--------------: | :---------- |
| criteria | `string` |  | eq | 검색 조건에 사용되는 필드명<br>criteria 의 값은 'key1,key2,key3' 과 같이 ,(콤마) 로 구분되며 cond, value 와 함께 사용됩니다.<br>- messageId - 메시지 아이디 입니다.<br>- groupId - 그룹 아이디 입니다.<br>- to - 수신 번호 입니다.<br>- from - 발신 번호 입니다.<br>- type - 문자 메시지의 타입 입니다.  (SMS, LMS, MMS, ATA, CTA, CTI)<br>- dateCreated - 그룹 생성일 입니다.<br>- dateUpdated - 그룹 정보를 변경한 마지막 시각 입니다.<br>- replacement - 대체 발송 여부 입니다. (true, false)<br>- statusCode - 문자 메시지의 상태 코드 입니다. |
| cond | `string` |  | eq | 검색 조건에 사용되는 연산자<br>criteria 와 같이 'cond1,cond2' 와 같이 ,(콤마)로 구분되며, criteria,value 와 함께 사용됩니다.<br>- eq - 같음 (=)<br>- ne - 같지 않음 (!=)<br>- gt - 보다 큼 (>)<br>- gte - 보다 크거나 같음 (>=)<br>- lt - 보다 작음 (<)<br>- lte - 보다 작거나 같음 (<=) |
| value | `string` |  | eq | 검색 값<br>criteria , cond 값에 대응하는 value 입니다.<br>criteria='messageId,statusCode'<br>cond='eq,eq'<br>일 경우 groupId 에 대응하는 value 값을 찾고 status 에 대응하는 값을 찾는 조건 입니다.<br>e.g - value='메시지아이디,2000' |
| limit | `number` |  | eq | 한 페이지에 불러옥 목록 개수 |
| dateType | `string` |  | eq | 설명 없음 |
| startDate | `date` |  | eq | 검색 시작 날짜 |
| endDate | `date` |  | eq | 검색 끝 날짜 |

---

## Samples

### 발송내역 엑셀 다운로드

> **Sample Request**

```
http://api.coolsms.co.kr/messages/v4/list/excel?criteria=messageId&value=M4V20180307110044DTYYJBBYLPQZIB1&cond=eq
```

> **Sample Response**

```json
"PK\u0003\u0004\n\u0000\u0000\u0000\b\u0000,+)Q}���0\u0001\u0000\u0000�\u0003\u0000\u0000\u0013\u0000\u0000\u0000[Content_Types].xml���N�0\u0010E%�\u0016%nY ��v�c\t�(\u001f0ؓĪ_�LK��8I+��H ��q�̜�ș-v�\u0016[Ld��Ŵ��\u0002�\n���\u0016o���V\u0014��5��\u0016{$���V��T�^O��㝔�:t@U��s҄��6�2�ZC��z2��*xF�%�3�|��\rl,\u0017���~t- Fk\u0014p֒y�(\u001ew9\u001c-���A���\u0013�� R%�C\ru&��) ��\u0013^�IF�\u0010�i�B\u001d��喊bB��!��հV\u000e�\u001f�KH�\f.O�;+?BZ����\u000e'�~O\u0018���\u000f!�a�^΃xo��I��\u0005�\u001d$ԯ��\r?/��O\u001e�˦B�2��&6gN�M�9%�\u0017\u001e�r���PK\u0003\u0004\n\u0000\u0000\u0000\u0000\u0000,+)Q\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0003\u0000\u0000\u0000xl/PK\u0003\u0004\n\u0000\u0000\u0000\u0000\u0000,+)Q\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u000e\u0000\u0000\u0000xl/worksheets/PK\u0003\u0004\n\u0000\u0000\u0000\b\u0000,+)Q2�\"�\u0018\u0002\u0000\u0000o\u0006\u0000\u0000\u0018\u0000\u0000\u0000xl/worksheets/sheet1.xml��oo�0\u0010ƿ����\tP(\b�Z(:����^\u001b�!\u0016q.�Mi���$��\u001d���ٿ<�{ι����:�� Ɇ�]\u0006�nS>�\u001fa�2�>d��1N�ɇ�h�pIu\u000br�ٓ\u0018��ƆjGt�8�J%��v\u0010�\";)\f%����jȿ1�95b+Ra>K�����\nı`|\u0006� yf�\\\u0014O�\"d:\u0011�>��5z�R0\u0005\u001abӲy����\u0006d@�A�Q$�[��F��c�\u0010\u000e7mL&���%�Q_��N�P\"Z��[_C��\u0006l\u0001���*\u001a�\u0000#%v�y�5�M\u0019�\u0001���\u0016m\t���GQu���\u001d_�O8���NmB��h^���Жj>����LR�\u0018E<������\u0017���ޥ�\u00195t2RpD�,A紸$�0�XCX��Pl���G��}�\u0004#�n�`'��'�:1��v���D�N<�D�N�}�N,|�W'�>ѯ\u0013+���\u0013�>1�\u0013�\u001b\u001csL]7 ���\u0006䟭�v���vsk۾���c\u0003�X6m@\u001cGf���\u0006�q~ހ8�dQ!au=��}�ճ_x?p����V���\u0006���m�u\u0003����U�N��\u000f:�scC�Nd\u001a���i�O��6���;��`\f�s����U\u0011u0�\u0001�9(\u0006��\u001f3�\u000bPK\u0003\u0004\n\u0000\u0000\u0000\u0000\u0000,+)Q\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0006\u0000\u0000\u0000_rels/PK\u0003\u0004\n\u0000\u0000\u0000\b\u0000,+)Q&��j�\u0000\u0000\u0000�\u0001\u0000\u0000\u000b\u0000\u0000\u0000_rels/.rels��Mj\u00031\f��b��h�E(%N6��])�\u0001T[�Ì-#;mr��BKSR�R�{���ٝ�l�Y�(�²i�pt���[x=>-\u001e��B��,�-\\8�n�y�J��aL�TF�\u0016�R�#bv\u0003\u0007ʍ$�u҉\u0006*��\u001e\u0013��z�UۮQ3��i\u000eނ\u001e�\u0012���\u001e�t��x/�\u00148�\u001b+�(*���b�<���&25\u0015\nx;���,�߉�\u000by*�N�\u0017I�[�X��\u0013ǋ{�����\u000e�W\u001f�~\u0002PK\u0003\u0004\n\u0000\u0000\u0000\b\u0000,+)Q��*\b\u0002\u0001\u0000\u0000�\u0001\u0000\u0000\u000f\u0000\u0000\u0000xl/workbook.xml��Ok�0\fſ��q<�\u0018!I/c����\u001dGiLl�X��~�9i�\u0006���'\u001e�!=�����\u0007\"\u0019�\r�E�\u0019x���}��^9����,zh�\u0005�����q�\u0011g�t�\u001d<F����3g���SJ�\u0012��\u0004NQ�\u0001|vF�N��ƃ�\u0010A\r4\u0001$g�SY�\b���\u0011*�\u001f�8\u0015�c�itA%�\u001bk�eem��\b\u0005��hxC}t��u�\b6\u0013��d\u0002m�|�\u001d�\u0019\u001d�pLE�↺;N�B��}m�D�m�DI.�hk��Z��ʼr9�U���EtC�\u0019g�2Y�n�|Alsbc��PK\u0003\u0004\n\u0000\u0000\u0000\u0000\u0000,+)Q\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\t\u0000\u0000\u0000xl/_rels/PK\u0003\u0004\n\u0000\u0000\u0000\b\u0000,+)Q\u0011gy��\u0000\u0000\u00004\u0002\u0000\u0000\u001a\u0000\u0000\u0000xl/_rels/workbook.xml.rels��Mk�0\f@���}q��\u0018�n/c�k?~���84����˿����@\u0007;�$��{\u000f�\\��:Q�>\u0006\u0003MU��`��Cg��xz\u0005ł��\u0010\u0003\u0019��a�Zni@)_���Ua\u00046�Eқ�l=��UL\u0014ʦ�yD)�����\u001d�E]��|ˀ9Sm���q\u000bP{�\u001d�\u0001����$�4�\n���D��ƶ�-�G�9R�;v=���\u001f�|\u0013#�@������o~�瘏��Z^F��\u001f�5FϮ��\u0000PK\u0003\u0004\n\u0000\u0000\u0000\u0000\u0000,+)Q\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\t\u0000\u0000\u0000docProps/PK\u0003\u0004\n\u0000\u0000\u0000\b\u0000,+)Q\u000b��Z5\u0001\u0000\u0000�\u0002\u0000\u0000\u0011\u0000\u0000\u0000docProps/core.xml��]K�0\u0014��J�}��s���@eW\u000e\u0005'�w!9݂�\u0007I�ۿ7��n�y%�&��<y�!�l�Z�\r�K�+��\u0014#��\b�W\u0015~]Γ\u001b�|`Z��h��\u0016<��%�\u00057\u000e�����\u0004��G���\n�C�\u0005!��A1�FB�bc�b!^݊X�?�\nHN�5Q\u0010�`��^��ш�J�G��r� \u0010�@\u000b\nt�$K3rd\u00038�/6\f�\u0013Rɰ�p\u0011=\u0014Gz��\bv]�v�\u0001��3�x|\u0019FM��7�\u0001ץ�\u0005w��q�Brg�i\u0002zj\u001a�\u0001�zp%9!�m�̇E\\{#A�m�j�\r���w2\u0010(F-v�\u001d*o����\u001c�9�iBo�Y�i��s�Ni��g9s\u001c�j�п�\u0007I=�?�6�\u000fPK\u0003\u0004\n\u0000\u0000\u0000\b\u0000,+)Q@�n�q\u0001\u0000\u0000�\u0002\u0000\u0000\u0014\u0000\u0000\u0000xl/sharedStrings.xml}��J�0\u001c�_��^�v�Mi+�����*λ�EWX��d2�ԩ\fv%V\u0010�D\u0010\u0014�\u000b��\n�B6}\u00073\u0006N;k�r~'�s\u0012���체�]j9D\u0003� \u0002\u0012&\u0005�h�-\r�\u001a�\u0003i Qf��Yv\b��.�`LW)eR��\u0012�\u0001E\u001c�\u0012k��'z��J�\u0006J�UF!��\u0012�M:�T0\u0011d�qm����\u0005i��f��0fv\u0019*\b\rC۴\b\u0010\u0011��2=��x��{\u0012?;�v�y*d�\n;�k�|y\r���9o���U��\b�_�,x���A�_�Eհ��/��2�N:1�wQ���\u0018�j�����A�\u001f^p�\u001f\u0017w�9���������\u001f����]���\u0011\u000e���\u0015CF\bE��k\n��(�R���䤑�g3������\\F��g~���H\"5�X2�W�s\u000b�\u0019%;�\u0018�3\\cQ\ru�tW\u0014M\u0019\u0013=\t�ϩ\u0001PK\u0003\u0004\n\u0000\u0000\u0000\b\u0000,+)Q��o\u0006�\u0001\u0000\u0000S\u0003\u0000\u0000\r\u0000\u0000\u0000xl/styles.xml���j�0\u0010�_E�^w�]��kl�\u00100��KS(�\u001edY�E5\u001a#iúOߑ�\t\u000bmu����7�\u0019����e��\u0007���}��v\n{�ƚ}jw�8\u000bQ�^Zt��\u000e���B\\��2i\u001d\u0019��qt�eg�~=��⌨.�|�q.�\bj� �\u001eg��2�\u0007\u0019��G\u0011f�e\u001f\u0012\t�8\u0016ŝ\u0000i�F(A�\u000f\u0004��y�w\na��tƚ�d�\u000b&��\u0004Fy\f8�=E\n\u001c\u0006�����,���r\u0017h!\u0006���\"��Ub�[\u001e��\u0006|��;\u0015�\u001f\u000b-\u0001 ��MS\tP������S�݉��\u0012\u001b��\u0006t��I�>�b�ҒrL�\n-z�Ǯ�m[�d'A�n\u000fҚΛ$\u000e\u0012�]��k%�-%4־&<�Uh*j`�޵ta��i��.G�_1��\u001fޣ�����M@�(o�����m���TV\u000f�\u0002�\u0019��G�E2�H�i���\u0011��\t�\u0012�\u001d\b���߆w\u0005]\u0007&��.-��X�<5?7�/����\u0002��m\u001emv��ޖ�N���7PK\u0001\u0002\u0014\u0000\n\u0000\u0000\u0000\b\u0000,+)Q}���0\u0001\u0000\u0000�\u0003\u0000\u0000\u0013\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000[Content_Types].xmlPK\u0001\u0002\u0014\u0000\n\u0000\u0000\u0000\u0000\u0000,+)Q\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0003\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0010\u0000\u0000\u0000a\u0001\u0000\u0000xl/PK\u0001\u0002\u0014\u0000\n\u0000\u0000\u0000\u0000\u0000,+)Q\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u000e\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0010\u0000\u0000\u0000�\u0001\u0000\u0000xl/worksheets/PK\u0001\u0002\u0014\u0000\n\u0000\u0000\u0000\b\u0000,+)Q2�\"�\u0018\u0002\u0000\u0000o\u0006\u0000\u0000\u0018\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000�\u0001\u0000\u0000xl/worksheets/sheet1.xmlPK\u0001\u0002\u0014\u0000\n\u0000\u0000\u0000\u0000\u0000,+)Q\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0006\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0010\u0000\u0000\u0000�\u0003\u0000\u0000_rels/PK\u0001\u0002\u0014\u0000\n\u0000\u0000\u0000\b\u0000,+)Q&��j�\u0000\u0000\u0000�\u0001\u0000\u0000\u000b\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000 \u0004\u0000\u0000_rels/.relsPK\u0001\u0002\u0014\u0000\n\u0000\u0000\u0000\b\u0000,+)Q��*\b\u0002\u0001\u0000\u0000�\u0001\u0000\u0000\u000f\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u001e\u0005\u0000\u0000xl/workbook.xmlPK\u0001\u0002\u0014\u0000\n\u0000\u0000\u0000\u0000\u0000,+)Q\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\t\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0010\u0000\u0000\u0000M\u0006\u0000\u0000xl/_rels/PK\u0001\u0002\u0014\u0000\n\u0000\u0000\u0000\b\u0000,+)Q\u0011gy��\u0000\u0000\u00004\u0002\u0000\u0000\u001a\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000t\u0006\u0000\u0000xl/_rels/workbook.xml.relsPK\u0001\u0002\u0014\u0000\n\u0000\u0000\u0000\u0000\u0000,+)Q\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\t\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0010\u0000\u0000\u0000�\u0007\u0000\u0000docProps/PK\u0001\u0002\u0014\u0000\n\u0000\u0000\u0000\b\u0000,+)Q\u000b��Z5\u0001\u0000\u0000�\u0002\u0000\u0000\u0011\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000�\u0007\u0000\u0000docProps/core.xmlPK\u0001\u0002\u0014\u0000\n\u0000\u0000\u0000\b\u0000,+)Q@�n�q\u0001\u0000\u0000�\u0002\u0000\u0000\u0014\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\f\t\u0000\u0000xl/sharedStrings.xmlPK\u0001\u0002\u0014\u0000\n\u0000\u0000\u0000\b\u0000,+)Q��o\u0006�\u0001\u0000\u0000S\u0003\u0000\u0000\r\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000�\n\u0000\u0000xl/styles.xmlPK\u0005\u0006\u0000\u0000\u0000\u0000\r\u0000\r\u0000\u0010\u0003\u0000\u0000�\f\u0000\u0000\u0000\u0000"
```

> **Sample Code**

{% tabs %}

{% tab title="NODE" %}

```javascript
var request = require('request');

var options = {
  headers: {
    Authorization:
      'HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4'
  },
  method: 'GET',
  json: true,
  url:
    'http://api.coolsms.co.kr/messages/v4/list/excel?criteria=messageId&value=M4V20180307110044DTYYJBBYLPQZIB1&cond=eq'
};

request(options, function(error, response, body) {
  if (error) throw error;
  console.log('result :', body);
});

```
{% endtab %}

{% tab title="PHP" %}

```php
<?php
$url = "http://api.coolsms.co.kr/messages/v4/list/excel?criteria=messageId&value=M4V20180307110044DTYYJBBYLPQZIB1&cond=eq";

$options = array(
    'http' => array(
        'header'  => "Authorization: HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4\r\n",
        'method'  => 'GET'
    )
);

$context  = stream_context_create($options);
$result = file_get_contents($url, false, $context);

var_dump($result);

```
{% endtab %}

{% tab title="PYTHON" %}

```python
import requests

url = "http://api.coolsms.co.kr/messages/v4/list/excel?criteria=messageId&value=M4V20180307110044DTYYJBBYLPQZIB1&cond=eq"
headers = {
  "Authorization": "HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4"
}

response = requests.get(url, headers=headers)
print(response.status_code)
print(response.text)

```
{% endtab %}

{% tab title="CURL" %}

```curl
#!/bin/bash
curl -X GET \
	-H 'Authorization: HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4' \
	http://api.coolsms.co.kr/messages/v4/list/excel?criteria=messageId&value=M4V20180307110044DTYYJBBYLPQZIB1&cond=eq
```
{% endtab %}

{% tab title="RUBY" %}

```ruby
require 'net/http'
require 'uri'
require 'json'

uri = URI.parse("http://api.coolsms.co.kr/messages/v4/list/excel?criteria=messageId&value=M4V20180307110044DTYYJBBYLPQZIB1&cond=eq")

headers = {
  "Authorization": "HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4"
}
http = Net::HTTP.new(uri.host, uri.port)
request = Net::HTTP::Get.new(uri.request_uri, headers)

response = http.request(request)
puts response.code
puts response.body

```
{% endtab %}

{% tab title="GO" %}

```go
package main

import (
  "fmt"
  "io/ioutil"
  "net/http"
  "strings"
)

func main() {
  uri := "http://api.coolsms.co.kr/messages/v4/list/excel?criteria=messageId&value=M4V20180307110044DTYYJBBYLPQZIB1&cond=eq"

  req, err := http.NewRequest("GET", uri, nil)
  if err != nil { panic(err) }

  req.Header.Set("Authorization", "HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4")

  client := &http.Client{}
  resp, err := client.Do(req)
  if err != nil { panic(err) }
  defer resp.Body.Close()

  bytes, _ := ioutil.ReadAll(resp.Body)
  str := string(bytes)
  fmt.Println(str)
}

```
{% endtab %}

{% tab title="JAVA" %}

```java
package solapi;

import java.io.BufferedReader;
import java.io.DataOutputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Request {
  public static void main(String[] args) throws Exception {
    String targetUrl = "http://api.coolsms.co.kr/messages/v4/list/excel?criteria=messageId&value=M4V20180307110044DTYYJBBYLPQZIB1&cond=eq";

    URL url = new URL(targetUrl);
    HttpURLConnection con = (HttpURLConnection) url.openConnection();

    con.setRequestMethod("GET");

    con.setRequestProperty("Authorization", "HMAC-SHA256 apiKey=NCSAYU7YDBXYORXC, date=2019-07-01T00:41:48Z, salt=jqsba2jxjnrjor, signature=1779eac71a24cbeeadfa7263cb84b7ea0af1714f5c0270aa30ffd34600e363b4");

    con.setDoOutput(true);
    DataOutputStream wr = new DataOutputStream(con.getOutputStream());
    wr.writeBytes(parameters);
    wr.flush();
    wr.close();

    int responseCode = con.getResponseCode();
    BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
    String line;
    StringBuffer response = new StringBuffer();
    while ((line = in.readLine()) != null) {
      response.append(line);
    }
    in.close();

    System.out.println("HTTP response code : " + responseCode);
    System.out.println("HTTP body : " + response.toString());
  }
}

```
{% endtab %}

{% endtabs %}

---

> 문서 생성일 : 2020-09-09
