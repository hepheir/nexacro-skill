# 공통 스크립트와 화면 규약

## 공통함수 조사

- 함수명만으로 동작을 추측하지 말고 정의, 호출부, include 순서, 반환값과 side effect를 확인한다.
- 공통 transaction wrapper는 service ID 생성, URL 변환, argument 보강, 공통 callback, progress 표시를 포함할 수 있다.
- validation, 메시지, popup helper도 프로젝트별 callback 방식과 return 계약이 다를 수 있다.
- 같은 이름의 Form 함수와 공통 함수가 있으면 호출 scope를 확인한다.

## Validation

- 필수값, 길이, 범위, 형식, 행 단위 오류를 서버 계약과 화면 입력 규칙에 맞춘다.
- Grid 편집 중인 값이 Dataset에 반영되는 시점과 validation 실행 시점을 확인한다.
- 첫 오류에서 중단하는지 전체 오류를 모으는지는 기존 UX 규칙을 따른다.
- 실패 시 focus 이동이나 Grid cell 이동이 필요하면 대상 컴포넌트가 실제로 활성화 가능한지 확인한다.

## 메시지와 팝업

- `alert`/`confirm`으로 기존 메시지 코드 체계를 우회하지 않는다.
- popup argument 이름, modal/modeless 여부, callback 이름과 반환 객체 구조를 기존 호출례에서 확인한다.
- popup callback은 취소, 닫기, 빈 반환, 중복 호출을 안전하게 처리한다.

일반 API만으로 설명할 때의 최소 popup 예시는 가상 helper와 혼동하지 않도록 표시한다:

```javascript
// 예시일 뿐이며 실제 프로젝트의 popup wrapper를 먼저 확인한다.
nexacro.open(
    "popEmployee",
    "Employee::EmployeePopup.xfdl",
    this.getOwnerFrame(),
    { department: department }
);
```

추가 style, 위치, 크기, opener가 필요하면 대상 Nexacro 17 빌드의 `nexacro.open()` signature를 공식 문서에서 확인해 뒤쪽 인자를 추가한다.

## 공통화 판단

- 한 화면에서만 필요한 짧은 동작은 성급히 전역 공통함수로 올리지 않는다.
- 여러 화면에서 이미 반복되는 계약이 있고 include/lifecycle 영향을 설명할 수 있을 때만 공통화를 제안한다.
- 공통함수 변경 시 전체 호출부의 argument와 반환값 호환성을 검색한다.

## 공식 자료

- [Nexacro Platform 17 전체 매뉴얼](https://docs.tobesoft.com/nexacro_17_ko)
- [응용 개발 가이드](https://docs.tobesoft.com/advanced_development_guide_nexacro_17_ko)
