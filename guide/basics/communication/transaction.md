# 서버로 조회 요청은 어떻게 보내나요?

[매뉴얼 목차](../../README.md)

**`transaction()`에 URL과 주고받을 데이터, 완료 함수를 지정합니다.** 회사에 공통 통신 함수가 있다면 업무 화면에서는 그 함수를 우선 사용합니다.

## 기본 API의 구성

아래는 `SvcURL`, `ds_search`, `ds_emp`가 준비된 경우의 설명용 예시입니다.

```javascript
this.transaction(
    "searchEmp",
    "SvcURL::employee/search.do",
    "in_search=ds_search:A",
    "ds_emp=out_emp",
    "",
    "fnCallback"
);
```

| 순서 | 의미 |
| --- | --- |
| service ID | 완료 후 어떤 요청인지 구분 |
| URL | 호출할 서버 주소 |
| input | 서버에 보낼 Dataset |
| output | 화면에서 응답을 받을 Dataset |
| arguments | 추가 전달값. 없으면 빈 문자열 |
| callback | 완료 후 실행할 함수명 |

## 매핑 방향을 읽는 방법

`in_search=ds_search:A`는 화면의 ds_search를 서버에 in_search라는 이름으로 보냅니다. `ds_emp=out_emp`는 서버의 out_emp를 화면의 ds_emp로 받습니다. **왼쪽이 받는 쪽, 오른쪽이 보내는 쪽**입니다.

예시의 `:A`는 조회 조건을 변경 여부와 관계없이 전체 전송하기 위한 설정입니다. 저장할 변경 데이터는 서버 계약에 따라 `:U` 등을 사용합니다.

여러 매핑은 공백으로 구분합니다. 별도 인자에 공백이 포함된 값은 `nexacro.wrapQuote()` 등 회사의 전달 규약을 따릅니다. 응답 결과는 다음 문서의 callback에서 처리합니다.

---

관련 문서: [callback](callbacks.md) · [공통 통신 함수](../common/transaction-wrapper.md)

강의: [6강 3:48 · transaction](https://www.youtube.com/watch?v=Q9NnAdtH_kU&t=228s)
