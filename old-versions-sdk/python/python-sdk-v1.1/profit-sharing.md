# Profit Sharing



솔루션 등록 키\(SRK\)  입력만으로 수익쉐어에 동참하실 수 있습니다. SRK 를 발급받기 위해 솔루션프로바이더\(SP\)로 등록해야하는데 [개발자 수익쉐어](https://www.coolsms.co.kr/me/apps) 페이지에서 SP등록과 SRK 발급이 가능합니다. [수익쉐어 적용하기](https://developer.coolsms.co.kr/Profit_Sharing_Apply) 에서 좀 더 자세한 안내를 받으실 수 있습니다. SRK를 발급받았다면 수익배분을 받기 위해 하실 코드는 srk=’K00001234′ 와 같이 객체를 생성할 때 파라메터를 추가해 줍니다.

```text
import coolsms
cool = coolsms.rest(api_key, api_secret, srk='K00001234')
cool.send(to,sender,message)
```

