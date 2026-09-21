# Nexacro Skill

Nexacro Platform 17 개발·분석·오류 진단을 위한 Codex 및 Claude Code 공용 스킬입니다.

## 신입사원 입문 매뉴얼

[넥사크로 스튜디오 업무 입문 매뉴얼](guide/README.md)은 프로젝트 설정과 Generate, 화면·이벤트·Dataset·공통 함수, Spring Legacy 연동을 설명합니다. 기존 프로젝트를 처음 확인한다면 [프로젝트 열기](guide/basics/project/project-start.md)부터 시작하세요.

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
