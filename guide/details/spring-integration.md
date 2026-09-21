# Spring Legacy 연동 설정과 요청·응답 추적

[매뉴얼 목차](../README.md) · 관련 문서: [Spring 연결 구조](../basics/server/spring-legacy.md)

경로와 클래스 이름은 예시입니다. 실제 프로젝트의 연동 모듈, 버전과 요청·응답 규약을 적용합니다.

## Spring과 WAS는 각각 무엇을 하나요?

WAS는 Java 웹 애플리케이션을 실행하는 환경이고, Spring은 그 안에서 요청·업무 로직 등을 구성하는 프레임워크입니다. 여기서는 Spring Boot 자동 설정이 아닌 **기존 Spring MVC 프로젝트를 읽는 관점**으로 설명합니다.

```text
Nexacro 화면 / 공통 통신 함수
    ↓ HTTP 요청
WAS → 필터·인증 → DispatcherServlet → Controller
                                      ↕ 요청·응답 데이터 변환
                                   Service
                                      ↓
                              DAO / Mapper → DB
```

응답은 역방향으로 돌아갑니다. 변환 모듈은 요청 인자를 만들고 반환값을 처리하는 단계 등에 관여하며, 배치는 회사 구현에 따라 다릅니다. Spring MVC의 `DispatcherServlet`은 URL에 맞는 Controller로 요청을 연결합니다. [Spring MVC 공식 설명](https://docs.spring.io/spring-framework/docs/4.3.x/spring-framework-reference/html/mvc.html)

## 영상의 JSP 대신 Spring Controller를 호출해도 되나요?

가능합니다. 넥사크로에서 중요한 것은 파일 확장자가 아니라 **요청 URL과 데이터 형식에 맞게 서버가 처리하는지**입니다.

| 항목 | 설명용 예시 |
| --- | --- |
| Services의 접두어 | `SvcURL` |
| 기본 URL | `http://localhost:8080/erp/` |
| 화면의 요청 URL | `SvcURL::employee/search.do` |
| 해석된 주소 | `http://localhost:8080/erp/employee/search.do` |
| 서버 Context Path | `/erp` |
| Controller 매핑 | `/employee/search.do` |

DispatcherServlet이 `*.do` 또는 `/` 등으로 이 요청을 받도록 설정되어 있어야 합니다. `.do`는 이 예시의 매핑 관례이며 필수 확장자는 아닙니다. 프록시를 경유하는 회사에서는 외부 URL과 WAS 내부 경로가 다를 수 있습니다.

## Dataset이 Java 객체로 바로 들어오나요?

**그 변환을 맡는 연동 코드가 필요합니다.** 다음 두 가지 형태를 기존 서버에서 찾아보세요.

| 방식 | 역할 | 코드에서 찾을 단서 |
| --- | --- | --- |
| X-API 직접 사용 | HTTP 데이터를 PlatformData/DataSet으로 읽고 응답 작성 | `HttpPlatformRequest`, `receiveData`, `HttpPlatformResponse` |
| Spring 연동 어댑터·사내 공통 모듈 | 요청 Dataset을 Java 객체로, 반환값을 응답 형식으로 변환 | argument resolver, return value handler, Nexacro용 View 등 |

X-API는 데이터 송수신·변환을 제공합니다. 이것이 SQL 실행까지 대신하는 것은 아닙니다. XML·SSV 등 전송 형식은 클라이언트와 서버 설정이 맞아야 합니다. [Nexacro 17 X-API 통신 설명](https://docs.tobesoft.com/server_setup_guide_nexacro_17_ko/572ac01860742c20)

어댑터를 쓰는 프로젝트에서는 `@ParamDataSet`, `NexacroResult` 같은 이름을 볼 수 있습니다. 이는 Spring 자체 API가 아니라 연동 라이브러리가 제공하는 기능입니다. 공식 [UIAdapter 설정 예](https://docs.tobesoft.com/edu-nexacro-egov/64758130f0590a7b)는 Nexacro N 기준이므로 **구성 요소를 이해하는 참고 자료**로 사용하고, 17.1 회사 프로젝트에는 설치된 모듈의 패키지·버전·설정 방식을 적용합니다.

일반 `@ResponseBody`로 임의 JSON을 반환한다고 기본 transaction 예제의 Dataset 매핑이 자동으로 성립하지는 않습니다. JSON 방식을 쓴다면 그 형식과 Dataset 변환을 처리하는 회사의 통신 규약이 있어야 합니다.

## 조회 하나는 어떤 약속으로 연결하나요?

아래 계약을 예로 들면, 화면과 서버에서 같은 이름을 찾아 추적할 수 있습니다.

| 단계 | 이름·내용 |
| --- | --- |
| 화면 조회 조건 | `ds_search`: `DEPT_CD`, `KEYWORD` |
| input 매핑 | `in_search=ds_search:A` |
| 서버 수신 이름 | `in_search` |
| 조회 처리 | 조건으로 Service → DAO/Mapper → SELECT |
| 서버 응답 이름 | `out_emp`: `EMPL_ID`, `FULL_NAME`, `DEPT_CD`, `SALARY` |
| output 매핑 | `ds_emp=out_emp` |
| 화면 반영 | `ds_emp`에 바인딩된 Grid·상세 갱신 |

서버는 검색어·권한·자료형을 검증합니다. 조회 결과가 0건인 경우에도 응답 Dataset과 컬럼 구조를 어떻게 제공할지 정해 두면 화면의 바인딩을 일관되게 유지할 수 있습니다.

## 서버 코드를 읽을 때의 처리 순서

다음은 **실제 API 문법이 아닌 의사코드**입니다. 서버 연동 방식에 따라 같은 역할을 다른 클래스가 맡습니다.

```text
/employee/search.do 요청을 받는다
  → in_search를 읽고 검색 조건으로 변환한다
  → 권한과 조건을 확인한다
  → EmployeeService가 조회한다
  → 결과를 out_emp라는 응답 Dataset으로 구성한다
  → 성공 코드와 함께 넥사크로 응답 형식으로 전송한다
```

X-API 직접 사용 코드라면 `receiveData()` → `getData()` → 업무 처리 → 응답 `setData()` → `sendData()`를 찾습니다. 어댑터 방식이라면 앞뒤 변환을 공통 모듈이 맡으므로 Controller에는 Java 객체를 받는 인자와 결과 객체 반환만 보일 수 있습니다.


## 저장과 DB 트랜잭션은 어떻게 구성하나요?

넥사크로의 `transaction()`은 통신 API이고, Spring의 트랜잭션은 **서버 DB 작업을 함께 성공·실패시키는 범위**입니다. 화면에서 API를 여러 번 호출했다고 하나의 DB 트랜잭션으로 묶이지는 않습니다.

여러 변경 행을 한 번에 저장한다면 서버 Service에서 업무 단위의 처리 범위를 정합니다. 원자적 저장이 필요한 경우 그 범위 내에서 검증과 INSERT/UPDATE/DELETE를 처리하고 실패 시 롤백합니다. Spring은 XML의 transaction advice 또는 `@Transactional` 등으로 이를 구성합니다. 애너테이션을 붙였다는 사실만이 아니라 transaction manager·적용 대상·롤백 규칙까지 확인해야 합니다. [Spring 4.3 트랜잭션 공식 설명](https://docs.spring.io/spring-framework/docs/4.3.x/spring-framework-reference/html/transaction.html)

| 저장 시 정할 내용 | 이유 |
| --- | --- |
| 신규·수정·삭제 상태의 전달 방식 | 어떤 SQL을 실행할지 구분 |
| 삭제 행과 식별자 처리 | 목록에서 사라진 기존 행도 삭제 요청에 포함 |
| 생성 키·서버 계산값의 응답 | 저장 뒤 화면과 DB 값 일치 |
| 실패 응답·롤백 범위 | 일부 저장 여부를 사용자가 판단할 수 있게 함 |
| 동시 수정 확인 | 다른 사용자의 변경을 덮어쓸지 결정 |

화면의 `:U`와 행 상태만 믿고 무조건 SQL을 실행하는 대신, 서버에서 권한·대상 존재·값의 유효성을 검증합니다. DAO가 MyBatis인지 JDBC인지, 별도 공통 저장 엔진인지도 회사 코드를 따라갑니다.

## 기존 프로젝트에서는 어느 파일부터 보나요?

| 확인할 파일·설정 | 찾을 내용 |
| --- | --- |
| `pom.xml` 또는 `WEB-INF/lib` | Spring·X-API·UIAdapter·사내 연동 모듈 버전 |
| `web.xml` 또는 초기화 코드 | DispatcherServlet, URL 매핑, 필터, Context 설정 |
| `*-servlet.xml` 등 MVC 설정 | Controller 검색, 인자·응답 변환, 오류 처리 |
| `context-*.xml` 등 서비스 설정 | DataSource, transaction manager, Service·DAO |
| 이미 동작하는 Controller | 수신 Dataset 이름, 반환 형식, 오류 규약 |
| 해당 SQL·Mapper | 컬럼 alias·자료형, 조회 조건, 저장 로직 |

파일명은 예시입니다. Spring Legacy라는 정보만으로 XML 설정·MyBatis 사용·어댑터 버전을 확정할 수는 없습니다. 새로운 설정을 추가하기 전에 기존 조회 화면 한 개의 요청부터 응답까지 연결해서 읽으세요.

## 통신 오류는 어디에서 구분하나요?

| 증상 | 확인 지점 |
| --- | --- |
| 404 | Context Path, Services URL, servlet·Controller 매핑 |
| 401/403 또는 로그인 화면 반환 | 세션·인증 필터, 회사의 요청 규약 |
| 브라우저에서만 교차 출처 오류 | 화면과 API의 origin, 개발 프록시·CORS 설정 |
| HTTP 200인데 처리 실패 | 업무 오류 코드, 응답이 HTML인지 Dataset 형식인지 |
| 응답 데이터는 있는데 Grid가 비어 있음 | output 이름 → 컬럼명 → 화면 바인딩 |
| 저장 요청은 왔는데 DB가 그대로 | input 이름·행 상태 → Service → SQL·커밋/롤백 |

브라우저 Network의 URL·상태·응답과 WAS 로그를 같은 요청 기준으로 대조하면 어느 구간의 문제인지 좁힐 수 있습니다. 화면 성공 메시지는 서버 업무 성공 응답을 확인한 뒤 표시합니다.
