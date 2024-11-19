- Swagger
  - 정의
    - **REST API를 설계, 빌드, 문서화 및 사용**하는 데 도움이 되는 OpenSource 도구들의 모음
    - 개발자가 REST 웹 서비스를 문서화, 설계, 테스트할 수 있게 도와주는 프레임워크
  - 주요 기능
    - **API 명세 작성** : YAML 또는 JSON 형식으로 API 정의
    - **시각화된 문서** : 작성된 명세를 웹 UI로 시각화
    - **API 테스트** : 문서 상에서 직접 API 호출 테스트 가능
    - **코드 생성** : 서버 스텁과 클라이언트 SDK 자동 생성
  - 구성 요소
    - **Swagger Editor** : API 문서 편집기
    - **Swagger UI** : API 문서 뷰어
    - **Swagger Codegen** : 서버/클라이언트 코드 생성기
  - 사용 예시
    ```java
    @ApiOperation(value = "사용자 정보 조회")
    @GetMapping("/users/{id}")
    public UserResponse getUser(
        @ApiParam(value = "사용자 ID") @PathVariable Long id
    ) {
        return userService.getUser(id);
    }
    ```
- OpnAPI
  - 정의
    - REST API를 **표준화된 방식으로 기술**하기 위한 명세
    - Swagger Specification이 **2016년에 OpenAPI Initiative로 이관**되며 이름 변경
  - 특징
    - **벤더 중립적** : 특정 회사나 기술에 종속되지 않음
    - **확장 가능** : 사용자 정의 확장 지원
    - **언어 독립적** : 모든 프로그래밍 언어에서 사용 가능
  - 구조
    - **Info** : API 메타데이터
    - **Paths** : API 엔드포인트와 동작 정의
    - **Components** : 재사용 가능한 API 컴포넌트
    - **Security** : 인증/인가 방식 정의
- OpenAPI 버전 별 특징 및 주요 차이점
  - **2.0 (Swagger)**
    - JSON과 YAML 형식 지원
    - 단순한 구조로 시작하기 쉬움
    - 제한된 재사용성과 모듈화
    ```yaml
    swagger: "2.0"
    info:
      title: "사용자 API"
      version: "1.0.0"
    ```
  - **3.0**
    - 향상된 재사용성과 모듈화
    - 컴포넌트 개념 도입
    - 링크 기능으로 HATEOAS 지원
    ```yaml
    openapi: "3.0.0"
    info:
      title: "사용자 API"
      version: "1.0.0"
    ```
  - **3.1**
    - JSON Schema 2020-12 지원
    - 웹훅 지원 강화
    - 확장된 보안 스키마
- OpenAPI Component
  - 정의
    - API 명세에서 **재사용 가능한 부분을 정의**하는 섹션
    - DRY(Don't Repeat Yourself) 원칙 실현
  - 주요 구성요소
    - **schemas** : 데이터 모델 정의
      ```yaml
      components:
        schemas:
          User:
            type: object
            properties:
              id:
                type: integer
              name:
                type: string
      ```
    - **parameters** : API 매개변수 정의
    - **requestBodies** : 요청 본문 정의
    - **responses** : 응답 정의
    - **securitySchemes** : 보안 방식 정의
  - 사용 이점
    - **코드 중복 감소**
    - **일관성 유지**
    - **유지보수성 향상**
  - 실제 적용
    ```yaml
    paths:
      /users:
        get:
          responses:
            "200":
              description: "성공"
              content:
                application/json:
                  schema:
                    $ref: "#/components/schemas/User"
    ```
