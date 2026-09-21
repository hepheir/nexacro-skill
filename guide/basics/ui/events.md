# 이벤트 함수는 어떻게 연결하나요?

[매뉴얼 목차](../../README.md)

**함수를 작성한 뒤 컴포넌트의 이벤트에 연결해야 실행됩니다.** `btnSearch_onclick`처럼 이름만 정했다고 자동 연결되지는 않습니다.

## Studio에서 등록하기

Design에서 컴포넌트 선택 → Properties의 이벤트 목록 → `onclick` 등을 더블클릭합니다. Studio가 처리 함수를 만들고 연결합니다. 기존 함수를 쓰려면 이벤트 속성에서 해당 함수명을 지정합니다.

```javascript
this.btnSearch_onclick = function (obj, e)
{
    trace("조회 버튼 클릭");
};
```

위 함수는 Button의 `onclick` 속성에 `btnSearch_onclick`이 지정되어 있어야 호출됩니다.

## 어떤 이벤트를 선택하나요?

| 시점 | 대표 이벤트 |
| --- | --- |
| 화면 로드 완료 | Form의 onload |
| 버튼 클릭 | Button의 onclick |
| 입력값 변경 | Edit의 onchanged |
| Dataset 값 변경 | oncolumnchanged |
| Dataset 현재 행 변경 | onrowposchanged |

Form의 `onload`에서 서버 조회를 시작했다고 응답까지 도착한 것은 아닙니다. 조회 결과를 사용하는 코드는 callback에서 처리합니다.

## 동적 연결도 가능한가요?

객체가 생성된 뒤 `addEventHandler()`로 연결하고 `removeEventHandler()`로 해제할 수 있습니다. 디자인에서 연결한 이벤트를 Script로 다시 등록하거나 화면 초기화 때 반복 등록하면 한 번의 동작에 이벤트가 여러 번 실행될 수 있습니다.

값 변경 이벤트 안에서 다시 값을 변경하면 이벤트가 이어질 수 있으므로 처리 조건도 확인하세요.

---

관련 문서: [this·obj와 객체 경로](script-scope.md) · [동적 등록·해제](../../details/events-and-common.md)

강의: [2강 10:01 · 이벤트 연결](https://www.youtube.com/watch?v=3JC5iB-qfv0&t=601s)
