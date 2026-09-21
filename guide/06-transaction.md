# 6. 행 추가·삭제에서 서버 조회·저장까지

[학습 목차](README.md) · 이전: [Grid](05-grid.md) · 다음: [최종 미션](07-mission.md)

> **이번 목표:** 화면의 데이터 변경과 서버 저장을 구분하고, 통신 결과를 callback에서 확인한다.

## 먼저, 서버 없이 추가·삭제

추가 Button의 `onclick`을 생성하고 **함수 본문**에 넣습니다.

```javascript
var row = this.ds_emp.addRow();
this.ds_emp.setColumn(row, "DEPT_CD", "D01");
this.ds_emp.setColumn(row, "SALARY", 0);
```

삭제 Button의 `onclick` 본문에는 다음을 넣습니다.

```javascript
var row = this.ds_emp.rowposition;
if (row < 0) {
    this.alert("삭제할 사원을 선택하세요.");
    return;
}
this.ds_emp.deleteRow(row);
```

실행해서 행을 추가하고 상세 입력창으로 이름·사번을 입력해 보세요. 행 삭제 후 목록과 건수도 확인합니다. **여기까지는 화면의 Dataset만 바뀝니다. DB에 저장한 것은 아닙니다.**

## 서버 연동 전 확인

아래 코드는 강의와 같은 통신 계약을 가정한 학습 예제입니다. 다음 준비가 끝난 경우에만 연결하세요.

- [ ] 개발용 서버와 조회·저장 API가 준비되어 있다.
- [ ] Services에 `SvcURL`이 등록되어 있고 개발 서버의 기본 URL을 가리킨다.
- [ ] 조회 API는 `out_emp`를 반환하고 저장 API는 `in_emp`를 받는다.
- [ ] 서버 컬럼 정의가 `ds_emp`와 맞는다. 4장의 최소 컬럼만으로 저장 가능한지도 확인했다.

서버가 없다면 아래 매핑과 callback 흐름을 읽고 최종 미션의 로컬 과정까지 진행하세요. 원문 자막만으로는 서버의 전체 주소·구현을 복원할 수 없습니다. 영상의 옛 공개 서버가 현재도 동작한다고 가정하지 않습니다.

## 핵심만 보기

```text
조회: 서버 out_emp ──→ 화면 ds_emp ──→ Grid·상세
저장: 화면 ds_emp  ──→ 서버 in_emp  ──→ DB 처리
```

| transaction 인자 | 조회 예시 | 의미 |
| --- | --- | --- |
| 1. service ID | `searchEmp` | 어떤 요청의 결과인지 구분 |
| 2. URL | `SvcURL::select_emp.jsp` | 호출할 서비스 |
| 3. input Dataset | 빈 문자열 | 서버에 보내는 Dataset |
| 4. output Dataset | `ds_emp=out_emp` | 화면이 받을 Dataset |
| 5. arguments | 빈 문자열 | 추가 전달값 |
| 6. callback | `fnCallback` | 통신이 끝나면 호출할 함수 |

매핑의 왼쪽은 **받는 쪽**, 오른쪽은 **보내는 쪽**입니다. 저장은 `in_emp=ds_emp:U`, 조회는 `ds_emp=out_emp`가 됩니다. `:U`는 변경 데이터 전송 옵션이며, 전체 전송 `:A`가 필요한지는 서버 계약에 따릅니다.

## 따라 하기: 조회 → 수정 → 저장 → 재조회

조회 Button의 `onclick` 본문:

```javascript
this.transaction(
    "searchEmp", "SvcURL::select_emp.jsp",
    "", "ds_emp=out_emp", "", "fnCallback"
);
```

저장 Button의 `onclick` 본문:

```javascript
this.transaction(
    "saveEmp", "SvcURL::save_emp.jsp",
    "in_emp=ds_emp:U", "", "", "fnCallback"
);
```

다음은 **다른 이벤트 함수 밖, Form Script에** 추가합니다.

```javascript
this.fnCallback = function (serviceId, errorCode, errorMsg)
{
    if (errorCode < 0) {
        trace(serviceId + ": " + errorMsg);
        this.alert("처리에 실패했습니다. 로그를 확인하세요.");
        return;
    }
    if (serviceId == "searchEmp") {
        trace("조회 건수: " + this.ds_emp.getRowCount());
    } else if (serviceId == "saveEmp") {
        this.alert("저장 요청이 성공했습니다. 재조회로 결과를 확인하세요.");
    }
};
```

서버의 성공·실패 코드 규약이 다르면 callback도 맞춰야 합니다. 통신은 비동기로 진행되므로 **조회 직후 결과를 사용하는 코드는 callback의 조회 성공 분기에** 작성합니다.

## 완료 체크

- [ ] 행을 추가·삭제하면 Grid와 건수가 바뀐다.
- [ ] 서버 준비 시: 조회 → 이름 수정 → 저장 → 재조회 후에도 변경한 이름이 유지된다.
- [ ] 통신 실패 시 성공 메시지가 나오지 않고 오류 로그가 남는다.

**막혔다면:** `SvcURL` 주소 → 요청·응답 Dataset 이름 → 컬럼명 → callback 연결 순서로 확인하세요. 새 Form에는 부서 코드 조회를 구현하지 않았으므로 서버의 부서 코드가 `ds_dept`에 없으면 이름이 표시되지 않을 수 있습니다.

## 더 해보기: 부서 목록도 서버에서

강의는 Form `onload`에서 코드 데이터를 조회합니다. `ds_dept=out_dept ds_pos=out_pos`처럼 여러 output 매핑은 공백으로 구분합니다. 실제 서버 계약과 수신 Dataset을 먼저 준비하세요. 서버 연동이 확인된 뒤 연습용 Rows를 제거하고 다시 실행해 봅니다. Columns는 유지합니다.

## 필요한 영상만 보기

- [6강 3:48 · transaction](https://www.youtube.com/watch?v=Q9NnAdtH_kU&t=228s)
- [6강 13:00 · callback](https://www.youtube.com/watch?v=Q9NnAdtH_kU&t=780s)
- [6강 21:10 · 행 추가·삭제](https://www.youtube.com/watch?v=Q9NnAdtH_kU&t=1270s)
- [6강 25:31 · 저장](https://www.youtube.com/watch?v=Q9NnAdtH_kU&t=1531s)
- [6강 32:38 · 코드 데이터 조회](https://www.youtube.com/watch?v=Q9NnAdtH_kU&t=1958s)

원문: [6강](<../기본06. 화면실습_데이터통신.md>)
