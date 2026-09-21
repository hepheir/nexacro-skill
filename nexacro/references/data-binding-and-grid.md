# Dataset, Binding, Grid

## Dataset 확인

- Dataset ID, `<ColumnInfo>`의 컬럼명·type·size, 초기 `<Rows>`, `useclientlayout`, key 역할 컬럼을 확인한다.
- 조회 후 값이 보이지 않으면 서버 응답 컬럼과 Dataset 컬럼, output mapping, bind column을 차례로 대조한다.
- 값 변경 로직은 현재 row가 유효한지 확인하고 `getColumn`/`setColumn`을 사용한다. rowposition 변경이 의도한 이벤트를 일으키는지도 확인한다.
- 저장 로직에서는 원본값, 삭제 row, row type을 고려한다. 단순 `rowcount`만으로 변경 여부를 판단하지 않는다.

대표 행 상태 점검 예시:

```javascript
var rowType = this.dsEmployee.getRowType(row);
if (rowType == Dataset.ROWTYPE_INSERT || rowType == Dataset.ROWTYPE_UPDATE) {
    // 변경 행 처리
}
```

일반 Form script에서는 공식 예제의 `Dataset.ROWTYPE_*` 표기를 사용한다. 프로젝트 wrapper가 숫자나 별도 상수로 감싼 경우에는 정의를 확인한 뒤 기존 표기를 따른다. 삭제 데이터는 일반 행과 별도 영역에서 관리될 수 있으므로 저장 계약을 확인한다.

Dataset에 filter가 적용되어 있으면 일반 `rowcount`와 `getRowType()` 순회만으로 숨겨진 변경 행을 놓칠 수 있다. 대상 빌드가 지원하면 `getRowCountNF()`와 `getRowTypeNF()`로 필터와 무관한 행을 검사하고, 삭제 영역은 `getDeletedRowCount()`로 별도 검사한다. NF 계열을 지원하지 않는 구형 빌드에서는 기존 filter를 보존한 채 안전하게 해제·복원하는 프로젝트 패턴을 확인한다.

## Binding

- 컴포넌트의 `value`, `text`, `index` 중 실제로 binding된 속성을 확인한다.
- `BindItem`의 `datasetid`, `columnid`, `compid`, `propid`를 한 세트로 검증한다.
- Dataset 값은 맞는데 화면이 틀리면 expression, displaytype/edittype, format mask, enable/readOnly 조건을 확인한다.

## Grid

- Grid의 `binddataset`과 format의 `text="bind:COLUMN"` 연결을 우선 확인한다.
- body/head/summary band와 실제 cell index를 구분한다. `setCellProperty`를 사용할 때 band와 index가 맞는지 확인한다.
- 정렬·필터·expression이 적용된 화면에서는 화면상의 행과 Dataset row 관계를 단정하지 않는다.
- Grid format을 바꿀 때 컬럼 ID와 사용자 정의 expression을 보존하고, head/body cell의 대응이 깨지지 않는지 검사한다.

간단한 값 변경 예시:

```javascript
var row = this.dsEmployee.rowposition;
if (row < 0) return;
this.dsEmployee.setColumn(row, "SELECTED", "1");
```

`dsEmployee`, `SELECTED`는 예시 ID다. 실제 작업에서는 프로젝트 정의를 사용한다.

## 공식 자료

- [Nexacro Platform 17 전체 매뉴얼](https://docs.tobesoft.com/nexacro_17_ko)
- 공식 매뉴얼에서 `Dataset`, `BindItem`, `Grid`, `GridCellControl`, `getRowType`, `getOrgColumn` 항목을 검색한다.
