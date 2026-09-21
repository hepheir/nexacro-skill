# Transaction과 서버 연동

## 표준 호출 형태

Nexacro 17의 Form `transaction()` 사용례는 일반적으로 다음 정보를 전달한다.

```javascript
this.transaction(
    "svcSearchEmployee",
    "<SERVICE_URL>",
    "",
    "dsEmployee=output1",
    "department=" + nexacro.wrapQuote(department),
    "fnTransactionCallback"
);
```

위 ID, URL, 서버 Dataset 이름과 argument 이름은 예시다. 실제 프로젝트의 wrapper가 있으면 wrapper의 signature와 공통 callback 흐름을 우선한다.

## 매핑 점검

- 첫 인자는 요청을 식별하는 service ID이며 callback 분기와 일치해야 한다.
- input Dataset mapping은 `serverDataset=localDataset[:U|:A|:N]` 방향이다. `:U`는 갱신 데이터, `:A`는 전체 데이터, `:N`은 삭제 행을 제외한 데이터를 보내는 옵션이며 서버 계약에 맞춰 선택한다.
- output Dataset mapping은 반대 방향인 `localDataset=serverDataset`이다. 양쪽 이름이 같으면 방향 오류가 가려지므로 역할을 기준으로 검증한다.
- argument 문자열은 공백 구분, quoting, null 처리 규약을 기존 코드 및 서버 계약과 맞춘다.
- URL은 literal인지 service prefix 기반인지 확인한다. Environment의 service 설정을 먼저 찾는다.
- callback 함수가 문자열로 전달되는 프로젝트인지 wrapper가 함수 참조를 받는지 임의로 바꾸지 않는다.

## Callback

대표적인 callback 모양:

```javascript
this.fnTransactionCallback = function (serviceId, errorCode, errorMsg)
{
    if (errorCode < 0) {
        trace(serviceId + ": " + errorMsg);
        return;
    }

    if (serviceId == "svcSearchEmployee") {
        // 조회 후 처리
    }
};
```

실제 callback signature와 성공/실패 기준은 프로젝트 wrapper 또는 공식 문서에서 확인한다. 공통 callback이 loading indicator, session 만료, 메시지 변환을 처리한다면 화면 callback에서 중복 처리하지 않는다.

## 저장 요청

- 신규·수정·삭제 행을 서버가 어떤 row type 규약으로 해석하는지 확인한다.
- 성공 후 재조회 또는 변경 상태 확정이 필요한지는 기존 화면과 서버 응답 규약을 따른다. 표준 transaction이 성공했다는 이유만으로 `applyChange()`를 무조건 추가하지 않는다.
- 중복 클릭 방지, 진행 상태, 실패 시 변경 데이터 보존 정책을 확인한다.
- callback에서 service ID별 후처리를 분리하고, 실패 경로가 성공 메시지나 Dataset 초기화를 실행하지 않게 한다.

## 진단 순서

1. service ID와 callback 분기
2. resolved URL 및 service prefix
3. input/output Dataset mapping 방향과 이름
4. argument quoting과 인코딩
5. 서버 응답의 error code/message 및 Dataset 이름
6. callback 연결과 공통 wrapper의 선·후처리

## 비동기 실행

`transaction()`의 `bAsync` 기본값은 `true`다. 특별한 근거가 없으면 callback으로 후속 처리를 이어간다. WRE에서 `bAsync=false` 동기 호출은 브라우저별 제약과 경고, focus 문제를 일으킬 수 있으므로 피하고, 불가피한 경우 대상 브라우저와 Nexacro 17 세부 빌드에서 검증한다.

## 공식 자료

- [Nexacro Platform 17 전체 매뉴얼](https://docs.tobesoft.com/nexacro_17_ko)
- [서버 설정/개발 가이드](https://docs.tobesoft.com/server_setup_guide_nexacro_17_ko)
- 공식 매뉴얼에서 `transaction`, `Dataset SSV Format`, `Dataset XML Format`을 검색한다.
