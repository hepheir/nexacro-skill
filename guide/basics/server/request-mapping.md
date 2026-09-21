# 화면 URL과 서버 Dataset 이름은 어떻게 맞추나요?

[매뉴얼 목차](../../README.md)

**주소와 데이터 이름을 각각 맞춰야 합니다.** 서버에 도착하더라도 Dataset 이름이 다르면 기대한 데이터가 연결되지 않습니다.

## URL을 해석하는 예

| 항목 | 설명용 값 |
| --- | --- |
| Services 접두어 | SvcURL |
| 기본 URL | http://localhost:8080/erp/ |
| 요청 URL | SvcURL::employee/search.do |
| 최종 주소 | http://localhost:8080/erp/employee/search.do |
| Controller 매핑 | /employee/search.do |

이 예시의 Context Path는 `/erp`입니다. DispatcherServlet이 해당 요청을 받도록 설정되어 있어야 합니다. `.do`는 매핑 관례이며 필수 확장자는 아닙니다. 프록시가 있으면 외부 주소와 WAS 내부 경로가 다를 수도 있습니다.

## 같은 요청의 데이터 계약

```text
화면 ds_search → input: in_search=ds_search:A → 서버 in_search
서버 out_emp  → output: ds_emp=out_emp       → 화면 ds_emp
```

서버가 `out_emp`를 반환한다면 output 매핑도 그 이름을 사용합니다. 사번·이름 같은 컬럼의 이름·자료형도 맞춰야 합니다. 예시에서는 화면과 서버의 Dataset 이름을 일부러 다르게 두어 방향을 구분합니다.

## 연결에 실패하면

404라면 주소·Context Path·매핑부터 확인합니다. 서버 응답은 있는데 Grid가 비어 있다면 응답 Dataset 이름 → 컬럼명 → 화면 바인딩 순서로 확인합니다.

HTTP 200이어도 로그인 HTML이나 업무 오류 응답일 수 있습니다. Network의 실제 응답과 WAS 로그를 같은 요청 기준으로 대조하세요.

---

관련 문서: [transaction 인자](../communication/transaction.md) · [서버 설정·변환 모듈·오류 구분](../../details/spring-integration.md)
