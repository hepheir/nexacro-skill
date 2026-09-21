# 2. 첫 화면과 이벤트

[학습 목차](README.md) · 이전: [개발환경](01-start.md) · 다음: [컴포넌트](03-components.md)

> **이번 목표:** 버튼을 누르면 메시지와 로그가 나오고, 버튼 글자가 바뀐다.

## 핵심만 보기

| 코드 | 의미 |
| --- | --- |
| `this` | 이 예제의 이벤트 함수가 속한 Form |
| `obj` | 이 클릭 이벤트를 발생시킨 버튼 |
| `set_text("완료")` | 컴포넌트의 text 속성 변경 |
| `obj.text` | 현재 text 값 읽기 |
| `this.alert(...)` / `trace(...)` | 사용자 메시지 / 개발 확인용 로그 |

## 따라 하기

1. Form 서비스 아래에서 `File > New > Form`을 선택하고 `Hello`를 만듭니다. 처음에는 위치 단위를 px로 두세요.
2. Design에서 Button을 하나 배치하고 ID를 `btnHello`, text를 `Hello`로 지정합니다.
3. Properties의 이벤트 목록에서 `onclick`을 더블클릭해 함수를 만듭니다.
4. **Studio가 만든 함수의 본문 안에** 아래 세 줄을 넣습니다.

```javascript
this.alert("Hello, Nexacro!");
obj.set_text("클릭 완료");
trace(obj.text);
```

5. 저장하고 QuickView로 실행한 뒤 버튼을 누릅니다.

**예상 결과:** 메시지창이 뜨고 버튼 글자가 `클릭 완료`로 바뀝니다. NRE 실행에서는 Studio Output, 브라우저 실행에서는 개발자 도구 Console에서 로그를 확인합니다.

## 작은 도전

버튼을 누를 때마다 횟수를 표시해 보세요. Form Script의 함수 밖에 `this.clickCount = 0;`을 선언하고, 이벤트 본문을 아래처럼 바꿉니다.

```javascript
this.clickCount += 1;
obj.set_text("클릭 " + this.clickCount + "회");
```

## 완료 체크

- [ ] 세 번 누르면 `클릭 3회`가 표시된다.
- [ ] 속성 변경에는 `set_속성명()`, 읽기에는 속성명을 쓴다는 것을 설명할 수 있다.
- [ ] 오류가 발생했을 때 로그를 어디에서 볼지 안다.

**막혔다면:** 버튼의 `onclick` 속성에 함수가 연결됐는지 확인하세요. ID를 바꾼 뒤 실패한다면 Script에 예전 ID가 남았는지 찾으세요. 여기서 `obj`는 클릭한 버튼 자신을 가리키므로 버튼 ID를 바꿔도 본문을 그대로 쓸 수 있습니다.

## 필요한 영상만 보기

- [2강 1:50 · Form 만들기](https://www.youtube.com/watch?v=3JC5iB-qfv0&t=110s)
- [2강 10:01 · 이벤트 연결](https://www.youtube.com/watch?v=3JC5iB-qfv0&t=601s)
- [2강 19:26 · 실행과 로그](https://www.youtube.com/watch?v=3JC5iB-qfv0&t=1166s)
- [2강 21:31 · 속성 변경](https://www.youtube.com/watch?v=3JC5iB-qfv0&t=1291s)

원문: [2강](<../기본02. 개발환경 설정과 Hello.md>)
