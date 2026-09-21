---
name: nexacro
description: 넥사크로(Nexacro) Platform 17, Nexacro Studio 17 프로젝트의 XPRJ/XADL/XFDL/XJS/JavaScript 화면 개발, Form·컴포넌트·Dataset·Grid·바인딩·이벤트·transaction 작성과 수정, NRE/QuickView 오류 진단 및 Nexacro N 코드의 17 호환성 분석을 지원한다. 순수 Nexacro N 구현이나 일반 웹 프론트엔드 작업에는 적용하지 않는다.
---

# Nexacro 17 Development

Nexacro Platform 17 코드와 프로젝트를 한국어로 분석·작성·수정한다. API, 객체, 컴포넌트, 속성, 이벤트 이름은 제품 표기를 유지한다.

## 먼저 확인할 것

1. 제공된 파일에서 제품 버전, 프로젝트 구조, Dataset 및 컴포넌트 ID, 서비스 URL, callback 규약, 공통함수와 명명 규칙을 찾는다. 관련 `.xprj`, `.xadl`, `.xfdl`, `.xjs`, `.js`, `environment.xml`, `typedefinition.xml`, `appvariables.xml`이 있으면 필요한 범위에서 함께 읽는다.
2. 실제 프로젝트 관례를 일반 예제보다 우선한다. 기존 공통 transaction wrapper, 메시지, 팝업, validation 함수를 발견하면 표준 API로 대체하지 말고 호출 규약을 추적한다.
3. 요청이 설명·진단인지 파일 수정인지 구분한다. 설명 요청은 근거와 수정 방향을 제시하고 파일을 바꾸지 않는다.
4. 중요한 식별자나 계약이 없으면 짧게 확인한다. 이미 제공된 계약은 다시 묻지 않는다. 예시만 필요한 경우에는 `dsExample`, `svcExample`, `<SERVICE_URL>`처럼 명백한 예시/자리표시자를 사용한다.

## 작업 원칙

- 존재가 불확실한 Nexacro API, 속성, 이벤트, 반환값을 추측하지 않는다. 저장소의 실제 사용례를 확인하고, 접근 가능하면 [TOBESOFT Nexacro 17 공식 매뉴얼](https://docs.tobesoft.com/nexacro_17_ko)로 교차검증한다. 공식 문서에 접근할 수 없으면 저장소 근거와 미검증 사실을 구분해 밝힌다.
- Nexacro 17과 Nexacro N을 동일하게 취급하지 않는다. N 자료만 확인되는 기능은 17 지원 여부를 별도로 검증하고, 검증하지 못했으면 그 한계를 밝힌다.
- 사용자가 요구하지 않은 대규모 재작성, ID 변경, Dataset 스키마 변경, 서비스 계약 변경을 피한다. XFDL의 선언부와 script가 함께 영향을 받는 변경은 양쪽 참조를 모두 확인한다.
- 표준 Nexacro API와 프로젝트 고유 helper를 명확히 구분한다. 고유 helper를 예시로 만들 때는 가상 함수라고 표시하고 예상 signature를 설명한다.
- 수정 후에는 정적 검증 결과와 Nexacro Studio/NRE에서 추가로 확인할 항목을 구분해 보고한다. 실행 환경이 없으면 실행 성공을 주장하지 않는다.

## 참조 라우팅

- 프로젝트 구성, XFDL/script 관계, Form 이벤트 흐름을 다룰 때는 [project-and-form.md](references/project-and-form.md)를 읽는다.
- 컴포넌트, Dataset binding, Grid format 및 행 상태를 다룰 때는 [data-binding-and-grid.md](references/data-binding-and-grid.md)를 읽는다.
- 서버 조회·저장, `transaction()` 인자, Dataset 매핑, callback 문제를 다룰 때는 [transactions.md](references/transactions.md)를 읽는다.
- 공통 스크립트, validation, 메시지 및 팝업 규약을 다룰 때는 [common-patterns.md](references/common-patterns.md)를 읽는다.
- 오류 진단, 성능, 브라우저/NRE 차이, 생성·배포 문제를 다룰 때는 [debugging-and-runtime.md](references/debugging-and-runtime.md)를 읽는다.
- 생성·수정·분석·진단 응답의 구체적인 모양이 필요할 때만 [examples.md](references/examples.md)를 읽는다.

필요한 참조만 읽고, 서로 연결된 문제라면 관련 문서를 함께 사용한다.

## 결과 작성

- 문제 원인 또는 구현 결과를 먼저 말하고, 관련 ID·이벤트·Dataset·서비스 매핑을 구체적으로 짚는다.
- 코드 변경은 기존 스타일과 구조를 보존한 최소 패치로 제안한다. 새 화면 예시는 선언부와 script의 연결 관계가 드러나도록 작성한다.
- 사실 확인에 사용한 공식 문서 페이지를 가능한 한 직접 링크한다. YouTube 강의는 학습 순서와 주제 선정에 활용하되 API 사실의 최종 근거로 사용하지 않는다.
- 코드 수정 후에는 변경 범위에 해당하는 이벤트 연결, Dataset 컬럼/행 상태, Grid binding, transaction 입출력 매핑, callback signature 및 브라우저/NRE 대상 환경만 검증한다.
