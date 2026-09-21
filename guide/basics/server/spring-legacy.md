# 넥사크로와 Spring Legacy는 어떻게 연결되나요?

[매뉴얼 목차](../../README.md)

**화면은 HTTP 요청을 보내고, WAS 안의 Spring 애플리케이션이 업무·DB 처리를 수행합니다.** Dataset을 바꾸는 것만으로 Java 코드나 SQL이 자동 실행되지는 않습니다.

```text
넥사크로 화면 → HTTP 요청 → Spring Controller
                                  ↓
                               Service
                                  ↓
                             DAO / Mapper → DB
```

응답은 역방향으로 돌아와 Dataset과 화면에 반영됩니다. WAS는 Java 웹 앱을 실행하는 환경이고 Spring은 그 안에서 요청과 업무 로직을 구성하는 프레임워크입니다.

## 요청은 어떻게 Controller를 찾나요?

Spring MVC의 DispatcherServlet이 요청 URL에 맞는 Controller를 연결합니다. 영상의 JSP 대신 `.do` 등의 Controller 경로를 호출할 수 있으며 URL과 데이터 형식이 맞아야 합니다. [Spring MVC 공식 설명](https://docs.spring.io/spring-framework/docs/4.3.x/spring-framework-reference/html/mvc.html)

## Dataset은 누가 Java 데이터로 바꾸나요?

서버에 있는 X-API, Spring 연동 어댑터 또는 사내 공통 모듈이 요청·응답 형식의 변환을 담당합니다. 변환된 데이터로 검증·조회·저장하는 업무 로직은 별도로 필요합니다.

일반 JSON을 반환했다고 Dataset으로 자동 연결되는 것은 아닙니다. 양쪽이 합의한 형식과 변환 코드가 필요합니다.

## 두 종류의 transaction

넥사크로 `transaction()`은 통신 API이고 Spring의 DB 트랜잭션은 DB 작업을 함께 커밋·롤백하는 범위입니다. 여러 화면 요청이 저절로 하나의 DB 트랜잭션으로 묶이지 않습니다. 서버에서는 transaction manager, 적용 대상과 롤백 규칙을 함께 확인합니다.

---

관련 문서: [URL·Dataset 이름 맞추기](request-mapping.md) · [Spring 설정과 요청 추적](../../details/spring-integration.md)
