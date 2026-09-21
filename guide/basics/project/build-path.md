# 빌드된 파일은 어디에 저장되나요?

[매뉴얼 목차](../../README.md)

**Generate Path가 실행용 산출물의 저장 위치입니다.** 회사 프로젝트를 처음 열 때 반드시 확인할 설정입니다.

## 설정 위치와 확인 방법

`Tools > Options > Project > Generate > General > Generate Path`

1. 프로젝트를 연 상태에서 위 설정을 엽니다.
2. 회사 규칙에 맞는 폴더를 지정합니다. 예: `D:\work\employee-ui-gen`.
3. 적용 후 `Generate > Application`을 실행합니다.
4. 지정 폴더에 `.xfdl.js` 등 산출물이 생성되는지, Output에 오류가 없는지 확인합니다.

`%(ProjectDir)` 같은 Studio 매크로도 사용할 수 있습니다. Generate Path를 **Studio의 Deploy Path와 같게 두거나 그 하위에 두지 않습니다.** [공식 경로 설정 설명](https://docs.tobesoft.com/development_tools_guide_nexacro_17_ko/1214c35fbf6a6248)

## 서로 다른 세 위치

| 위치 | 무엇을 하나요? |
| --- | --- |
| 원본 폴더 | 개발자가 XFDL·XJS를 수정 |
| Generate 폴더 | Studio가 실행용 파일을 생성 |
| 웹서버/WAS 게시 폴더 | 실행 URL을 통해 사용자에게 파일 제공 |

개발 웹서버가 Generate 폴더를 직접 제공할 수도 있고, 별도 복사·게시 절차가 있을 수도 있습니다. 경로만 바꿔서는 WAS의 설정이나 게시 위치가 바뀌지 않습니다.

## 경로를 바꿨는데 화면은 그대로라면

먼저 생성 파일의 변경을 확인하고, 실행 URL이 어느 폴더의 파일을 제공하는지 확인합니다. **원본 저장 → Generate 결과 → 서버 게시 파일 → Reload/캐시** 순서로 보면 됩니다. 실제 실행 서버는 Launch와 Run Configuration에서도 확인할 수 있습니다.

---

관련 문서: [자동·수동 Generate](generate.md) · [경로 예시와 실행 반영 확인](../../details/build-and-deploy.md)

강의: [2강 37:55 · Generate 경로](https://www.youtube.com/watch?v=3JC5iB-qfv0&t=2275s)
