- OAuth 2.0

  - 정의
    - **인증을 위한 개방형 표준 프로토콜**
    - 제3의 서비스에게 **사용자의 인증/인가 권한을 위임**하는 방식
  - 주요 용어
    - **Resource Owner** : 사용자 (실제 계정의 주인)
    - **Client** : 애플리케이션 (OAuth를 사용해 인증하려는 서비스)
    - **Resource Server** : 자원 서버 (사용자의 보호된 자원을 가진 서버)
    - **Authorization Server** : 인증 서버 (토큰 발행/검증)
  - 인증 흐름

    1. **권한 부여 요청** (Authorization Request)

       ```
       GET /oauth/authorize?
           client_id=CLIENT_ID&
           response_type=code&
           redirect_uri=REDIRECT_URI&
           scope=read
       ```

    2. **권한 부여 승인** (Authorization Grant)
       - Authorization Code
       - Implicit Grant
       - Resource Owner Password Credentials
       - Client Credentials
    3. **액세스 토큰 요청** (Access Token Request)
    4. **액세스 토큰 발급** (Access Token Response)

       ```json
       {
       	"access_token": "ISSUED_ACCESS_TOKEN",
       	"token_type": "Bearer",
       	"expires_in": 3600,
       	"refresh_token": "ISSUED_REFRESH_TOKEN"
       }
       ```

  - 토큰 종류
    - **Access Token** : 실제 인증에 사용되는 토큰
    - **Refresh Token** : Access Token 갱신용 토큰
    - **ID Token** : 사용자 인증 정보를 포함한 JWT (OpenID Connect)

- HTTP Cookie
  - 정의
    - 웹사이트가 사용자의 브라우저에 저장하는 **작은 텍스트 파일**
    - **상태 유지**를 위한 데이터 저장소 역할
  - 특징
    - **이름=값** 형태로 구성
    - **도메인, 경로, 만료일** 등의 속성 보유
    - 최대 **4KB**까지 저장 가능
  - 주요 속성
    - **Domain** : 쿠키가 전송될 도메인 지정
    - **Path** : 쿠키가 전송될 경로 지정
    - **Expires/Max-Age** : 쿠키 만료 시간
    - **Secure** : HTTPS 연결에서만 전송
    - **HttpOnly** : JavaScript에서 접근 불가
    - **SameSite** : CSRF 공격 방지
  - 종류
    - **Session Cookie**
      - 브라우저 종료시 삭제
      - 만료 시간 미지정
    - **Persistent Cookie**
      - 지정된 만료 시간까지 유지
      - 사용자 설정 저장 등에 활용
    ```
    Set-Cookie: user=john;
        Domain=example.com;
        Path=/;
        Expires=Wed, 21 Oct 2024 07:28:00 GMT;
        Secure;
        HttpOnly
    ```
  - 보안 고려사항
    - **XSS 공격** 방지
      - HttpOnly 플래그 사용
      - 민감 정보 저장 제한
    - **CSRF 공격** 방지
      - SameSite 속성 활용
      - CSRF 토큰 사용
    - **암호화**
      - 중요 정보는 암호화하여 저장
      - HTTPS 사용 강제
  - 활용 사례
    - **로그인 상태 유지**
      ```jsx
      // 서버 응답 헤더
      Set-Cookie: sessionId=abc123; HttpOnly; Secure
      ```
    - **사용자 선호도 저장**
      ```jsx
      // 클라이언트에서 쿠키 설정
      document.cookie = "theme=dark; expires=Fri, 31 Dec 2024 23:59:59 GMT";
      ```
    - **장바구니 기능**
      ```jsx
      // 장바구니 아이템 저장
      Set-Cookie: cart=item1,item2,item3; Path=/shop
      ```
