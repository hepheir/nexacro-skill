# 화면 크기가 바뀌어도 배치를 유지하려면요?

[매뉴얼 목차](../../README.md)

**어느 영역은 고정하고 어느 영역은 늘릴지 정한 뒤 Position을 설정합니다.** 편집 화면에서 보기 좋게 정렬하는 것과 실행 중 크기 변화에 대응하는 것은 다릅니다.

## 영역과 크기 기준

앱 전체의 상단·메뉴·업무 화면 틀은 Application의 Frame 구성에서 확인합니다. 업무 Form 내부는 Div와 Tab으로 묶을 수 있습니다.

| 설정 | 동작 | 사용 예 |
| --- | --- | --- |
| px | 고정 크기·간격 | 버튼 너비, 여백 |
| % | 부모 크기에 비례 | 넓어지는 입력 영역 |
| left + right | 양쪽 여백을 유지하며 너비 조정 | 좌우에 여백을 둔 Grid |
| top + bottom | 위아래 여백을 유지하며 높이 조정 | 남는 높이를 채우는 목록 |
| Arrangement | 다른 컴포넌트 기준의 상대 위치 | 입력창 옆 버튼 간격 유지 |

Grid를 `left=20`, `right=20`, `top=80`, `bottom=20`으로 두고 고정 width/height를 비우면 부모 크기에 맞춰 영역을 확보할 수 있습니다. [공식 Position 설명](https://docs.tobesoft.com/development_tools_guide_nexacro_17_ko/06af719130eb5647)

## Align과 Arrangement의 차이

Align은 Studio에서 여러 컴포넌트의 위치·크기·간격을 맞추는 도구입니다. 실행 중에도 다른 컴포넌트의 변화에 따라 움직이려면 Position이나 Arrangement가 필요합니다.

단순히 크기만 바뀌면 Position으로, 화면 크기에 따라 배치 자체를 바꾸려면 여러 Layout으로 구성할 수 있습니다. `fittocontents`로 컴포넌트 크기가 달라질 때는 인접 컴포넌트의 Arrangement와 Form의 스크롤 영역도 함께 확인합니다.

---

관련 문서: [스타일 적용](styles.md) · [여러 Layout·내용 크기·스크롤](../../details/layout-and-grid.md)

강의: [6강 38:15 · 크기와 배치](https://www.youtube.com/watch?v=Q9NnAdtH_kU&t=2295s)
