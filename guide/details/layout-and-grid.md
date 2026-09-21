# 가변 레이아웃·스타일·Grid 편집의 세부 사항

[매뉴얼 목차](../README.md) · 관련 문서: [레이아웃](../basics/ui/layout.md) / [Grid](../basics/data/grid.md)

여러 Layout, 내용에 따른 크기 변화, 셀 인덱스처럼 기본 설정만으로 해결되지 않는 부분을 확인합니다.

## 창 크기가 바뀌면 배치는 어떻게 유지하나요?

| 설정 | 역할 | 사용 예 |
| --- | --- | --- |
| px | 고정된 간격·크기 | 버튼 너비, 여백 |
| % | 부모 영역 크기에 비례 | 넓어지는 조회 결과 영역 |
| left + right | 양쪽 여백을 기준으로 너비 조정 | 좌우 20px 여백을 둔 Grid |
| top + bottom | 위아래 여백을 기준으로 높이 조정 | 남는 높이를 채우는 목록 |
| Arrangement | 다른 컴포넌트를 기준으로 상대 위치 지정 | 앞 입력창이 커져도 버튼 간격 유지 |
| fittocontents | 내용 크기에 맞춰 컴포넌트 크기 조정 | 길이가 달라지는 설명문 |

예를 들어 Grid를 `left=20`, `right=20`, `top=80`, `bottom=20`으로 두고 고정 `width/height`를 비우면, 부모 크기에 맞춰 영역을 확보할 수 있습니다. 같은 축의 위치·크기를 모두 고정하기보다 어떤 기준으로 늘어날지 정하세요. [공식 Position 설명](https://docs.tobesoft.com/development_tools_guide_nexacro_17_ko/06af719130eb5647)

Align은 편집할 때 여러 컴포넌트의 위치·간격을 맞추는 도구입니다. 실행 중 크기 변화에 따라 움직이려면 Position이나 Arrangement 설정이 필요합니다.

Form은 기본 Layout 외에 화면 크기·Screen에 대응하는 Layout을 추가할 수 있습니다. 단순한 크기 변화는 Position으로, 배치 자체가 달라지는 경우는 여러 Layout으로 구성합니다. [공식 Layout 생성 설명](https://docs.tobesoft.com/development_tools_guide_nexacro_17_ko/c2110744f6996894)

## 스타일은 어디에서 입히나요?

| 위치 | 적용 범위 | 작업 방식 |
| --- | --- | --- |
| Theme / XCSS | 앱과 컴포넌트의 공통 디자인 | 프로젝트의 스타일 리소스에서 정의·수정 |
| 컴포넌트 `cssclass` | 정의된 디자인 선택 | Properties에서 클래스명 지정 |
| 컴포넌트 개별 속성 | 해당 객체의 예외 표현 | `background`, `color`, `font` 등 지정 |

개발자는 보통 디자인 가이드의 클래스명을 `cssclass`에 지정합니다. 예를 들어 회사에 `btn_WF_Search`라는 Button 스타일이 정의되어 있다면 다음처럼 선택할 수 있습니다.

```javascript
this.btnSearch.set_cssclass("btn_WF_Search");
```

클래스명은 예시입니다. 문자열을 지정했다고 스타일이 새로 만들어지지는 않습니다. 프로젝트의 Theme/XCSS에 해당 컴포넌트용 정의가 있어야 합니다. Theme와 XCSS는 Studio에서 편집하는 스타일 리소스입니다. [공식 스타일 편집 설명](https://docs.tobesoft.com/development_tools_guide_nexacro_17_ko/34a012d680c30621)

스타일이 기대와 다르면 **클래스명·컴포넌트 종류 → 개별 속성 → disabled/readonly 같은 상태 → 생성·배포된 스타일 파일**을 확인합니다. `cssclass`를 바꾼다고 필수값 검사나 권한 처리가 생기는 것은 아닙니다.

## 내용에 따라 높이가 변하는 화면

`fittocontents`로 커진 영역 아래의 컴포넌트가 함께 이동하려면 Arrangement도 필요합니다. 강의의 데이터 바인딩 예제는 Form의 `onbindingvaluechanged`에서 `resetScroll()`을 호출해 스크롤 영역을 갱신합니다. 실제 프로젝트에서는 해당 화면의 스크롤·바인딩 구조와 기존 처리 여부를 함께 확인하세요.

## Script에서 셀을 바꿀 때 주의할 점은요?

`setCellProperty()` 같은 API는 band와 cell index를 사용합니다. 화면의 세 번째 열이 항상 cell index 2라는 보장은 없습니다. 셀 병합·여러 줄 포맷을 확인한 뒤 지정하세요.

저장 전에는 Grid에서 편집하던 마지막 값이 Dataset에 반영되었는지 확인합니다. 이 처리는 공통 저장 함수에 이미 있을 수 있으므로 기존 구현을 먼저 읽으세요.

## 관련 강의

강의: [4강 2:55 · cssclass](https://www.youtube.com/watch?v=233w6zyRlxg&t=175s), [6강 38:15 · 크기와 배치](https://www.youtube.com/watch?v=Q9NnAdtH_kU&t=2295s), [47:24 · 바인딩과 스크롤](https://www.youtube.com/watch?v=Q9NnAdtH_kU&t=2844s)

강의 자료: [3강](<../../youtube/기본03. 넥사크로 컴포넌트.md>), [4강](<../../youtube/기본04. 화면실습_데이터 바인드.md>), [6강](<../../youtube/기본06. 화면실습_데이터통신.md>)

강의: [5강 0:08 · 구조](https://www.youtube.com/watch?v=WoTH8nZgMK0&t=8s), [6:16 · Combo 셀](https://www.youtube.com/watch?v=WoTH8nZgMK0&t=376s), [12:16 · Expression](https://www.youtube.com/watch?v=WoTH8nZgMK0&t=736s)

강의 자료: [5강](<../../youtube/기본05. 화면실습_그리드.md>)
