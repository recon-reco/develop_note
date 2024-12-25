# Cloud Fuctions

```
npm install -g firebase-tools
```
> 권한 문제로 npm이 글로벌 패키지를 설치할 수 없다. 
> sudo 로 밀어붙임

**Firebase용 Cloud Fuctions는 Firebase 기능과 HTTPS 요청에 의해**
**트리거되는 이벤트에 응답하여 백엔드 코드를 자동으로 실핼할 수 있는 서버리스 프레임워크**

- Firebase Emulator실행
> - Firebase 프로젝트의 fuctions 디렉토리로 이동한 뒤 에뮬레이터를 실행합니다.
```
cd path/to/firebase/functions
firebase emulators:start --only functions
```
> - 실행중인 nodeMailAPI의 엔드포인트를 확인합니다.
> ```http://localhost:5001/[YOUR_PROJECT_ID]/[REGION]/nodeMailAPI```

- 프론트엔드에서 API 호출 설정
프론트엔드에서 handleForgotPassword 함수가 호출되었을 때,   
MailConnector의 forgotPassword 메서드가 로컬 Firebase Emulator의 nodeMailAPI/forgotPassword 엔드포인트를 호출하도록 합니다.      
MailConnector의 BaseConnector에서 getURL()이 로컬 Firebase Emulator URL을 반환하도록 임시로 수정합니다.
```
getURL() {
  return 'http://localhost:5001/[YOUR_PROJECT_ID]/[REGION]/nodeMailAPI';
}
```
- 테스트 데이터 설정
handleForgotPassword 함수에 필요한 테스트 데이터를 준비합니다
- 프론트엔드에서 함수 호출
handleForgotPassword가 실행되도록 버튼을 클릭하거나 UI에서 동작을 트리거합니다.
- Firebase Emulator에서 로그 확인
Firebase Emulator 콘솔에서 로그를 확인합니다.   
nodeMailAPI/forgotPassword 엔드포인트가 호출되었는지 확인하세요.   
로그에서 StudentMailBuilder가 이메일 전송 요청을 처리했는지 확인합니다.   
- 결과 확인
API가 제대로 호출되었다면: Firebase Emulator의 로그에 요청 정보가 기록됩니다.   
에러가 발생하면:Firebase Functions 로그 또는 네트워크 탭에서 요청이 실패한 이유를 확인합니다.   


Cloud Functionsでメール送信をテストしたいのですが、以下のエラーを回避する方法がどうしても分かりません。どのツールを使ってどのようにテストすれば良いのか、教えていただけませんでしょうか？
```
Access to fetch at '   :9000/#/:1 Access to fetch at 'https://nodemailapi-hn7w3foona-dt.a.run.app/verifyMail' from origin 'http://127.0.0.1:9000' has been blocked by CORS policy: Response to preflight request doesn't pass access control check: No 'Access-Control-Allow-Origin' header is present on the requested resource. If an opaque response serves your needs, set the request's mode to 'no-cors' to fetch the resource with CORS disabled.

POST asyncProcessor.ts:51 
 POST https://nodemailapi-hn7w3foona-dt.a.run.app/verifyMail net::ERR_FAILED
    post                    @asyncProcessor.ts:51
    forgotPassword          @mailConnector.ts:37
    handleForgotPassword    @LoginForm.vue:151

 
 Uncaught (in promise) TypeError: Failed to fetch
    at AsyncProcessor.post (asyncProcessor.ts:51:23)
    at MailConnector.forgotPassword (mailConnector.ts:37:39)
    at handleForgotPassword (LoginForm.vue:151:23)
    at callWithErrorHandling (chunk-YEGD7IN3.js?v=8d42fdfd:2239:19)
    at callWithAsyncErrorHandling (chunk-YEGD7IN3.js?v=8d42fdfd:2246:17)
    at emit (chunk-YEGD7IN3.js?v=8d42fdfd:8314:5)
    at navigateOnClick (quasar_dist_quasar_c…s?v=8d42fdfd:2267:7)
    at onClick (quasar_dist_quasar_c…s?v=8d42fdfd:2810:7)
    at callWithErrorHandling (chunk-YEGD7IN3.js?v=8d42fdfd:2239:19)
    at callWithAsyncErrorHandling (chunk-YEGD7IN3.js?v=8d42fdfd:2246:17)

```