# 목록과 상세 화면은 어떻게 함께 바뀌나요?

[매뉴얼 목차](../../README.md)

**Grid와 상세 입력창을 같은 Dataset에 바인딩하면 됩니다.** Grid에서 현재 행이 바뀔 때 상세 입력창도 해당 행을 보여줍니다.

```text
                    ┌─ Grid: 여러 사원 표시
           ds_emp ──┤
                    └─ Edit 등: 현재 사원의 컬럼 표시·수정
```

## 무엇을 연결하나요?

| 대상 | 연결 설정 |
| --- | --- |
| Grid | binddataset = ds_emp |
| Grid의 이름 셀 | text = bind:FULL_NAME |
| 이름 Edit | ds_emp의 FULL_NAME → Edit의 value |
| Div 안의 이름 Edit | 위 설정 + 정확한 컴포넌트 경로 |

Edit 같은 컴포넌트는 BindItem으로 Dataset·컬럼·컴포넌트·속성을 연결합니다. 대부분 입력값은 `value`지만 실제로 어떤 속성을 연결했는지 확인해야 합니다.

## Studio에서 연결하는 방법

Dataset을 Grid나 입력 컴포넌트에 드래그해 연결할 수 있습니다. 입력창에 연결할 때는 Bind Item 창에서 컬럼과 속성을 확인합니다. Div 안의 객체라면 `divDetail.form.edtName`처럼 경로도 맞아야 합니다.

상세에서 이름을 수정하면 같은 Dataset을 보는 Grid에도 반영됩니다. 단순히 값을 함께 표시하기 위해 매번 복사하는 Script를 작성할 필요는 없습니다.

## 값이 보이지 않으면

Dataset의 Rows → 현재 행 → 컬럼명 → 바인딩 속성 순서로 확인합니다. 데이터가 있어도 현재 행이나 연결 속성이 잘못되면 상세는 비어 있을 수 있습니다.

입력 중인 마지막 값은 편집 확정 시점과 관련됩니다. 저장할 때는 화면에 보이는 입력값이 Dataset에도 반영됐는지 확인하세요.

---

관련 문서: [Combo의 목록과 선택값](combo.md) · [Grid 표시·편집](grid.md)

강의: [4강 17:35 · 바인딩](https://www.youtube.com/watch?v=233w6zyRlxg&t=1055s)
