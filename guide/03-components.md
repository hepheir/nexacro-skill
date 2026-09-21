# 3. 사원관리 화면의 뼈대 만들기

[학습 목차](README.md) · 이전: [첫 화면](02-hello.md) · 다음: [바인딩](04-binding.md)

> **이번 목표:** 어떤 정보를 어떤 컴포넌트로 보여줄지 정하고 화면에 배치한다.

## 핵심만 보기

| 보여줄 정보 | 컴포넌트 | 연습용 ID |
| --- | --- | --- |
| 사원 목록 | Grid | `grdEmp` |
| 이름·사번 | Edit | `edtName`, `edtId` |
| 부서 선택 | Combo | `cboDept` |
| 급여 | MaskEdit | `mskSalary` |
| 상세 영역 묶기 | Div | `divDetail` |
| 항목 이름 | Static | 자유롭게 지정 |
| 실행 동작 | Button | `btnSearch`, `btnAdd`, `btnDelete`, `btnSave` |

Calendar는 날짜 입력, CheckBox는 체크 여부, Radio는 몇 개의 선택지 중 하나를 고를 때 사용합니다. 먼저 위 표의 작은 화면을 완성하고 확장하세요.

## 따라 하기

1. 샘플의 `Form_Emp_Exe`를 열거나, 새 `EmployeePractice` Form을 만듭니다. 아래는 **새 Form 기준**입니다. 샘플에서는 기존 컴포넌트 ID를 확인해 대응시키세요.
2. 상단에 조회·추가·삭제·저장 Button 4개, 왼쪽에 Grid, 오른쪽에 Div를 배치합니다.
3. **Div 안에** 이름·사번 Edit, 부서 Combo, 급여 MaskEdit와 제목 Static을 배치합니다.
4. 각 ID를 위 표대로 지정합니다. 이미 같은 ID가 있다면 중복 생성하지 않습니다.
5. 여러 컴포넌트를 선택해 Align으로 왼쪽 위치와 너비를 맞춥니다. 기준 컴포넌트의 진한 테두리를 확인하세요.
6. QuickView에서 입력 영역과 버튼이 잘 보이는지 확인합니다. 아직 목록과 버튼이 동작하지 않아도 괜찮습니다.

```text
Form
├─ grdEmp
└─ divDetail
   └─ form
      ├─ edtName
      ├─ edtId
      ├─ cboDept
      └─ mskSalary
```

Form Script에서 Div 안의 이름 입력창에 접근하는 경로는 `this.divDetail.form.edtName`입니다. 화면상으로 Div 위에 겹쳐 보여도 실제 부모가 Div인지 확인하세요.

## 완료 체크

- [ ] 목록과 상세 영역을 구분해 배치했다.
- [ ] 컴포넌트의 ID와 화면에 보이는 text를 구분한다.
- [ ] Div 안의 컴포넌트 접근 경로를 찾을 수 있다.

**막혔다면:** 샘플의 `cssclass`는 프로젝트에 해당 스타일이 있어야 적용됩니다. 새 프로젝트에서는 스타일 복제보다 배치와 동작 확인을 먼저 끝내세요.

## 필요한 영상만 보기

- [3강 39:10 · 기본 컴포넌트](https://www.youtube.com/watch?v=c_Bfona4Hns&t=2350s)
- [4강 0:53 · 실습 Form 찾기](https://www.youtube.com/watch?v=233w6zyRlxg&t=53s)
- [4강 6:38 · 상세 영역 배치](https://www.youtube.com/watch?v=233w6zyRlxg&t=398s)

원문: [3강](<../기본03. 넥사크로 컴포넌트.md>), [4강](<../기본04. 화면실습_데이터 바인드.md>)
