# 디버깅, 성능, 실행 환경

## 오류 진단

1. 먼저 제공된 코드와 데이터 계약으로 원인을 좁힌다. 환경 차이가 개입할 수 있거나 정적 검토로 확정되지 않을 때 재현 조건, 대상 환경(브라우저 또는 NRE), Nexacro 17 세부 버전을 확인한다.
2. 최초 오류 메시지와 stack, Output/console 기록을 확보한다.
3. XFDL event 연결, 함수명, include 순서, 객체 생성 시점을 확인한다.
4. Dataset·Grid·transaction 문제라면 관련 참조 문서의 계약을 대조한다.
5. 증상을 가리는 방어 코드보다 최초 원인을 수정한다.

`trace()`를 추가할 때 개인정보, 인증정보, 전체 서버 응답을 기록하지 않는다. 임시 진단 코드는 최종 패치에서 제거하거나 의도를 명시한다.

## 성능

- 반복문 안에서 동일 컴포넌트 탐색, format 변경, 불필요한 redraw와 expression 재계산을 줄인다.
- 대량 Dataset 갱신은 event/redraw 제어가 필요한지 검토하되, 기존 상태를 저장해 작업 후 반드시 복원한다.
- 모든 성능 문제를 `set_enableevent(false)`로 덮지 않는다. callback과 validation 등 필요한 이벤트가 사라지는 영향을 점검한다.
- Grid가 느리면 row 수, 복잡한 expression, cell별 script 호출, format 재생성, 이미지와 custom control을 함께 확인한다.

## 브라우저와 NRE

- 파일 시스템, 외부 프로세스, 장치 API, WebBrowser, 다운로드/업로드 등은 실행 환경 차이가 클 수 있다.
- 브라우저에서만 또는 NRE에서만 재현되는 문제는 user agent 추측보다 공식 지원 범위와 실제 runtime 로그를 우선한다.
- 환경별 분기는 기존 프로젝트의 runtime 판별 방식을 재사용한다.

## 생성과 배포

- 원본 XFDL/XJS와 generate 결과물을 구분한다. generate output을 직접 고치는 방식은 제안하지 않는다.
- Base Lib Path, Generate Path, service URL, bootstrap/start 설정, cache 및 배포 버전 불일치를 확인한다.
- 수정이 Studio generate/build를 요구하면 정적 검증과 실행 검증을 분리해 보고한다.

## 완료 보고 체크리스트

- 확인한 원인과 변경 범위
- 정적으로 확인한 event, ID, Dataset 컬럼, Grid binding, transaction mapping
- 브라우저/NRE 중 검증한 대상
- Nexacro Studio generate, QuickView 또는 NRE에서 사용자가 추가로 확인할 항목

## 공식 자료

- [개발도구 가이드](https://docs.tobesoft.com/development_tools_guide_nexacro_17_ko)
- [응용 개발 가이드](https://docs.tobesoft.com/advanced_development_guide_nexacro_17_ko)
- [앱 배포 가이드](https://docs.tobesoft.com/deployment_guide_nexacro_17_ko)
