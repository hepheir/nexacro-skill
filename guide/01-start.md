# 1. 개발환경과 프로젝트

[학습 목차](README.md) · 다음: [첫 화면과 이벤트](02-hello.md)

> **이번 목표:** 프로젝트를 열고, 원본 파일과 실행용 파일을 구분한다.

## 핵심만 보기

| 용어 | 지금 기억할 내용 |
| --- | --- |
| Nexacro Studio | 화면을 만들고 실행·디버깅하는 개발 도구 |
| Project | 화면과 설정을 묶은 작업 단위. `.xprj`로 연다 |
| Form | 화면 하나. 원본 파일 확장자는 `.xfdl` |
| Generate | 원본을 실행용 JavaScript 등으로 변환하는 과정 |
| QuickView | 작업 중인 Form을 실행해서 확인하는 기능 |

```text
원본 Form(.xfdl) → Generate → 실행용 파일(.xfdl.js 등) + 넥사크로 라이브러리 → 실행
```

수정할 파일은 **원본 `.xfdl`**입니다. 생성된 `.xfdl.js`를 고치면 다시 Generate할 때 덮어써질 수 있습니다.

## 따라 하기

**샘플이 있다면**

1. 교육자료의 `EduProject17.1` 폴더 전체를 실습 위치에 복사합니다.
2. Studio에서 `File > Open > Project`로 복사본의 `.xprj`를 엽니다.
3. `Generate > Application`을 실행하고 Output에서 오류 여부를 확인합니다.
4. 프로젝트 실행 기능으로 Run Configuration을 열어, 준비된 실행 환경에서 실행합니다.

**샘플이 없다면**

1. `File > New > Project`에서 별도 연습 프로젝트를 생성합니다. 마법사 설정은 아래 1강의 34:00 구간을 참고하세요.
2. `TypeDefinition > Services`에서 Form을 저장할 `form` 서비스가 있는지 확인합니다. 없다면 `Hello`라는 이름으로 추가합니다.
3. 다음 장에서 이 서비스 아래에 Form을 만듭니다. 이후 사원관리 화면도 새 Form으로 직접 구성할 수 있습니다.

## 완료 체크

- [ ] 프로젝트 탐색기에서 화면 파일을 찾았다.
- [ ] 원본 위치와 Generate 경로를 구분할 수 있다.
- [ ] 샘플 실행에 성공했거나, 새 프로젝트에 Form을 만들 준비가 됐다.

**막혔다면:** 복사한 프로젝트가 실행되지 않으면 먼저 Generate 결과를 확인하세요. 전체 재생성이 필요할 때는 `Generate > Regenerate > Application`을 사용합니다. `Skip`은 같은 산출물의 재생성을 생략했다는 뜻이며, 그 자체가 오류는 아닙니다.

## 필요한 영상만 보기

- [1강 22:30 · Studio 구성](https://www.youtube.com/watch?v=Mu-HkDkjEZI&t=1350s)
- [1강 34:00 · 프로젝트 만들기](https://www.youtube.com/watch?v=Mu-HkDkjEZI&t=2040s)
- [3강 4:11 · 샘플 프로젝트 열기](https://www.youtube.com/watch?v=c_Bfona4Hns&t=251s)
- [3강 7:30 · Generate](https://www.youtube.com/watch?v=c_Bfona4Hns&t=450s)

원문: [1강](<../기본01. 넥사크로플랫폼 개요.md>), [3강](<../기본03. 넥사크로 컴포넌트.md>)
