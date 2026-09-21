# this·obj는 무엇이고 컴포넌트는 어떻게 찾나요?

[매뉴얼 목차](../../README.md)

**Form에 연결된 이벤트 함수에서 `this`는 현재 Form, `obj`는 이벤트를 발생시킨 객체를 가리킵니다.** 다른 범위에서 호출하는 공통 함수는 그 함수의 실행 범위를 따로 확인합니다.

## 속성 읽기와 변경

```javascript
this.btnSearch_onclick = function (obj, e)
{
    obj.set_text("조회");
    trace(obj.text);
};
```

`set_text()`는 속성 변경, `obj.text`는 값 읽기입니다. 속성을 바꾸는 코드를 단순 대입으로 대체하지 않습니다. `e`에는 클릭 위치 등 이벤트 종류에 따른 정보가 들어옵니다.

## Div 안의 객체 경로

| 객체 위치 | Form Script에서 접근 |
| --- | --- |
| Form에 직접 배치한 Button | this.btnSearch |
| Div 안에 배치한 Edit | this.divDetail.form.edtName |

화면에서 Div 위에 겹쳐 보이는 것만으로 부모가 Div라고 판단할 수는 없습니다. 실제 객체 트리를 확인하세요. 다른 Form을 URL로 불러오는 경우에는 그 Form의 로딩이 완료된 뒤 내부 객체에 접근해야 합니다.

## 변수의 범위

```javascript
this.searchCount = 0;        // Form이 보관할 상태
this.fnSearch = function ()
{
    var keyword = "";       // 이 함수 안에서 사용할 값
};
```

ID를 바꾸면 객체 경로를 쓰는 Script·바인딩을 함께 확인합니다. `fn`, `gfn`, `btn` 같은 접두어는 회사의 명명 규칙이며 기능을 자동으로 부여하는 예약어는 아닙니다.

---

관련 문서: [공통 함수](../common/functions.md) · [공통 화면](../common/ui-reuse.md)

강의: [2강 21:31 · 속성](https://www.youtube.com/watch?v=3JC5iB-qfv0&t=1291s)
