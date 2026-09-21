# 동적 이벤트와 공통 코드의 의존성

[매뉴얼 목차](../README.md) · 관련 문서: [이벤트 등록](../basics/ui/events.md) / [공통 함수](../basics/common/functions.md)

동적 이벤트와 공통 코드는 여러 초기화 시점과 화면에서 공유될 수 있으므로 등록 시점과 사용처를 함께 확인합니다.

## 이벤트 리스너는 어떻게 등록하나요?

**일반적인 방법:** Design에서 컴포넌트 선택 → Properties의 이벤트 목록 → `onclick` 같은 이벤트를 더블클릭합니다. Studio가 처리 함수를 만들고 연결합니다. 기존 함수를 연결할 때는 해당 이벤트 속성에서 함수명을 지정합니다.

```javascript
// Form Script: 함수 정의
this.btnSearch_onclick = function (obj, e)
{
    trace("조회 버튼 클릭");
};
```

이 함수가 호출되려면 Button의 `onclick` 속성에도 `btnSearch_onclick`이 연결되어 있어야 합니다. **함수 이름이 그럴듯하다는 이유만으로 자동 등록되지는 않습니다.**

**동적으로 연결할 때:** 객체가 만들어진 뒤 `addEventHandler()`를 사용합니다. 아래는 위의 Design 연결을 대신하는 방법입니다.

```javascript
// 객체 생성 후 초기화 지점에서 한 번 등록
this.btnSearch.addEventHandler("onclick", this.btnSearch_onclick, this);

// 연결을 해제해야 하는 시점에 실행
this.btnSearch.removeEventHandler("onclick", this.btnSearch_onclick, this);
```

위 두 줄은 등록·해제 위치를 보여주는 예시이며 함께 연속 실행하지 않습니다. 세 번째 인자 `this`는 처리 함수가 사용할 실행 범위입니다. 디자인 연결과 동적 등록을 겹치거나 재초기화 때 반복 등록하지 않도록 확인합니다. [공식 이벤트 등록 API](https://docs.tobesoft.com/advanced_development_guide_nexacro_17_en_kr/d036db0989d6184a)


## 무엇을 공통으로 만들 수 있나요?

| 반복되는 내용 | 구성 방법 | 예시 |
| --- | --- | --- |
| 색상·폰트·버튼 디자인 | Theme/XCSS + cssclass | 조회 버튼 스타일 |
| 자주 쓰는 계산·검증 | 공통 Script | 날짜 처리, 필수값 검사 |
| 세션·오류·로딩을 포함한 통신 | 공통 transaction 함수 | 화면의 조회·저장 요청 |
| 여러 컴포넌트를 묶은 영역 | 별도 Form을 Div 등에 포함 | 공통 검색 조건 |
| 독립된 선택 화면 | 팝업 Form과 공통 호출 함수 | 사원 선택 팝업 |
| 새 화면의 초기 구조 | Form Template, Code Snippet | 업무 화면 기본 틀 |
| 독립적인 재사용 컨트롤 | 프로젝트의 사용자 컴포넌트·모듈 | 사내 전용 입력 컴포넌트 |

템플릿·Snippet은 생성 시 내용을 복사하는 도구입니다. 원본 템플릿을 바꿨다고 이미 만든 모든 화면이 함께 수정되지는 않습니다. 재사용 Form·공통 함수는 공유 코드가 바뀌면 여러 사용처에 영향을 줍니다.

## 공통 함수는 어떻게 불러오나요?

대표적인 방식은 Form Script에서 공통 `.xjs`를 include하는 것입니다.

```javascript
include "Lib::Common.xjs";
```

`Lib`는 Services에 등록된 Script 경로 접두어, `Common.xjs`는 파일명입니다. 공통 파일에서 함수를 `this.gfnCheckRequired = function (...) { ... };`로 제공하는 구조라면 포함한 Form에서 `this.gfnCheckRequired(...)`처럼 호출합니다. 함수명과 인자는 프로젝트마다 다릅니다.

Studio에서 include 구문의 **Open Include File**로 정의 파일을 열어 다음을 확인하세요.

| 확인할 것 | 이유 |
| --- | --- |
| 입력 인자·반환값 | 화면에서 올바르게 호출하기 위해 |
| this가 가리키는 범위 | Form인지 Application인지 구분하기 위해 |
| 다른 include·전역값 의존성 | QuickView에서만 실패하는 원인을 찾기 위해 |
| 다른 호출 화면 | 실제 사용 규칙과 예외 처리를 보기 위해 |

어떤 프로젝트는 Application 함수나 공통 초기화 Script를 통해 함수를 제공합니다. 파일명이 보이지 않는다고 새 공통 함수를 만들기 전에 기존 함수의 정의를 검색하세요.

## 공통 통신 함수는 무엇을 하나요?

```text
화면의 조회 함수
  → 공통 통신 함수: URL·인자 구성, 로딩 표시, 기본 설정
    → Nexacro transaction()
      → 공통 callback: 오류·세션·로딩 종료 처리
        → 화면 callback: 조회 후 선택, 업무 메시지 등
```

이 흐름은 설계 예시이며 실제 호출 순서는 회사 구현을 확인합니다. 이름이 `gfnTransaction`이라고 해서 넥사크로 기본 API인 것은 아닙니다. 공통 함수가 Dataset 매핑을 자동 생성하는지, 서비스 ID를 변환하는지, 실패할 때도 화면 callback을 호출하는지 읽어야 합니다.

화면마다 통신 코드를 복사하기보다 **공통 함수의 호출 규약**을 사용합니다. 공통 처리가 이미 오류 메시지나 로딩 표시를 처리한다면 화면에서 중복 실행하지 않습니다.

## 공통 화면과 공통 컴포넌트는 어떻게 쓰나요?

공통 Form이 등록되어 있다면 Div의 `url`에 `Common::SearchArea.xfdl`처럼 연결할 수 있습니다. `Common`과 파일명은 예시입니다. 포함된 Form의 내부 객체 경로는 `divSearch.form...` 형태입니다.

부모 화면이 내부 Edit를 일일이 조작하기보다, 공통 화면이 제공하는 함수와 입력·결과 규약을 사용하는 편이 변경에 대응하기 쉽습니다. URL로 Form을 로드한 직후에는 초기화가 끝났다고 가정하지 말고 공통 화면의 준비 시점과 사용 예제를 확인하세요.

사용자 컴포넌트는 TypeDefinition의 객체·모듈 등록, 라이브러리 버전, 배포 파일이 함께 맞아야 합니다. 회사에서 제공한 모듈과 사용 가이드를 기준으로 설정합니다.

## 전역 Dataset은 언제 쓰나요?

여러 화면이 공유하는 로그인 정보·공통 코드 등에 사용할 수 있습니다. 한 화면에서만 편집할 업무 데이터는 Form Dataset으로 두는 편이 범위를 이해하기 쉽습니다. 전역 데이터는 누가 초기화·갱신하는지 확인하고, 화면의 임시 편집값으로 덮어쓰지 않도록 합니다.

강의: [3강 19:49 · 공통 함수와 Snippet](https://www.youtube.com/watch?v=c_Bfona4Hns&t=1189s), [21:05 · 공통 Script](https://www.youtube.com/watch?v=c_Bfona4Hns&t=1265s)

강의 자료: [3강](<../../youtube/기본03. 넥사크로 컴포넌트.md>) · 심화: [공통 규약 점검 참고](../../nexacro/references/common-patterns.md)
