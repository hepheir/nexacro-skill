# 프로젝트 구조와 Form

## 조사 순서

1. `.xprj`에서 `environment.xml`, `typedefinition.xml`, `appvariables.xml` 및 Application `.xadl` 참조 경로를 확인한다.
2. 선택된 `.xadl`에서 Application, MainFrame, Frame 구조, Application script와 event를 확인하고 `appvariables.xml`에서 전역 Dataset/Variable을 확인한다.
3. Environment 및 TypeDefinition에서 service prefix, protocol, 등록 객체와 component/module 의존성을 확인한다.
4. 대상 `.xfdl`의 Form 속성, objects, components, bind 정보, `<Script>` 및 이벤트 연결을 함께 읽는다.
5. include된 `.xjs`/`.js`와 Application 공통 영역에서 동일 함수명과 전역 규약을 검색한다.

파일명만 보고 구조를 단정하지 않는다. Nexacro Studio 설정과 프로젝트별 생성 방식에 따라 파일 구성이 달라질 수 있다.

## Form 생명주기와 이벤트

- 초기화 코드는 실제로 연결된 `oninit`/`onload` handler와 상위 Frame/Application 초기화 순서를 확인한 뒤 배치한다. 객체·컴포넌트 생성 직후의 `oninit`과 로딩 완료 후의 `onload` 역할을 바꾸지 않는다.
- 컴포넌트 이벤트 handler를 변경할 때는 XFDL 이벤트 속성과 script 함수명이 일치하는지 확인한다.
- Div, Tabpage, popup Form 등 중첩 Form에서는 `this`가 가리키는 Form 범위와 상위 Form 접근 방식을 기존 코드에서 확인한다. 초기 로딩에서는 URL로 연결된 자식 Form의 `onload`가 이를 포함한 부모 Form의 `onload`보다 먼저 발생하므로 자식에서 부모의 로딩 완료를 가정하지 않는다. `preload=false`인 비활성 Tabpage와 런타임에 URL을 설정한 Form은 이후에 로드될 수 있으므로 접근 시점을 별도로 검증한다.
- 화면 재진입, popup 재사용, 다중 호출 가능성이 있으면 Dataset 초기화와 동적 event handler 중복 등록 여부를 확인한다.

## 안전한 수정

- 컴포넌트 ID 변경은 binding, Grid expression, event handler, `lookup`/동적 참조, 공통함수 호출까지 검색한다.
- Dataset 컬럼 변경은 `<ColumnInfo>`, bind, Grid cell, expression, transaction 계약을 모두 추적한다.
- XML을 직접 수정할 때는 기존 serialization 형식과 script CDATA 경계를 보존한다.
- 생성된 JavaScript 결과물을 원본 XFDL 대신 수정하지 않는다. 어느 파일이 원본인지 불명확하면 먼저 확인한다.

## 공식 자료

- [Nexacro Platform 17 전체 매뉴얼](https://docs.tobesoft.com/nexacro_17_ko)
- [응용 개발 가이드](https://docs.tobesoft.com/advanced_development_guide_nexacro_17_ko)
- [개발도구 가이드](https://docs.tobesoft.com/development_tools_guide_nexacro_17_ko)
- [제품 정보](https://docs.tobesoft.com/product_information_nexacro_17_ko)
