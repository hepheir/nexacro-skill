# 넥사크로 스튜디오 업무 입문 매뉴얼

기존 회사 프로젝트에서 화면을 수정하고 Java Spring Legacy 서버와 데이터를 주고받을 때 필요한 내용을 정리했습니다.

처음이라면 [프로젝트 열기](basics/project/project-start.md) → [빌드 경로 설정](basics/project/build-path.md) → [Dataset의 역할](basics/data/dataset.md) → [Spring 연결 구조](basics/server/spring-legacy.md) 순서로 전체 흐름을 확인하세요.

## 개발환경과 빌드

| 주제 | 주요 내용 |
| --- | --- |
| [회사 프로젝트를 받으면 무엇부터 열어야 하나요?](basics/project/project-start.md) | 파일 구조, QuickView와 전체 실행 |
| [저장하면 자동으로 빌드되나요?](basics/project/generate.md) | Auto Generate, 수동 Generate, Regenerate |
| [빌드된 파일은 어디에 저장되나요?](basics/project/build-path.md) | Generate Path 지정과 반영 확인 |

## 화면·스타일·이벤트

| 주제 | 주요 내용 |
| --- | --- |
| [어떤 컴포넌트를 선택하면 되나요?](basics/ui/components.md) | 입력·선택·표·컨테이너의 용도 |
| [화면 크기가 바뀌어도 배치를 유지하려면요?](basics/ui/layout.md) | Position, Align, Arrangement |
| [컴포넌트에 스타일은 어떻게 적용하나요?](basics/ui/styles.md) | Theme/XCSS, cssclass, 개별 속성 |
| [이벤트 함수는 어떻게 연결하나요?](basics/ui/events.md) | 이벤트 등록과 호출 시점 |
| [this·obj는 무엇이고 컴포넌트는 어떻게 찾나요?](basics/ui/script-scope.md) | 속성 변경, Div 경로, 변수 범위 |

## Dataset과 Grid

| 주제 | 주요 내용 |
| --- | --- |
| [Dataset은 DB 테이블인가요?](basics/data/dataset.md) | 화면 데이터와 DB의 차이 |
| [Dataset 컬럼은 어떤 기준으로 설계하나요?](basics/data/dataset-design.md) | 식별자·자료형·서버 계약 |
| [목록과 상세 화면은 어떻게 함께 바뀌나요?](basics/data/binding.md) | Grid·입력창 바인딩 |
| [Combo에는 왜 두 종류의 데이터를 연결하나요?](basics/data/combo.md) | 선택지 목록과 현재 선택값 |
| [Grid의 표시 모양과 편집 방식은 어떻게 정하나요?](basics/data/grid.md) | band, displaytype, edittype |
| [Grid에 순번과 합계를 표시하려면요?](basics/data/grid-expression.md) | bind와 expr, 계산식 |

## 통신·저장·공통화

| 주제 | 주요 내용 |
| --- | --- |
| [서버로 조회 요청은 어떻게 보내나요?](basics/communication/transaction.md) | transaction 인자와 매핑 방향 |
| [조회 결과는 언제 사용할 수 있나요?](basics/communication/callbacks.md) | 비동기 호출과 callback |
| [화면에서 바꾼 값은 언제 DB에 저장되나요?](basics/communication/data-sync.md) | 저장 요청과 결과 동기화 |
| [공통 함수는 어디에 있고 어떻게 사용하나요?](basics/common/functions.md) | XJS include와 함수 규약 |
| [공통 화면·컴포넌트·템플릿은 어떻게 다른가요?](basics/common/ui-reuse.md) | 재사용 방식의 선택 |
| [공통 통신 함수는 무엇을 대신 처리하나요?](basics/common/transaction-wrapper.md) | 공통 처리와 화면 후처리 |

## Spring 연동과 문제 해결

| 주제 | 주요 내용 |
| --- | --- |
| [넥사크로와 Spring Legacy는 어떻게 연결되나요?](basics/server/spring-legacy.md) | WAS·Spring·DB의 역할 |
| [화면 URL과 서버 Dataset 이름은 어떻게 맞추나요?](basics/server/request-mapping.md) | URL 해석과 데이터 계약 |
| [문제가 생기면 어디부터 확인하나요?](basics/project/troubleshooting.md) | 증상별 첫 확인 지점과 로그 |
| [회사 프로젝트를 빠르게 파악하려면요?](basics/project/project-map.md) | 기존 업무 화면 추적 방법 |

## 심화 주제

| 주제 | 주요 내용 |
| --- | --- |
| [빌드·실행·배포 경로 추적](details/build-and-deploy.md) | 생성 파일과 실제 실행 파일이 다를 때 |
| [가변 레이아웃·스타일·Grid 세부 사항](details/layout-and-grid.md) | 내용 크기·스크롤·셀 인덱스를 다룰 때 |
| [Dataset 계약·행 상태·저장 후 동기화](details/dataset-and-save.md) | 삭제·저장 실패·동시 수정을 처리할 때 |
| [동적 이벤트와 공통 코드의 의존성](details/events-and-common.md) | 등록·해제 또는 공유 코드를 수정할 때 |
| [Spring Legacy 연동 설정과 요청 추적](details/spring-integration.md) | 서버 변환 모듈·설정·DB 처리 범위를 확인할 때 |

## 참고 자료

화면 개발 내용은 저장소의 [투비소프트 기본 강의 6편](../youtube/)과 Nexacro Platform 17.1 공식 문서를 바탕으로 합니다. 서버 연동은 전통적인 Spring MVC 구조를 기준으로 설명합니다. ID·경로·코드는 예시이며, 실제 프로젝트의 버전과 공통 규약을 우선하세요.
