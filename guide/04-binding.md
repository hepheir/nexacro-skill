# 4. Dataset 하나로 목록과 상세 연결하기

[학습 목차](README.md) · 이전: [컴포넌트](03-components.md) · 다음: [Grid](05-grid.md)

> **이번 목표:** 목록에서 다른 사원을 선택하면 상세 정보도 함께 바뀐다.

## 핵심만 보기

- **Dataset:** 행과 열로 데이터를 보관하는 객체. 화면에는 직접 보이지 않습니다.
- **Binding:** Dataset 컬럼과 컴포넌트 속성을 연결하는 설정입니다.
- **InnerDataset:** Combo 등에 표시할 선택지 목록입니다.

```text
                         ┌→ Grid: 여러 사원 표시
사원 Dataset ds_emp ──────┤
                         └→ 상세 입력창: 현재 행 표시·수정
부서 Dataset ds_dept ───────→ Combo: 선택 가능한 부서 목록
```

## 따라 하기 ① 테스트 데이터

Form에 Dataset을 추가하고 ID를 `ds_emp`로 지정합니다. Invisible Object 영역에서 더블클릭해 Dataset Editor를 엽니다. Columns와 Rows에 아래 내용을 만드세요. 크기와 값은 이 가이드의 연습용 정의입니다.

| Column ID | Type | Size |
| --- | --- | --- |
| EMPL_ID | STRING | 20 |
| FULL_NAME | STRING | 50 |
| DEPT_CD | STRING | 10 |
| SALARY | INT | 기본값 |

| EMPL_ID | FULL_NAME | DEPT_CD | SALARY |
| --- | --- | --- | --- |
| E001 | 김하나 | D01 | 3000000 |
| E002 | 이두리 | D02 | 4000000 |

`ds_dept`도 추가합니다. `DEPT_CD`는 STRING/10, `DEPT_NAME`은 STRING/50으로 만들고 다음 두 행을 넣습니다.

| DEPT_CD | DEPT_NAME |
| --- | --- |
| D01 | 개발팀 |
| D02 | 기획팀 |

샘플의 Dataset을 사용한다면 이미 있는 컬럼·데이터를 확인하고 활용하세요. 실제 서버 연동 시에는 **서버가 주고받는 컬럼명·타입·크기**에 맞춰야 합니다.

## 따라 하기 ② 목록과 상세

1. `ds_emp`를 Grid에 드래그해서 컬럼을 생성합니다. Grid의 `binddataset`이 `ds_emp`인지 확인합니다.
2. `ds_emp`를 이름 Edit에 드래그하고 Bind Item에서 `FULL_NAME`을 선택합니다. 연결 속성은 `value`입니다.
3. 같은 방법으로 사번 Edit의 `value`는 `EMPL_ID`, 급여 MaskEdit의 `value`는 `SALARY`에 연결합니다.
4. 급여 MaskEdit의 `type`을 `number`, `format`을 `#,##0`으로 지정합니다.
5. 실행하고 Grid의 행을 바꿉니다. 상세 값이 바뀌는지 확인합니다.
6. 상세 이름을 수정하고 다른 입력창으로 포커스를 옮깁니다. Grid의 이름도 바뀌는지 확인합니다.

## 따라 하기 ③ 부서 Combo — 연결은 두 번

| 설정 | 값 | 역할 |
| --- | --- | --- |
| innerdataset | `ds_dept` | 선택지 공급 |
| codecolumn | `DEPT_CD` | 실제 저장할 코드 |
| datacolumn | `DEPT_NAME` | 화면에 보여줄 이름 |
| value 바인딩 | `ds_emp.DEPT_CD` | 현재 사원의 부서 |

먼저 `ds_dept`를 Combo에 드래그해 **Bind InnerDataset**을 설정합니다. 이어 `ds_emp`를 드래그해 **Bind Item**으로 `DEPT_CD`를 `value`에 연결합니다.

**예상 결과:** E001을 선택하면 `개발팀`이 보입니다. Combo에서 `기획팀`을 선택하면 사원 Dataset에는 이름 대신 `D02`가 저장됩니다.

## 완료 체크

- [ ] 행을 바꾸면 이름·사번·급여·부서가 함께 바뀐다.
- [ ] 이름을 수정하면 Grid에도 반영된다.
- [ ] Combo의 목록 데이터와 선택값 데이터가 왜 다른지 설명할 수 있다.

**막혔다면:** Grid가 비면 Dataset의 Rows와 `binddataset`부터 확인하세요. Combo 목록만 나오고 현재 부서가 선택되지 않으면 `value` 바인딩과 양쪽 부서 코드가 일치하는지 확인하세요. 컬럼명의 대소문자도 구분합니다.

## 필요한 영상만 보기

- [4강 12:35 · Dataset 만들기](https://www.youtube.com/watch?v=233w6zyRlxg&t=755s)
- [4강 17:35 · Grid 바인딩](https://www.youtube.com/watch?v=233w6zyRlxg&t=1055s)
- [4강 19:22 · 상세 바인딩](https://www.youtube.com/watch?v=233w6zyRlxg&t=1162s)
- [4강 34:23 · 목록형 컴포넌트](https://www.youtube.com/watch?v=233w6zyRlxg&t=2063s)

원문: [4강](<../기본04. 화면실습_데이터 바인드.md>)
