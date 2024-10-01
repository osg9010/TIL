# GCM (Google Cloud Messaging)

-  Android & IOS 를 지원
- 서버와 클라이언트 간 APP PUSH 메세지를 보낼수 있다.


# FCM (Firebase Cloud Messaging)

- GCM 의 새로운 버전
- Android & IOS & Mobile Web 모두 지원

## 차이점

1. 지원 기기 GCM(Android & IOS) , FCM(Android & IOS & Mobile Web)
2. GCM 에서 불편했던 등록, 구독 로직을 FCM 라이브러리에 포함시켜 간편화
3. 전송로직 또한 GCM 은 com.google.android.gcm.server 패키지를 import 해서 구현 해야 했지만
FCM 에서는 직접 소켓을 사용하여 전송로직 구현 가능하다.
4. GCM은 2019년 4월 11일 부로 지원 종료 - 사용 불가능
