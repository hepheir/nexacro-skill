# 컴포넌트에 스타일은 어떻게 적용하나요?

[매뉴얼 목차](../../README.md)

**보통 회사 디자인 가이드의 클래스명을 `cssclass`에 지정합니다.** 클래스 이름은 이미 정의된 스타일을 선택하는 값입니다.

## 스타일을 정하는 세 위치

| 위치 | 역할 |
| --- | --- |
| Theme / XCSS | 공통 디자인 정의 |
| 컴포넌트의 cssclass | 적용할 디자인 선택 |
| background·color·font 등 개별 속성 | 특정 객체의 표현 설정 |

Design에서 컴포넌트를 선택하고 Properties의 `cssclass`를 지정합니다. Script에서도 변경할 수 있습니다.

```javascript
this.btnSearch.set_cssclass("btn_WF_Search");
```

`btn_WF_Search`는 예시입니다. 프로젝트에 해당 Button 스타일이 있어야 적용됩니다. 문자열을 지정하는 것만으로 스타일이 새로 생기지는 않습니다. [공식 Theme/XCSS 설명](https://docs.tobesoft.com/development_tools_guide_nexacro_17_ko/34a012d680c30621)

## 같은 클래스인데 모양이 다르면

클래스명과 컴포넌트 종류, 개별 속성, disabled/readonly 같은 상태를 확인합니다. 다른 Button에서는 잘 보인다면 두 객체의 속성을 비교하면 됩니다. 모든 화면에서 이전 디자인이 보인다면 생성·배포된 스타일 파일도 확인하세요.

여러 화면의 디자인을 바꿀 때는 공유 스타일의 사용처를 살펴봅니다. 한 화면의 작은 조정인지 공통 디자인 변경인지에 따라 수정 위치가 달라집니다.

## 디자인과 기능은 따로 설정합니다

필수 항목용 cssclass를 지정해도 필수값 검사가 자동으로 생기지는 않습니다. 입력 검증·이벤트·권한 처리는 해당 로직에서 다룹니다.

---

관련 문서: [이벤트 등록](events.md) · [스타일과 상태 확인](../../details/layout-and-grid.md)

강의: [4강 2:55 · cssclass](https://www.youtube.com/watch?v=233w6zyRlxg&t=175s)
