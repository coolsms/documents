---
description: 잔액 소진 알림 설정 정보를 조회합니다.
---

# 잔액 소진 알림 설정 정보 조회

{% api-method method="get" host="https://rest.coolsms.co.kr" path="/v1/balance/alert" %}
{% api-method-summary %}
Get Low Balance Alert
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-authenticated-account-id" type="string" required=true %}
인증정보
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
성공적으로 조회
{% endapi-method-response-example-description %}

```javascript
{
    "balances": [
        20,
        4000,
        60000
    ],
    "_id": "12925149",
    "dateCreated": "2018-06-26T07:20:58.731Z",
    "dateUpdated": "2018-06-26T07:20:58.757Z"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}


