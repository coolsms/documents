# Example



REST\_API를 이용하여 문자를 보내고 전송결과를 받으며 발신번호 및 문자에 사용 될 이미지를 등록할 수 있습니다.

PHP SDK 에서는 크게 네가지 분류로 나뉘며 각각의 기능에 대해서는 아래 설명을 참고 해주세요.

| 분류                                                                              | 설명                                                                                             |
| ------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| [Message](https://developer.coolsms.co.kr/PHP\_SDK\_EXAMPLE\_Message)           | 각 타입별 문자발송, 전송내역 확인, 예악문자 취소 등을 담당합니다.                                                         |
| [GroupMessage](https://developer.coolsms.co.kr/PHP\_SDK\_EXAMPLE\_GroupMessage) | <p>REST 2 에서 새롭게 추가된 그룹문자 발송을 담당합니다.<br>( 대량문자 측면에서 'Message'보다 빠르고 유실 없는 메시지 전송이 가능합니다. )</p> |
| [Image](https://developer.coolsms.co.kr/PHP\_SDK\_EXAMPLE\_Image)               | MMS( 포토문자 )에 사용 될 이미지를 미리 등록, 삭제 등을 담당합니다.                                                     |
| [SenderID](https://developer.coolsms.co.kr/PHP\_SDK\_EXAMPLE\_SenderID)         | 2015년 10월 16일부터 필수가 된 발신번호 등록제를 위한 API로 발신번호 등록, 삭제를 담당합니다.                                    |
