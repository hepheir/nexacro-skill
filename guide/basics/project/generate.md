# 저장하면 자동으로 빌드되나요?

[매뉴얼 목차](../../README.md)

**Auto Generate가 켜져 있으면 저장할 때 실행용 파일을 생성합니다.** 프로젝트를 열기만 한 경우와 파일을 저장한 경우는 구분해야 합니다.

## 자동 생성 옵션

`Tools > Options > Environment > Generate > Auto Generate`에서 **Auto generate when file saved**를 확인합니다. 켜져 있으면 저장 시 생성하며, 꺼져 있으면 수동 Generate가 필요합니다.

산출물 위치를 지정하는 `Project > Generate`와는 다른 설정입니다. 자동 생성은 “언제 만들지”, Generate Path는 “어디에 만들지”를 정합니다. [공식 옵션 설명](https://docs.tobesoft.com/development_tools_guide_nexacro_17_ko/1214c35fbf6a6248)

## 수동 Generate는 언제 하나요?

| 상황 | 작업 |
| --- | --- |
| 회사 프로젝트의 원본만 받음 | `Generate > Application` |
| 자동 생성이 꺼진 상태에서 수정함 | 필요한 범위를 수동 Generate |
| 전체 산출물을 다시 만들 필요가 있음 | `Generate > Regenerate > Application` |

외부에서 받은 파일은 아직 저장·생성하지 않았을 수 있습니다. 처음에는 전체 Generate 결과를 확인하세요. Output의 `Skip`은 불필요한 생성을 건너뛰었다는 뜻이며 그 자체가 오류는 아닙니다.

## 빌드 완료와 배포 완료는 다릅니다

Generate가 성공해도 Java 컴파일, WAR 생성, WAS 게시까지 자동으로 완료되는 것은 아닙니다. 회사의 별도 자동화가 있는지 확인합니다. 수정한 화면이 그대로라면 생성 파일이 바뀌었는지, 실행 URL이 그 파일을 읽는지를 대조하세요.

---

관련 문서: [빌드 경로 지정](build-path.md) · [생성부터 배포까지](../../details/build-and-deploy.md)

강의: [2강 37:08 · 저장 시 생성](https://www.youtube.com/watch?v=3JC5iB-qfv0&t=2228s)
