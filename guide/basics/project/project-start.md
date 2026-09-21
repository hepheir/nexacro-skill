# 회사 프로젝트를 받으면 무엇부터 열어야 하나요?

[매뉴얼 목차](../../README.md)

**Studio에서 `.xprj`를 열고, 프로젝트 버전·생성 경로·실행 환경을 확인합니다.** 화면 파일 하나만 여는 것과 전체 프로젝트를 여는 것은 다릅니다.

## 처음 만나는 파일과 설정

| 파일·설정 | 역할 |
| --- | --- |
| `.xprj` | `File > Open > Project`로 여는 프로젝트 파일 |
| `.xadl` | Application과 Frame, 시작 화면 구성 |
| `.xfdl` | 화면 하나의 원본: 배치·Script·이벤트·바인딩 |
| `.xjs` | 공통 Script |
| Services | Form·Script·서버 URL의 경로 접두어 |
| Theme / XCSS | 공통 디자인과 스타일 |

Environment와 AppVariables에는 실행 환경·전역 변수·Dataset 등이 있습니다. 실제 파일명과 위치는 프로젝트에 따라 다릅니다.

## 열었다고 바로 실행되지는 않습니다

받은 폴더에 원본만 있다면 실행용 파일을 만들어야 합니다. **빌드 경로를 지정한 뒤 `Generate > Application`**을 실행하고, Output에서 오류 여부를 확인합니다. 설치된 Studio와 프로젝트 라이브러리 버전도 맞아야 합니다.

화면을 수정할 때는 `.xfdl`과 `.xjs` 원본을 편집합니다. 생성된 `.xfdl.js`를 직접 수정하면 다음 Generate 때 변경이 사라집니다.

## 화면 하나와 전체 앱 실행

QuickView는 작업 중인 Form을 확인하는 데 사용합니다. 회사의 로그인·메뉴·전역 초기화에 의존하는 화면은 Application 전체 실행으로 확인해야 할 수 있습니다. QuickView에서만 실패하면 화면 코드뿐 아니라 공통 초기화 여부도 살펴보세요.

---

관련 문서: [빌드 경로 지정](build-path.md) · [자동·수동 Generate](generate.md)

강의: [3강 4:11 · 프로젝트 열기](https://www.youtube.com/watch?v=c_Bfona4Hns&t=251s)
