# 대표 요청과 응답 패턴

이 문서는 답변 문구를 고정하지 않는다. 실제 프로젝트 정보를 우선하면서 누락되기 쉬운 판단을 확인하는 데 사용한다.

## 1. 조회 화면 생성

요청: “부서별 사원 조회 화면을 만들어줘.”

좋은 처리:

- 기존 Form template, Dataset ID/컬럼, service prefix, transaction wrapper를 먼저 찾는다.
- 정보가 없다면 필요한 계약을 질문하거나 `<EMPLOYEE_SERVICE_URL>` 같은 자리표시자를 쓴다.
- Dataset, BindItem, Grid `binddataset`/format, 조회 Button event, callback의 연결을 한 흐름으로 제시한다.
- `dsEmployee`, `EMP_ID` 같은 이름이 예시임을 밝힌다.

## 2. Transaction 오류 수정

요청: “조회 callback은 성공인데 Grid가 비어 있어.”

좋은 진단 순서:

1. output mapping의 로컬/서버 Dataset 이름을 확인한다.
2. callback 시점의 `rowcount`를 확인한다.
3. Grid `binddataset`을 확인한다.
4. body cell의 bind column과 Dataset `<ColumnInfo>`를 대조한다.
5. filter/expression/format 문제를 확인한다.

근거 없이 callback에 `Grid.redraw()`만 추가하지 않는다.

## 3. 최소 리팩터링

요청: “중복된 버튼 이벤트를 정리해줘.”

좋은 처리:

- 연결된 event handler와 외부 호출 여부를 검색한다.
- 공통 동작만 작은 Form helper로 추출하고 handler 이름은 유지한다.
- 전역 공통 스크립트로 승격하지 않는다.
- 변경 전후의 validation과 transaction 호출 순서가 같은지 확인한다.

## 4. Dataset 변경 감지

요청: “저장 버튼 활성화가 삭제 행을 놓쳐.”

좋은 처리:

- 현재 행의 `getRowType()` 검사뿐 아니라 삭제 행 보관 영역도 확인한다.
- 프로젝트의 기존 변경 감지 helper가 있으면 재사용한다.
- 저장 성공 후 변경 상태를 확정하는 방식이 재조회인지 `applyChange()`인지 기존 규약을 따른다.

## 5. 프로젝트 고유 helper

요청 파일에 `gfnTransaction`, `gfnOpenPopup`, `gfnAlert`가 포함된 경우:

- 정의와 실제 호출례에서 signature를 확인한다.
- 표준 `transaction`, `open`, `alert`로 곧바로 치환하지 않는다.
- helper가 표준 API가 아니라 프로젝트 함수임을 설명한다.

## 6. Nexacro N 자료만 발견된 경우

요청: “N 예제의 MultiCombo를 17 화면에 그대로 추가해줘.”

좋은 처리:

- Nexacro 17 TypeDefinition과 공식 17 문서에서 해당 컴포넌트 지원 여부를 확인한다.
- 17 지원 근거가 없으면 동일 API라고 가정하지 않는다.
- 설치 module 또는 대체 UI가 필요한지 분리해서 설명하고 사용자 선택 없이 의존성을 추가하지 않는다.

## 학습 자료

- [Nexacro 17 YouTube 강의 재생목록](https://www.youtube.com/playlist?list=PL103FbwuueMkdMvz18Gu2TyteV6AdWUGU): 주제 순서와 실무 흐름을 참고한다.
- [Nexacro Platform 17 공식 매뉴얼](https://docs.tobesoft.com/nexacro_17_ko): API 및 동작 사실의 최종 기준으로 사용한다.
