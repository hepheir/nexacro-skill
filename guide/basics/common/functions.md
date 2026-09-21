# 공통 함수는 어디에 있고 어떻게 사용하나요?

[매뉴얼 목차](../../README.md)

**반복되는 기능을 공통 Script에 정의하고 화면에서 불러오는 방식이 대표적입니다.** 회사 프로젝트에서는 이미 사용하는 함수와 호출 예제를 먼저 찾습니다.

## include로 불러오는 구조

```javascript
include "Lib::Common.xjs";
```

`Lib`는 Services에 등록된 Script 경로 접두어이고 `Common.xjs`는 파일명입니다. 실제 이름은 프로젝트마다 다릅니다.

공통 파일이 Form 범위에 `gfnCheckRequired`라는 함수를 제공한다면 화면에서는 `this.gfnCheckRequired(...)`처럼 호출할 수 있습니다. 인자·반환값은 그 함수의 정의를 따릅니다. 함수명의 `gfn`은 명명 규칙이며 기본 API를 뜻하지 않습니다.

## 정의를 읽을 때 볼 것

Studio의 Open Include File로 파일을 열거나 함수명을 검색합니다.

| 확인 항목 | 알아야 하는 이유 |
| --- | --- |
| 입력 인자·반환값 | 호출할 때 무엇을 넘기고 받을지 |
| 실행 범위 | Form 함수인지 Application 함수인지 |
| 전역값·다른 공통 함수 | 어떤 초기화가 먼저 필요한지 |
| 기존 호출 화면 | 실제 사용법과 예외 처리 방식 |

Application이나 공통 초기화 Script가 함수를 제공하는 구조도 있습니다. include가 보이지 않아도 함수의 정의와 초기화 흐름을 먼저 확인하세요.

## 공통 함수를 고칠 때

여러 화면이 함께 사용하는 코드이므로 인자·반환값을 바꾸면 다른 호출부도 영향을 받습니다. 한 화면의 임시 요구인지 여러 화면의 공통 규칙인지 구분하고, 전체 사용처를 검색한 뒤 변경합니다.

---

관련 문서: [공통 화면](ui-reuse.md) · [공통 통신 함수](transaction-wrapper.md)

관련 문서: [공통 코드의 의존성](../../details/events-and-common.md) · 강의: [3강 21:05](https://www.youtube.com/watch?v=c_Bfona4Hns&t=1265s)
