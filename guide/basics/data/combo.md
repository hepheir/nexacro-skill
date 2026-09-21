# Combo에는 왜 두 종류의 데이터를 연결하나요?

[매뉴얼 목차](../../README.md)

**고를 수 있는 목록과 현재 선택값의 역할이 다르기 때문입니다.** 부서 Combo라면 전체 부서 목록과 현재 사원의 부서가 각각 필요합니다.

## 부서 선택 예시

| 설정 | 예시 | 역할 |
| --- | --- | --- |
| innerdataset | ds_dept | 선택 가능한 부서 목록 |
| codecolumn | DEPT_CD | 실제 값: D01 |
| datacolumn | DEPT_NAME | 표시명: 개발팀 |
| value 바인딩 | ds_emp.DEPT_CD | 현재 사원이 선택한 부서 |

사용자에게 `개발팀`이 보이더라도 사원 데이터에는 `D01`을 저장할 수 있습니다. 부서명을 바꾸어도 식별할 코드를 별도로 관리하는 구조입니다.

## Studio에서 연결하기

먼저 `ds_dept`를 Combo에 드래그하고 Bind InnerDataset으로 코드·표시명 컬럼을 지정합니다. 이어 `ds_emp`를 드래그해 Bind Item으로 `DEPT_CD`를 Combo의 `value`에 연결합니다.

이름이 비슷해도 두 설정을 구분하세요. InnerDataset은 목록의 내용, value 바인딩은 현재 사원의 값을 정합니다.

## 목록만 나오고 현재 값이 안 보이면

현재 사원의 부서 코드와 목록의 코드가 일치하는지 확인합니다. `D01`이 선택값인데 목록에는 `01`만 있으면 기대한 이름을 표시할 수 없습니다.

목록을 서버에서 가져온다면 그 데이터가 아직 도착하지 않았을 수도 있습니다. 코드 목록과 사원 조회의 순서가 필요한 화면은 callback 흐름을 확인합니다. Grid의 Combo 셀도 같은 원리지만 설정 속성 이름은 다릅니다.

---

관련 문서: [Grid의 Combo 셀](grid.md) · [callback과 조회 순서](../communication/callbacks.md)

강의: [4강 34:23 · 목록과 선택값](https://www.youtube.com/watch?v=233w6zyRlxg&t=2063s)
