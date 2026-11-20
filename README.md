# AI 개발팀

업무 맥북과 개인 맥북에서 같은 개발 워크플로를 설치하는 Codex 플러그인입니다. 각 맥북에서 Codex로 현재 로컬 프로젝트를 열고 리드 → 구현 → 리뷰 순서로 작업합니다. 중앙 서버는 필요 없습니다.

## 비공개 Git 저장소 준비

Git 호스트에 비어 있는 **비공개 저장소**를 하나 만들고, 이 폴더에서 아래 명령을 실행합니다. `<비공개-Git-URL>`을 실제 Git URL로 바꿔 주세요. 숨김 폴더인 `.agents/`가 포함되어야 합니다.

```sh
git init -b main
git add .agents/plugins/marketplace.json plugins/ai-dev-team README.md .gitignore
git commit -m "feat: AI 개발팀 플러그인 추가"
git remote add origin '<비공개-Git-URL>'
git push -u origin main
```

업무 맥북에서는 회사가 허용하는 Git 호스트와 계정을 사용하세요. 회사에서 개인 비공개 저장소 접근을 제한하면, 회사가 허용하는 저장소에 플러그인 설정 파일만 두고 그 URL을 사용하세요. 코드와 작업 브랜치는 각 프로젝트 저장소에서, 토큰과 SSH 키는 기기별 인증 설정에서 관리합니다.

## 두 맥북에 설치

각 맥북에서 Codex CLI와 ChatGPT 데스크톱 앱의 Codex 모드를 준비합니다. 해당 기기의 Git 계정으로 비공개 저장소에 접근할 수 있어야 합니다. 터미널에서 확인한 실제 URL을 사용해 플러그인 소스를 등록하고 설치합니다.

```sh
git ls-remote '<비공개-Git-URL>' HEAD
codex plugin marketplace add '<비공개-Git-URL>' --ref main
codex plugin add ai-dev-team@ai-dev-team-private
codex plugin list --marketplace ai-dev-team-private
```

설치는 터미널의 `codex plugin add` 또는 데스크톱의 플러그인 목록 중 한 곳에서 하면 됩니다. 데스크톱으로 설치할 경우 소스 등록 후 앱을 재시작하고 **AI 개발팀 (개인)** 소스에서 **AI 개발팀**을 찾아 설치하세요. 소스가 표시되지 않으면 앱 버전과 업무 워크스페이스의 플러그인 정책을 확인하세요.

## 프로젝트에서 사용

Codex에서 작업할 로컬 Git 프로젝트를 열고 새 채팅의 스킬 선택 메뉴에서 `ai-dev-team:dev-team`을 선택합니다. 아래처럼 요청할 수도 있습니다.

> AI 개발팀으로 현재 저장소의 상품 상세 이미지 로딩을 개선해줘. 관련 테스트를 실행하고 변경분을 리뷰해줘.

각 프로젝트의 지침과 도구를 따릅니다. 읽기 전용 요청은 조사와 리뷰까지 진행하고, 구현 요청은 변경과 검증까지 진행합니다. 커밋·푸시·병합·배포는 각각 요청했을 때 진행합니다. 채팅, 작업 중인 코드, 미커밋 변경은 각 환경에서 관리됩니다.

## 업데이트

팀 규칙은 `plugins/ai-dev-team/skills/dev-team/SKILL.md`에서 바꿉니다. 변경 내용을 비공개 Git 저장소의 `main`에 반영한 뒤 각 맥북에서 다음을 실행합니다.

```sh
codex plugin marketplace upgrade ai-dev-team-private
codex plugin add ai-dev-team@ai-dev-team-private
codex plugin list --marketplace ai-dev-team-private
```

열려 있는 데스크톱 앱은 재시작한 뒤 새 Codex 채팅에서 스킬을 사용하세요. 회사가 허용한 별도 Git 소스를 쓰는 경우 그 저장소에도 먼저 설정 변경을 반영합니다.

[OpenAI 플러그인 패키징 및 마켓플레이스 문서](https://developers.openai.com/plugins/build/plugins)
