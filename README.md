# Nexacro Skill

Nexacro Platform 17 개발·분석·오류 진단을 위한 Codex 및 Claude Code 공용 스킬입니다.

## 신입사원 학습 가이드

저장소의 유튜브 기본 강의 6편을 바탕으로, 화면 만들기부터 데이터 바인딩·Grid·서버 연동까지 실습하는 [넥사크로 스튜디오 자습 가이드](youtube/guide/README.md)입니다. 각 장에 핵심 개념, 실습 순서, 완료 체크와 영상 구간 링크를 정리했습니다.

## Codex

사용자 전역에 설치:

```bash
mkdir -p ~/.agents/skills
cp -R ./nexacro ~/.agents/skills/nexacro
```

특정 프로젝트에만 설치:

```bash
mkdir -p /path/to/project/.agents/skills
cp -R ./nexacro /path/to/project/.agents/skills/nexacro
```

Codex에서 `$nexacro`로 호출합니다. 설치 후 보이지 않으면 Codex를 다시 시작하세요.

## Claude Code

사용자 전역에 설치:

```bash
mkdir -p ~/.claude/skills
cp -R ./nexacro ~/.claude/skills/nexacro
```

특정 프로젝트에만 설치:

```bash
mkdir -p /path/to/project/.claude/skills
cp -R ./nexacro /path/to/project/.claude/skills/nexacro
```

Claude Code에서 `/nexacro`로 호출합니다.

## 참고

- [Codex 스킬 공식 문서](https://learn.chatgpt.com/docs/build-skills)
- [Claude Code 디렉터리 공식 문서](https://code.claude.com/docs/en/claude-directory)
