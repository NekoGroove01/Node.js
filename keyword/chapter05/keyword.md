- 환경 변수
  - 정의
    - 프로세스가 컴퓨터에서 동작하는 방식에 영향을 미치는, **동적인 값들의 모임**
    - 운영체제가 참조하는 동적인 값들의 집합
  - 종류
    - **사용자 변수**
      - 로그인한 사용자에게만 적용
      - 다른 사용자와 독립적으로 설정/관리
      - 시스템 변수보다 **우선 적용**
    - **시스템 변수**
      - 시스템을 사용하는 모든 사용자에게 적용
      - 공통으로 사용되는 설정값들 포함
    - **PATH 변수**
      - 실행 파일을 찾는 기본 경로 지정
      - 사용자/시스템 변수 모두에 존재
      - 특이사항: 시스템 PATH가 사용자 PATH보다 우선 적용
  - 활용 사례
    - 개발 환경별 설정 분리
      - 개발(Development)
      - 테스트(Test)
      - 운영(Production)
    - 민감 정보 관리
      - DB 접속 정보
      - API 키
      - 비밀번호
- CORS
  - 정의
    - 다른 출처(도메인, 프로토콜, 포트)의 리소스를 공유하기 위한 **HTTP 헤더 기반 메커니즘**
    - 웹 브라우저에서 보안상의 이유로 적용하는 정책
  - 작동 방식
    - **1단계**: 브라우저가 요청 헤더에 Origin 포함
    - **2단계**: 서버가 Access-Control-Allow-Origin 응답
    - **3단계**: 브라우저가 정책 위반 여부 검사
  - 주요 헤더
    ```
    Origin: <https://frontend.com>
    Access-Control-Allow-Origin: <https://api.backend.com>
    Access-Control-Allow-Methods: GET, POST, PUT, DELETE
    Access-Control-Allow-Headers: Content-Type
    ```
  - 해결 방법
    1. 서버 설정
       - 허용할 출처 명시
       - 와일드카드(\*) 사용 가능 (보안상 좋지 않음)
    2. 프록시 서버 활용
       - 동일 출처에서 요청하는 것처럼 우회
    3. 개발 환경 설정
       - webpack dev server 설정
       - package.json proxy 설정
- DB Connection, DB Connection Pool
  - 정의: **데이터베이스와 애플리케이션 간의 연결 세션**
    - 특징
      - 연결 생성은 비용이 큰 작업
      - 동시 연결 수 제한 존재
  - **Connection Pool**
    - 정의: **미리 생성해둔 Connection들을 관리하는 공간**
    - 장점
      - 연결 생성/종료 오버헤드 감소
      - 리소스 재사용으로 성능 향상
      - 동시 접속자 관리 용이
    - 설정 요소
      ```
      # 예시 설정
      maximumPoolSize=10
      minimumIdle=5
      maxLifetime=1800000
      connectionTimeout=30000
      ```
- 비동기 (async, await)
  - 정의
    - **비동기 작업을 동기식 코드처럼 작성**할 수 있게 해주는 문법
    - Promise를 기반으로 동작
  - 주요 특징
    - **async 함수**
      - 항상 Promise를 반환
      - await 키워드 사용 가능
    - **await 키워드**
      - Promise 완료까지 대기
      - 비동기 작업의 결과값 반환
  - 예시 코드
    ```jsx
    async function fetchData() {
    	try {
    		const response = await fetch("api/data");
    		const data = await response.json();
    		return data;
    	} catch (error) {
    		console.error("데이터 조회 실패:", error);
    	}
    }
    ```
- try/catch/finally
  - 정의
    - **예외 처리를 위한 구문**
    - 프로그램의 안정성과 신뢰성 보장
  - 구조
    - **try 블록**
      - 예외 발생 가능성이 있는 코드
      - 정상적인 흐름 처리
    - **catch 블록**
      - 예외 발생 시 처리할 코드
      - 에러 로깅, 대체 로직 실행
    - **finally 블록**
      - 예외 발생 여부와 관계없이 실행
      - 리소스 정리 등에 사용
  - 실제 예시
    ```java
    try {
        connection = dataSource.getConnection();
        // DB 작업 수행
    } catch (SQLException e) {
        logger.error("DB 연결 실패", e);
        throw new DatabaseException("데이터베이스 오류 발생");
    } finally {
        if (connection != null) {
            connection.close();  // 리소스 정리
        }
    }
    ```
  - 모범 사례
    - 구체적인 예외 처리
    - 적절한 로깅
    - 리소스 해제 보장
    - 예외 전환 및 래핑
