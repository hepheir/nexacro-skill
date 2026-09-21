# 빌드·실행·배포 경로를 끝까지 추적하기

[매뉴얼 목차](../README.md) · 관련 문서: [빌드 경로 설정](../basics/project/build-path.md)

화면이 반영되지 않으면 원본, Generate 결과물, 서버 게시 파일과 실행 URL을 차례로 대조합니다.

## 프로젝트에서 어떤 파일을 보나요?

| 파일·설정 | 확인할 내용 |
| --- | --- |
| `.xprj` | Studio에서 여는 프로젝트 파일 |
| `.xadl` | Application과 Frame 구성, 시작 화면 |
| `.xfdl` | 화면 하나의 원본. 배치·Script·이벤트·바인딩 포함 |
| `.xjs` | 여러 화면에서 사용하는 Script |
| TypeDefinition / Services | Form·Script·서버 URL 등에 쓰는 서비스 접두어 |
| Environment / AppVariables | 실행 환경 설정, 전역 변수·Dataset |
| Theme / XCSS | 공통 디자인과 컴포넌트 스타일 |

실제 파일명과 설정 배치는 프로젝트에 따라 다릅니다. 수정 대상은 원본이며, Generate된 `.xfdl.js`를 직접 고치면 다음 생성 때 덮어써집니다.

## 회사 프로젝트를 처음 받았어요

`File > Open > Project`로 `.xprj`를 엽니다. 먼저 라이브러리 버전, 아래의 Generate Path, 개발 서버 URL을 확인한 후 `Generate > Application`을 실행합니다. 외부에서 복사하거나 소스 관리로 받은 파일은 **열기만 했다고 전체 생성되지 않습니다.**

| 상황 | 사용할 기능 |
| --- | --- |
| 원본만 받았거나 전체 산출물이 없음 | `Generate > Application` |
| 저장할 때 수정 내용을 생성하고 싶음 | Auto Generate 활성화 |
| 전체를 다시 생성해야 함 | `Generate > Regenerate > Application` |
| 작업 중인 화면만 확인 | QuickView |
| 로그인·메뉴·공통 초기화까지 확인 | Application 실행 |

`Skip`은 생성할 필요가 없는 항목을 건너뛰었다는 뜻입니다. 실패 여부는 Output의 오류 메시지로 판단합니다. QuickView는 전체 애플리케이션의 로그인·전역 초기화 흐름을 그대로 재현하지 않을 수 있습니다.

## 빌드 경로는 어디서 지정하나요?

**메뉴: `Tools > Options > Project > Generate > General > Generate Path`**

1. 프로젝트를 연 상태에서 위 옵션을 엽니다.
2. Generate Path에 생성 파일을 둘 폴더를 입력하거나 선택합니다.
3. 적용 후 `Generate > Application`을 실행합니다.
4. 해당 폴더에 화면의 `.xfdl.js` 등 산출물이 생겼는지, Output에 오류가 없는지 확인합니다.

경로에는 `%(ProjectDir)` 같은 Studio 매크로도 사용할 수 있습니다. 팀에서 지정한 경로가 있다면 그 규칙을 따르세요. **Generate Path를 Studio의 Deploy Path와 같게 두거나 그 하위에 두지 않습니다.** 공식 문서에서 이 구성을 피하도록 안내합니다. [공식 옵션 설명](https://docs.tobesoft.com/development_tools_guide_nexacro_17_ko/1214c35fbf6a6248)

다음은 경로를 구분하기 위한 예시입니다. 회사의 실제 디렉터리 구조를 뜻하지 않습니다.

| 용도 | 예시 | 의미 |
| --- | --- | --- |
| 원본 | `D:\work\employee-ui-src` | `.xprj`, `.xfdl`, `.xjs`를 수정하는 곳 |
| Generate Path | `D:\work\employee-ui-gen` | 실행용 파일이 생성되는 곳 |
| Deploy Path | `D:\work\employee-ui-deploy` | Studio의 배포 작업 산출물 위치 |
| WAS에 게시된 UI 폴더 | `D:\servers\tomcat\webapps\erp\ui` | 서버가 실제 제공하는 파일의 위치 예시 |
| 화면 실행 URL | `http://localhost:8080/erp/ui/<시작문서>` | 사용자가 접속하는 주소 |
| API 기본 URL | `http://localhost:8080/erp/` | 조회·저장 요청을 받는 주소 |

`<시작문서>`는 프로젝트에서 생성·배포하는 실제 시작 문서명으로 바꿉니다. UI가 별도 웹서버에 있을 수도 있습니다.

```text
원본 폴더 → Generate 폴더 → 회사의 복사·패키징·배포 절차 → 웹서버/WAS 게시 폴더
                                                            ↑
                                                     실행 URL이 읽는 곳
```

**Generate Path를 바꾸는 것만으로 WAS 설정이나 배포 위치가 바뀌지는 않습니다.** 회사 빌드 스크립트가 자동 복사하는지, IDE가 게시하는지, 개발 웹서버가 Generate 폴더를 직접 제공하는지 확인해야 합니다. 운영 폴더를 로컬 Generate 대상으로 지정하지 마세요.

## 저장하면 자동으로 빌드되나요?

**메뉴: `Tools > Options > Environment > Generate > Auto Generate`**

`Auto generate when file saved`를 켜면 파일 저장 시 Generate가 실행됩니다. 꺼져 있으면 수동 Generate가 필요합니다. 이 설정과 산출물 위치를 지정하는 **Project > Generate**는 역할이 다릅니다. [공식 Auto Generate 설명](https://docs.tobesoft.com/development_tools_guide_nexacro_17_ko/1214c35fbf6a6248)

강의에서 저장 후 바로 실행된 것은 자동 생성이 동작하는 환경이었기 때문입니다. 자동 생성이 켜져 있어도 **Java 컴파일, WAR 생성, WAS 재시작, 운영 배포까지 수행되는 것은 아닙니다.** 별도 자동화가 연결되어 있다면 그 절차를 확인하세요.

## Generate했는데 실행 화면은 그대로예요

확인 순서는 **원본 저장 → Output → 생성 파일 → 실행 URL의 파일 → Reload/캐시**입니다.

- 생성 폴더의 파일은 바뀌었는데 화면이 그대로면, 실행 URL이 다른 폴더를 보고 있는지 확인합니다.
- Studio의 `Project > Launch`와 실행 시 Run Configuration에서 어떤 서버·환경을 사용하는지 확인합니다.
- 넥사크로 라이브러리를 찾지 못하면 `Project > General > Base Library Path`와 프로젝트 버전을 확인합니다.
- Java 코드를 바꾼 경우에는 회사의 서버 빌드·게시 절차가 별도로 필요합니다.

## 강의에서 확인

[2강 37:08 · 저장 시 생성](https://www.youtube.com/watch?v=3JC5iB-qfv0&t=2228s) · [2강 37:55 · 생성 경로](https://www.youtube.com/watch?v=3JC5iB-qfv0&t=2275s) · [3강 7:30 · 받은 프로젝트 Generate](https://www.youtube.com/watch?v=c_Bfona4Hns&t=450s)

강의 자료: [1강](<../../youtube/기본01. 넥사크로플랫폼 개요.md>), [2강](<../../youtube/기본02. 개발환경 설정과 Hello.md>), [3강](<../../youtube/기본03. 넥사크로 컴포넌트.md>)
