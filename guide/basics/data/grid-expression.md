# Grid에 순번과 합계를 표시하려면요?

[매뉴얼 목차](../../README.md)

**Expression으로 셀에 보여줄 값을 계산합니다.** Dataset 컬럼을 그대로 보여주는 bind와 계산해서 보여주는 expr를 구분합니다.

## 어디에 입력하나요?

Grid Contents Editor에서 셀을 선택하고 text의 **Set Expression**을 엽니다. 이 창에는 식만 입력합니다. text 속성에 직접 쓴다면 `expr:currow + 1`처럼 접두어를 붙입니다.

| 목적 | 식 | 위치 |
| --- | --- | --- |
| 순번 | currow + 1 | body |
| 건수 | dataset.getRowCount() + "건" | summary |
| 급여 합계 | dataset.getSum("SALARY") | summary |
| 사번과 이름 | EMPL_ID + " / " + FULL_NAME | body |

`dataset`은 Grid에 바인딩된 Dataset입니다. 합계를 계산할 컬럼의 자료형과 실제 값도 확인하세요.

## 데이터 자체를 바꾸는 기능인가요?

표현식은 **보여줄 값을 계산**합니다. 사번과 이름을 합쳐 표시해도 원래 컬럼이 합쳐지는 것은 아닙니다. DB 데이터 역시 이 설정만으로 바뀌지 않습니다.

순번은 표시 순서이며 사원 고유 식별자가 아닙니다. 수정·삭제할 사원을 서버에 전달할 때는 사번처럼 업무에서 정한 식별자를 사용합니다.

## 결과가 예상과 다르면

표현식을 입력한 band가 맞는지, 컬럼명이 일치하는지 확인합니다. 필터·정렬이 적용된 화면에서는 현재 표시되는 행과 계산 대상도 확인해야 합니다.

Script로 셀 속성을 변경한다면 열의 위치와 cell index를 단정하지 않습니다. 병합 셀이나 여러 줄 포맷에서는 화면의 열 순서와 실제 cell index가 다를 수 있습니다.

---

관련 문서: [서버 조회 요청](../communication/transaction.md) · [Grid 편집 주의점](../../details/layout-and-grid.md)

강의: [5강 12:16 · Expression](https://www.youtube.com/watch?v=WoTH8nZgMK0&t=736s)
