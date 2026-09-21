# 5. 읽기 쉽고 편집하기 좋은 Grid

[학습 목차](README.md) · 이전: [바인딩](04-binding.md) · 다음: [데이터 통신](06-transaction.md)

> **이번 목표:** 부서 코드 대신 이름을 표시하고, 사원 수와 급여 합계를 보여준다.

## 핵심만 보기

| 구분 | 역할 |
| --- | --- |
| head / body / summary | 제목 / 각 행의 데이터 / 합계 영역 |
| displaytype | 평소 어떻게 보여줄지 |
| edittype | 편집할 때 어떤 입력 방식을 쓸지 |
| bind | 컬럼 값을 연결 |
| expr | 계산하거나 조건에 따라 값을 표현 |

## 따라 하기 ① 부서 코드 → 부서 이름

1. Grid를 더블클릭해 **Grid Contents Editor**를 엽니다.
2. head의 제목을 `사번`, `이름`, `부서`, `급여`로 정리합니다. body의 컬럼 연결은 유지하세요.
3. **body의 부서 셀**을 선택해 다음을 설정합니다.

| 속성 | 값 |
| --- | --- |
| text | `bind:DEPT_CD` |
| displaytype | `combotext` |
| edittype | `combo` |
| combodataset | `ds_dept` |
| combocodecol | `DEPT_CD` |
| combodatacol | `DEPT_NAME` |

실행하면 `D01` 대신 `개발팀`이 나옵니다. 부서 셀을 편집하면 Combo로 선택할 수 있고 상세의 부서도 함께 바뀝니다.

## 따라 하기 ② 순번과 합계

1. 맨 앞에 컬럼을 하나 추가하고 head의 text를 `No`로 지정합니다.
2. body의 새 셀에서 text의 **Set Expression**을 열고 `currow + 1`을 입력합니다.
3. 우클릭 메뉴의 **Add Summary Row**로 summary를 추가합니다.
4. summary의 첫 셀과 급여 셀에 아래 계산식을 각각 설정합니다.

| 위치 | Set Expression 창에 입력할 식 | 초기 데이터의 예상 결과 |
| --- | --- | --- |
| body의 No | `currow + 1` | 1, 2 |
| summary의 No | `dataset.getRowCount() + "건"` | 2건 |
| summary의 급여 | `dataset.getSum("SALARY")` | 7000000 |

Set Expression 창에는 **식만** 입력합니다. text 속성에 직접 작성하는 경우에는 `expr:currow + 1`처럼 `expr:`를 붙입니다.

급여 body·summary 셀의 `displaytype`을 `number`, `textAlign`을 `right`로 설정해 숫자를 읽기 쉽게 정리하세요. 이 실습의 순번은 표시 순서이며 사원을 식별하는 고유 사번이 아닙니다.

## 완료 체크

- [ ] 부서명이 보이고 Grid에서 부서를 바꿀 수 있다.
- [ ] 처음에는 `2건`, 급여 합계 `7000000`이 나온다.
- [ ] 상세에서 급여를 바꾸고 포커스를 옮기면 합계도 바뀐다.

**막혔다면:** 제목만 바뀌고 데이터가 그대로라면 head를 편집했는지 확인하세요. 합계가 이상하면 `SALARY`의 타입과 값을, 값 대신 수식이 보이면 Set Expression 사용 여부를 확인하세요.

## 필요한 영상만 보기

- [5강 0:08 · Grid 구조](https://www.youtube.com/watch?v=WoTH8nZgMK0&t=8s)
- [5강 6:16 · 부서 Combo](https://www.youtube.com/watch?v=WoTH8nZgMK0&t=376s)
- [5강 12:16 · 순번](https://www.youtube.com/watch?v=WoTH8nZgMK0&t=736s)
- [5강 18:27 · 급여 합계](https://www.youtube.com/watch?v=WoTH8nZgMK0&t=1107s)

원문: [5강](<../기본05. 화면실습_그리드.md>)
