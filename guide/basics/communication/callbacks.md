# 조회 결과는 언제 사용할 수 있나요?

[매뉴얼 목차](../../README.md)

**비동기 요청의 결과는 callback에서 사용합니다.** `transaction()` 다음 줄이 실행될 때는 서버 응답이 아직 오지 않았을 수 있습니다.

## 요청과 완료를 구분하기

```text
조회 버튼 → 서버 요청 시작 → 다른 코드 실행 가능 → 응답 도착 → callback
```

Form의 `onload`에서 조회를 시작해도 원리는 같습니다. 로딩 이벤트가 끝났다는 사실이 서버 데이터 도착을 뜻하지는 않습니다.

## callback 예시

Form Script에 함수를 정의하고 transaction의 callback 인자로 `"fnCallback"`을 전달합니다.

```javascript
this.fnCallback = function (serviceId, errorCode, errorMsg)
{
    if (errorCode < 0) {
        trace(serviceId + ": " + errorMsg);
        return;
    }
    if (serviceId == "searchEmp") {
        trace("조회 건수: " + this.ds_emp.getRowCount());
    }
};
```

예시는 음수를 실패로 판단합니다. 회사에서 정한 오류 코드나 공통 callback이 있다면 그 규약을 적용합니다. 실패를 처리한 뒤에는 성공 로직이 이어지지 않도록 합니다.

## 두 조회에 순서가 필요하다면

부서 목록을 받아야 사원 데이터를 올바르게 표시할 수 있는 화면이라면, 부서 조회가 성공한 뒤 사원 조회를 시작하도록 연결합니다. 요청 코드를 위아래로 나열하는 것만으로 완료 순서가 보장되지는 않습니다.

공통 통신 함수가 오류 메시지·로딩 종료를 이미 처리한다면 화면 callback에서는 업무 후처리에 집중합니다. 회사 공통 함수가 실패 시 화면 callback도 호출하는지는 구현을 확인하세요.

---

관련 문서: [저장과 DB 동기화](data-sync.md) · [공통 callback의 역할](../common/transaction-wrapper.md)

강의: [6강 13:00 · callback](https://www.youtube.com/watch?v=Q9NnAdtH_kU&t=780s)
