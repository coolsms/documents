# PHP SDK v2



해당 SDK는 SMS API v2를 이용하여 만들어 졌습니다. 반드시 메뉴얼을 보시고 사용 부탁드립니다. -&gt; [메뉴얼 바로가기](https://developer.coolsms.co.kr/SMS_API_v2)

## Start here \( SDK v2.0 \)

Coolsms PHP SDK v2.0 PSR-4에 준수하여 코딩 되어있습니다.

이 의미는 namespace 와 autoload를 이용하여 만들어져 있다는 이야기입니다.

[namespacing](http://php.net/manual/en/language.namespaces.rationale.php) 과 [autoloading](http://php.net/manual/en/function.spl-autoload-register.php) 의 개념을 이해하시는 것이 개발 하는데에 있어서 더 도움이 될 것 입니다.

### Step 1. Download SDK

아래 방법중 한 가지를 선택해 다운로드 해주세요.

* Composer를 이용해 다운로드 가능 합니다.

  ```text
  composer require coolsms/php-sdk
  ```

* Coolsms 사이트에서도 다운로드 받으실 수 있습니다. 해당 압축파일에는 Coolsms PHP SDK, 코드 샘플이 포함되어 있습니다. -&gt; [바로가기](https://developer.coolsms.co.kr/download/3130218)
* Github를 통해 소스를 가져올 수 있습니다. -&gt; [바로가기](https://github.com/coolsms/php-sdk)

### Step 2. COOLSMS 회원가입

* [쿨에스엠에스](https://www.coolsms.co.kr/signup)로 가서 회원가입을 해주세요.

### Step 3. API KEY 생성

* [환경설정](https://www.coolsms.co.kr/credentials) 페이지로 가서 생성 버튼을 눌러 API\_KEY와 API\_SECRET을 발급 받아주세요.

![API\_KEY &#xC0DD;&#xC131;.png](https://developer.coolsms.co.kr/files/attach/images/4789067/095/789/004/57d202589a16c4c500d02d7daa5bbb81.png)

### Step 4. 문자보내기

* 이제 PHP SDK를 사용할 준비가 되었습니다! [Example](https://developer.coolsms.co.kr/PHP_SDK_Example)을 통해 사용 방법을 알아보세요.

### 참고사항

10월 16일 이후로 발신번호 사전등록제로 인해 등록된 발신번호로만 문자를 보내실 수 있습니다. 아래 관련링크를 참고 해주세요.

* [발신번호 사전등록제 공지사항](https://support.coolsms.co.kr/hc/ko/articles/115008027767-%EB%B0%9C%EC%8B%A0%EB%B2%88%ED%98%B8%EB%9E%80-)  
* [PHP SDK 발신번호 등록 방법](https://developer.coolsms.co.kr/PHP_SDK_Example#SenderID)  
* [웹 에서 발신번호 등록하기](https://www.coolsms.co.kr/senderids)

## System requirements

* PHP 5.5 or greater  
* The curl extension  
* Composer \(optional\)

