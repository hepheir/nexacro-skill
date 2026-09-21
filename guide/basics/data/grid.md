# Grid의 표시 모양과 편집 방식은 어떻게 정하나요?

[매뉴얼 목차](../../README.md)

**Grid Contents Editor에서 body 셀의 표시·편집 속성을 설정합니다.** 제목을 바꾸는 작업과 데이터 셀을 바꾸는 작업을 구분하세요.

## Grid의 세 영역

| 영역 | 역할 |
| --- | --- |
| head | 제목: 사번·이름·부서 |
| body | Dataset의 각 행 |
| summary | 건수·합계 |

Grid를 더블클릭해 편집합니다. 값이 보이지 않으면 Dataset Rows → Grid의 `binddataset` → body의 `text=bind:컬럼명`을 확인합니다.

## 표시와 편집은 별도 설정입니다

| 용도 | displaytype | edittype |
| --- | --- | --- |
| 문자열 표시·입력 | normal | text |
| 선택지의 이름 표시 | combotext | combo |
| Combo 모양 계속 표시 | combocontrol | combo |
| 체크 표시·편집 | checkboxcontrol | checkbox |

숫자 표시는 `number`를 사용할 수 있습니다. 편집 가능 여부는 edittype과 읽기 전용 설정을 함께 확인합니다.

## 부서 코드 대신 이름 보여주기

```text
text           = bind:DEPT_CD
displaytype    = combotext
edittype       = combo
combodataset   = ds_dept
combocodecol   = DEPT_CD
combodatacol   = DEPT_NAME
```

예시 설정에서는 `개발팀`을 보여주고 Dataset에는 `D01`을 저장합니다. 상세 Combo도 같은 컬럼을 바인딩하면 변경이 함께 반영됩니다.

이미 편집한 Grid 포맷을 다시 생성하면 기존 셀 설정이 바뀔 수 있습니다. 컬럼 추가·재생성 전에는 바인딩과 표현식을 확인하세요.

---

관련 문서: [순번·합계 표현식](grid-expression.md) · [셀 인덱스와 편집 확정](../../details/layout-and-grid.md)

강의: [5강 6:16 · Combo 셀](https://www.youtube.com/watch?v=WoTH8nZgMK0&t=376s)
