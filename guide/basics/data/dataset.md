# Dataset은 DB 테이블인가요?

[매뉴얼 목차](../../README.md)

**Dataset은 화면에서 데이터를 보관하는 메모리상의 객체입니다.** 표처럼 행과 열이 있지만 DB 테이블 자체는 아니며, DB와 자동으로 연결되지 않습니다.

## 무엇을 보관하나요?

| 요소 | 의미 |
| --- | --- |
| Columns | 컬럼 ID·자료형·크기 등의 구조 |
| Rows | 실제 데이터 |
| rowposition | 현재 행. 유효한 행이 없으면 -1 |
| 행 상태·원본값·삭제 데이터 | 저장 시 변경된 내용을 구분하는 정보 |

Dataset은 Grid 없이도 사용할 수 있습니다. 서버 응답을 담을 수도 있고 Studio의 Dataset Editor에서 테스트 데이터를 넣을 수도 있습니다.

## 어디서 만드나요?

Form에 Dataset을 추가하면 Invisible Object 영역에 나타납니다. 더블클릭해서 Columns와 Rows를 편집합니다. Dataset 자체는 실행 화면에 보이지 않으며 Grid나 입력 컴포넌트에 바인딩해서 표시합니다.

## 데이터를 바꾸면 무슨 일이 생기나요?

```javascript
var row = this.ds_emp.rowposition;
if (row >= 0) {
    this.ds_emp.setColumn(row, "DEPT_CD", "D01");
}
```

현재 행의 부서 코드가 바뀝니다. 같은 값에 바인딩된 화면에도 반영될 수 있지만 **이 코드로 DB가 수정되지는 않습니다.** `addRow()`와 `deleteRow()`도 화면 데이터의 추가·삭제입니다.

DB 반영은 서버로 저장 요청을 보내고 서버가 처리해야 이루어집니다. 다른 사용자의 DB 변경을 받으려면 재조회 등 별도의 갱신 동작도 필요합니다.

---

관련 문서: [Dataset 설계](dataset-design.md) · [화면 바인딩](binding.md)

강의: [4강 10:30 · Dataset](https://www.youtube.com/watch?v=233w6zyRlxg&t=630s)
