# 어떤 컴포넌트를 선택하면 되나요?

[매뉴얼 목차](../../README.md)

**입력할 정보와 사용자 동작에 맞춰 컴포넌트를 고릅니다.** 처음에는 각 컴포넌트의 모든 속성보다 용도를 구분하면 됩니다.

## 자주 쓰는 컴포넌트

| 목적 | 컴포넌트 | 먼저 볼 속성 |
| --- | --- | --- |
| 항목명·설명 | Static | text |
| 동작 실행 | Button | text, onclick |
| 한 줄 / 여러 줄 입력 | Edit / TextArea | value |
| 숫자·문자 형식 입력 | MaskEdit | type, format |
| 날짜 입력 | Calendar | value, dateformat |
| 목록에서 선택 | Combo / ListBox / Radio | innerdataset, value |
| 체크 여부 | CheckBox | value, truevalue, falsevalue |
| 표 조회·편집 | Grid | binddataset |
| 영역 묶기 | Div | 위치·크기, url |
| 탭별 화면 | Tab / Tabpage | 탭과 포함 Form |

Dataset은 데이터를 보관하는 객체입니다. 컴포넌트와 함께 사용하지만 화면에 직접 표시되지는 않습니다.

## 사원 화면에 적용하면

사원 목록은 Grid, 이름은 Edit, 부서는 Combo, 급여는 숫자 MaskEdit로 표현할 수 있습니다. 이름 입력창처럼 보이더라도 사번의 앞자리 0을 보존해야 한다면 데이터는 문자열로 설계합니다.

ID는 코드에서 객체를 찾는 이름이고 text는 화면에 표시할 글자입니다. ID를 바꾸면 관련 Script·이벤트·바인딩 참조도 확인해야 합니다.

## 같은 Form을 보는 세 탭

Design은 배치와 속성, Source는 XFDL의 XML 구조, Script는 이벤트와 업무 코드를 편집합니다. 별개의 화면 세 개가 아니라 **같은 Form을 다른 방식으로 보는 탭**입니다.

---

관련 문서: [레이아웃 구성](layout.md) · [스타일 적용](styles.md)

강의 자료: [3강 컴포넌트](<../../../youtube/기본03. 넥사크로 컴포넌트.md>)
