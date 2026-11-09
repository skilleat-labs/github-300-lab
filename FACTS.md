# GH-300 공식 문서 사실 정리 (2026-11-04 조사)

교안과 가이드의 기술 내용은 **이 파일에 있는 것만** 쓴다. 출처 URL이 없는 내용은 쓰지 않는다. "(검색 요약)"은 페이지를 직접 열지 못하고 검색 결과로만 확인한 것이라, 가이드에서는 "화면 이름이 다를 수 있음"을 함께 적는다.

## 1. VS Code 설정
- VS Code 1.116(2026-04-15)부터 **Copilot Chat이 기본 내장**. 확장을 따로 설치하지 않는다. https://code.visualstudio.com/updates/v1_116
- 로그인: 상태 표시줄의 Copilot 아이콘에 마우스 → **Use AI Features** → 로그인 방법 선택. 또는 계정 메뉴에서 GitHub로 로그인, 또는 명령 팔레트 **GitHub Copilot: Sign in**. 구독이 없는 계정은 Copilot Free가 된다. https://code.visualstudio.com/docs/copilot/setup
- 상태 표시줄의 **Copilot status dashboard**에서 월 사용량(%)을 본다. https://code.visualstudio.com/docs/copilot/setup
- github.com에서 플랜 확인: 개인 설정 → **Billing & licensing** 또는 Copilot 설정. https://docs.github.com/en/copilot/how-tos/manage-your-account/get-started-with-a-copilot-plan
- 사용한 AI Credits는 GitHub 설정의 Copilot 사용량 페이지에서 본다. https://github.blog/changelog/2026-07-20-copilot-users-can-now-see-ai-credits-used-per-billing-cycle/
- 프록시: VS Code는 시스템 프록시를 따른다. 인증 방식 Basic, Digest, NTLM, Negotiate. SSL 오류면 프록시 인증서를 OS 신뢰 저장소에. https://code.visualstudio.com/docs/setup/network
- 회사 방화벽 허용 주소(개인 플랜): `github.com/login/*`, `github.githubassets.com`, `avatars.githubusercontent.com`, `*.individual.githubcopilot.com`, `copilot-proxy.githubusercontent.com`, `origin-tracker.githubusercontent.com`. https://docs.github.com/en/copilot/reference/copilot-allowlist-reference

## 2. Copilot Pro 플랜
- 월 10달러, 매월 **AI Credits 1,500**(기본 1,000 + 유연 500). https://docs.github.com/en/copilot/get-started/plans
- 1 크레딧 = 0.01달러. 모델과 토큰(입력, 출력, 캐시)에 따라 차감. 기본 크레딧부터 쓰고 매월 1일 00:00 UTC 초기화, 이월 없음. https://docs.github.com/copilot/concepts/billing/usage-based-billing-for-individuals
- 자동 모델 선택(Auto) 10% 할인 → 화면에서 Auto가 사라지고 Copilot Fusion(30% 할인, 11-30까지)으로 바뀜. 아래 2026-11-08 항목 참고. 같은 URL
- 크레딧을 쓰는 것: Chat, CLI, 클라우드 에이전트, Spaces, 타사 코딩 에이전트. 같은 URL
- **코드 완성(인라인 제안)과 다음 편집 제안(NES)은 유료 플랜에서 무제한, 크레딧을 쓰지 않는다.** 같은 URL
- 크레딧이 다 떨어지면: 상위 플랜으로 올리거나, 추가 사용 예산을 정하거나, 다음 달 초기화까지 기다린다. 같은 URL
- Pro에 포함: 에이전트 모드, 클라우드 에이전트, 코드 리뷰, MCP, Copilot CLI, 리포지토리·개인 사용자 지정 지침, 프롬프트 파일, 공개 코드 필터, PR 요약. **포함 안 됨: 콘텐츠 제외(Content exclusion), 조직 지침.** https://docs.github.com/en/copilot/get-started/plans
- Opus 계열 모델은 Pro에서 쓸 수 없다. 같은 URL
- 코드 리뷰는 **AI Credits와 Actions 사용 시간**을 쓴다. 리뷰 1회 평균 Lite 약 0.25달러, Balanced 약 1.50달러, Max 약 10달러. 기본 강도는 2026-09-28부터 Balanced. https://docs.github.com/en/copilot/reference/copilot-billing/models-and-pricing , https://github.blog/changelog/2026-08-28-upcoming-changes-to-github-copilot-policies-and-billing/
- Pro, Pro+ 신규 가입이 2026-04-20에 일시 중단됐다가 2026-06-17부터 단계적으로 다시 열림. 지금 열려 있는지는 확인 못 함. https://github.blog/news-insights/company-news/changes-to-github-copilot-individual-plans/ , https://github.blog/changelog/2026-06-17-copilot-individual-plan-sign-ups-are-reopening
- Spark는 github.com에서 종료(2026-08-04 신규 중단). https://github.blog/changelog/2026-08-04-upcoming-deprecation-of-github-spark-on-github-com/
- 2026-06-01부터 모든 플랜이 premium request 대신 AI Credits로 과금. https://github.blog/changelog/2026-06-01-updates-to-github-copilot-billing-and-plans/

## 3. VS Code의 Copilot 기능
- 단축키(Mac / Windows): Chat 보기 ⌃⌘I / Ctrl+Alt+I, 인라인 채팅 ⌘I / Ctrl+I(터미널에서도), Quick Chat ⇧⌥⌘L / Ctrl+Shift+Alt+L, 인라인 제안 수락 Tab, 거절 Esc. https://code.visualstudio.com/docs/agents/reference/ai-features-cheat-sheet
- **하네스(Harness)**: 언어 모델, 맥락, 도구를 조율하는 층. Copilot(일상 작업에 권장, 기본), Local(VS Code 내장, 창을 닫으면 멈춤), Claude, Codex. Chat 보기에서 **+(New Chat)** 후 **Session Target** 컨트롤로 고른다. 활성 하네스는 채팅 제목 앞에 표시. https://code.visualstudio.com/docs/agents/run/agent-harnesses
- **역할(Agent 선택기)**: **Ask**(질문, 코드 설명. 읽기 전용 도구만), **Agent**(변경을 구현하고 검증), **Plan**(조사 후 구현 계획. Copilot 하네스에서는 `/plan`). Edit 역할은 없다. 사용자 지정 에이전트도 같은 선택기에 나온다. Autopilot은 역할이 아니라 Copilot 하네스의 모드. 같은 URL
- 빠른 시작 기본값: Session Target **Copilot**, Agent **Agent**, Language model **Auto**, Permissions **Manual**(도구 사용을 내가 승인). https://code.visualstudio.com/docs/agents/quickstart
- 변경 검토: 채팅에 바뀐 파일과 diff 통계가 보이고, 눌러서 본다. diff에서 부분을 선택해 수정 요청 가능. 같은 URL
- ⌃⇧G / Ctrl+Shift+G는 **Source Control 보기**. **Changes**(스테이징 전), **Staged Changes** 목록. (에이전트 빠른 시작 문서는 같은 단축키를 Changes 패널로 부르지만, 가이드는 소스 제어 보기로 통일) https://code.visualstudio.com/docs/sourcecontrol/overview
- 되돌리기: 이전 요청에 마우스를 올리고 **Restore Checkpoint**. 파일과 채팅 기록을 되돌리지만 터미널 명령, 네트워크 요청, 배포, 외부 서비스는 되돌리지 않는다. 같은 URL
- 실행 중 조정: Send 드롭다운의 **Steer with Message**, **Stop and Send**. 멈춰도 이미 한 작업은 그대로. 같은 URL
- Agents 창: 제목 표시줄의 **Open in Agents** 또는 명령 **Chat: Open Agents window**. 같은 URL
- 슬래시 명령: `/plan /explain /fix /tests /doc /new /compact /clear /help /models /tools /init /agents /instructions /skills /prompts /create-instructions /create-prompt /create-skill /create-agent` 등. https://code.visualstudio.com/docs/agents/reference/ai-features-cheat-sheet
- 맥락: `#`를 치면 맥락 항목 목록(`#codebase`, `#fetch` 확인됨). **+(Add Context)** 버튼으로 Files & Folders, Symbols, Issue, Pull Request. 파일, 이미지 끌어다 놓기. **`@workspace` 같은 @참여자는 더 이상 쓰지 않으며 Copilot 하네스에서 동작하지 않는다.** https://code.visualstudio.com/docs/chat/copilot-chat-context
- Manual은 자동 승인되지 않은 작업만 확인을 요청한다. 읽기 전용 명령, 이미 허용한 규칙은 묻지 않을 수 있다. 버튼: **Allow Once**, in this Session, **Always Allow**. https://code.visualstudio.com/docs/agents/run/approvals
- 권한 수준 설정 `chat.permissions.default`: Manual(기본), Assisted, Allow all, Autopilot. 터미널 명령 자동 승인 `chat.tools.terminal.autoApprove`. 읽기 전용 명령은 자동, `rm`, `del`은 승인 필요. https://code.visualstudio.com/docs/agents/run/approvals

- 화면 이름: Activity Bar, Primary Side Bar, Secondary Side Bar(기본으로 Chat 보기), Editor, Panel, Status Bar. 단축키: Command Palette ⇧⌘P / Ctrl+Shift+P, Quick Open ⌘P / Ctrl+P, Primary Side Bar ⌘B / Ctrl+B. https://code.visualstudio.com/docs/getstarted/userinterface
- 자동 저장: **File** → **Auto Save**. https://code.visualstudio.com/docs/editor/codebasics
- 스마트 작업: 소스 제어 입력 칸의 반짝이 아이콘 **Generate Commit Message**. 코드 선택 후 오른쪽 클릭 **Explain**, **Generate Code** → **Generate Docs**, **Generate Tests**, **Fix**, **Review**. 터미널에서 실패한 명령 옆 반짝이 아이콘으로 설명과 수정. 병합 충돌 **Resolve Merge Conflict with AI**(실험 기능). https://code.visualstudio.com/docs/copilot/copilot-smart-actions
- 새 채팅 ⌘N / Ctrl+N, 터미널 인라인 채팅 ⌘I / Ctrl+I, `/doc`은 인라인 채팅에서 문서 주석 생성. https://code.visualstudio.com/docs/copilot/reference/copilot-vscode-features
- 맥락 항목 `#selection`(선택한 글), 파일 선택. 쓸 수 있는 `#` 목록은 하네스, 확장에 따라 다르고 도구 이름은 하네스마다 다를 수 있다. https://code.visualstudio.com/docs/agents/reference/tools-reference

## 4. 사용자 지정 파일
- 항상 적용되는 지침: `.github/copilot-instructions.md`(리포지토리 루트의 .github 폴더) 또는 루트의 `AGENTS.md`. 개인: `~/.copilot/copilot-instructions.md`. 명령 팔레트 **Chat: New Instructions File**. 적용 확인: 새 채팅에서 작업 후 응답의 **References**를 펼쳐 지침 파일이 들어갔는지 본다. https://code.visualstudio.com/docs/agent-customization/custom-instructions
- `.github` 폴더 관례: 워크플로는 `.github/workflows`(https://docs.github.com/en/actions/writing-workflows/about-workflows). `dependabot.yml`은 `.github`에(https://docs.github.com/en/code-security/dependabot/dependabot-version-updates/configuring-dependabot-version-updates). 이슈 양식 `.github/ISSUE_TEMPLATE`, 커뮤니티 파일(CONTRIBUTING, SECURITY 등)은 `.github`, 루트, `docs` 순서로 찾음(https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file). CODEOWNERS도 `.github` → 루트 → `docs`(https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners). PR 양식 `.github/pull_request_template.md`는 "hidden directory"(https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/creating-a-pull-request-template-for-your-repository). 리포지토리 지침은 `.github/copilot-instructions.md`, Markdown 자연어(https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions).
- 대상 지정 지침: `.github/instructions/*.instructions.md`, 머리말 `description`, `applyTo: '**/*.py'`. 같은 URL
- 프롬프트 파일: `.github/prompts/*.prompt.md`. 명령 **Chat: New Prompt File**. 실행은 Chat에서 `/이름` 또는 **Chat: Run Prompt**. **프롬프트 파일은 Chat 보기의 Local 하네스 세션에서만 실행된다.** 다른 하네스에서 재사용하려면 에이전트 스킬을 쓴다. 머리말 `description`, `agent`(ask/agent/plan), `model`, `tools`. 본문에서 `${selection}` 사용 예. https://code.visualstudio.com/docs/agent-customization/prompt-files
- 사용자 지정 에이전트: `.github/agents/*.agent.md`. 머리말 `name`, `description`, `tools`. 예전 `.chatmode.md`는 `.agent.md`로. https://code.visualstudio.com/docs/agent-customization/custom-agents
- (2026-11-08 확인) **Local 하네스는 관리되지 않는 편집기에서 기본으로 숨겨짐.** 보이게 하려면 실험 설정 `chat.editor.localAgent.enabled`. Copilot 하네스가 자동 선호(`chat.defaultToCopilotHarness`, `chat.editor.preferCopilotHarness`). 조직 정책으로 막힐 수 있음. 그래서 3-3은 프롬프트 파일 대신 스킬. https://code.visualstudio.com/docs/agents/run/agent-harnesses
- (화면 확인 2026-11-08) Session Target은 채팅 입력 칸 아래 줄에 하네스 이름(예: Copilot)으로 표시. 모델 선택기에 **Auto 없음**, 맨 위 **Copilot Fusion**(Standard). Fusion: 모델을 고르거나 조합. Standard는 모든 플랜, High/Max는 Max/Business/Enterprise. 2026-11-30까지 유료 플랜 모델 비용 30% 할인. https://docs.github.com/en/copilot/concepts/models/copilot-fusion (Auto 대체 여부는 공식 문서에 직접 문장 없음, 커뮤니티 공지 https://github.com/orgs/community/discussions/211017)
- 스킬 머리말 추가: `argument-hint`, `user-invocable`, `disable-model-invocation`, `context: fork`. `name` 최대 64자, 잘못된 문자면 조용히 로드 실패. `description` 최대 1024자. `/idea 뒤에 글`처럼 명령 뒤에 맥락을 이어 씀. 만들기: **Chat: Open Customizations** → Skills → New Skill. 개인 스킬 `~/.copilot/skills/`. 스킬은 Copilot in VS Code, Copilot CLI, Copilot app 등에서 동작. 같은 URL 아래
- 스킬: `.github/skills/<이름>/SKILL.md`. `name`은 소문자와 하이픈, 폴더 이름과 같게. `description`에 무엇을 하는지와 언제 쓰는지. `/이름`으로 실행하거나 요청이 맞으면 자동 로드. https://code.visualstudio.com/docs/agent-customization/agent-skills
- (2026-11-08 확인) **스킬은 개방형 표준(Agent Skills)**: "an open standard that works across multiple AI agents", 만든 스킬은 스킬을 지원하는 에이전트끼리 옮겨 쓸 수 있다. 단 위치와 선택 기능은 에이전트마다 다르다. 표준 https://agentskills.io . 하네스별 위치: Copilot `.github/skills/`(개인 `~/.copilot/skills/`), Anthropic Claude `.claude/skills/`(개인 `~/.claude/skills/`), OpenAI Codex `.agents/skills/`(개인 `~/.agents/skills/`). 스킬은 `SKILL.md`만이 아니라 폴더 전체(지침, 스크립트, 예시, 자료). 지침 파일과 차이: 지침은 항상 적용되는 규칙만, 스킬은 작업별로 필요할 때 불러오는 능력과 순서. 같은 URL
- (2026-11-08 확인) GitHub에서 스킬이 동작하는 곳: Copilot app, Copilot CLI, **github.com의 Copilot 클라우드 에이전트와 Copilot 코드 리뷰**, VS Code, Visual Studio, JetBrains의 에이전트 모드. 리포지토리 위치 `.github/skills`, `.claude/skills`, `.agents/skills` 중 하나, 개인 `~/.copilot/skills`, `~/.agents/skills`. "used by a range of different AI systems". https://docs.github.com/en/copilot/concepts/agents/about-agent-skills
- (2026-11-08 확인) 남이 만든 스킬 설치: GitHub CLI `gh skill search 주제`, `gh skill preview`(설치 없이 SKILL.md와 파일 목록 보기), `gh skill install OWNER/REPOSITORY SKILL`. 경고: "Skills are not verified by GitHub and may contain prompt injections, hidden instructions, or malicious scripts." 설치 전에 `gh skill preview`로 내용을 본다. https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/add-skills

## 5. MCP
- 추가: 명령 **MCP: Add Server**(HTTP 또는 Command), 또는 Chat의 Customizations → MCP Servers, 또는 확장 보기에서 `@mcp` 검색. 개인 설정 파일 `~/.copilot/mcp-config.json`. `.vscode/mcp.json`은 호환용으로만 남음. https://code.visualstudio.com/docs/agent-customization/mcp-servers
- GitHub MCP 서버 원격 주소 `https://api.githubcopilot.com/mcp/`, 기본 OAuth. (검색 요약) https://docs.github.com/en/copilot/how-tos/copilot-in-your-ide/customize-copilot/extend-copilot-with-tools-and-context/set-up-the-github-mcp-server

- MCP 서버 끄기, 지우기: **Chat: Open Customizations** → **MCP Servers** → 서버의 **...** → **Disable** 또는 **Uninstall**. 로그인이 필요한 서버는 게시자의 로그인 방법을 따른다. https://code.visualstudio.com/docs/copilot/customization/mcp-servers
- (화면 확인 2026-11-08) Copilot 하네스의 Agent 선택기에는 Ask, Agent와 확장이 추가한 사용자 지정 에이전트가 보이고 Plan은 없다. 계획은 `/plan`.

## 6. github.com의 Copilot
- 코드 리뷰: PR의 **Reviewers**에서 Copilot 옆 **Request**. 기본은 댓글형 리뷰(승인, 변경 요청이 아님). (검색 요약) https://docs.github.com/en/copilot/how-tos/copilot-on-github/use-copilot-agents/copilot-code-review
- PR 요약: PR 설명이나 댓글 칸의 Copilot 메뉴 → **Summary**. Free에서는 안 됨. (검색 요약) https://docs.github.com/en/copilot/responsible-use/pull-request-summaries
- 클라우드 에이전트(예전 이름 coding agent): Pro 포함. 이슈의 **Assignees**에서 **Copilot**을 지정하면 작업 후 항상 PR을 연다. (검색 요약) https://docs.github.com/en/copilot/how-tos/use-copilot-agents/cloud-agent/use-cloud-agent-on-github
- 클라우드 에이전트 PR: 기본 설정에서는 Copilot이 올린 변경에 워크플로가 자동 실행되지 않음. 병합 영역의 **Approve and run workflows**(쓰기 권한 필요)를 누른다. 먼저 변경, 특히 `.github/workflows/`를 읽는다. 끝나면 리뷰를 요청함. PR 댓글의 `@copilot`으로 수정 요청. https://docs.github.com/en/copilot/how-tos/use-copilot-agents/cloud-agent/use-cloud-agent-on-github
- Copilot은 PR을 **Ready for review**로 바꾸거나 승인, 병합할 수 없음. 맡긴 사람은 그 PR을 승인할 수 없음. https://docs.github.com/en/copilot/concepts/security-governance-and-network-settings/risks-and-mitigations
- Pages 사용자 지정 워크플로: 배포 작업에 최소 `pages: write`, `id-token: write`, `environment`(기본 `github-pages`) 필요. 예제 `configure-pages@v5`, `upload-pages-artifact@v4`, `deploy-pages@v4`. 무료 플랜 계정의 리포지토리는 Public이어야 함. https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages , https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site
- 병합 충돌: 같은 파일의 같은 줄을 다르게 고치거나 한쪽이 파일을 지울 때 발생. 다른 줄, 다른 파일은 보통 자동 병합. 해결은 최종 내용을 정하는 일. https://docs.github.com/en/pull-requests/reference/merge-conflicts
- (2026-11-08 확인) 브랜치: "a lightweight movable pointer to one of these commits". 파일을 복사하지 않아 만들고 지우는 일이 거의 즉시. "Branching means you diverge from the main line of development and continue to do work without messing with that main line." `HEAD`는 지금 있는 로컬 브랜치를 가리킴. https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell
- (2026-11-08 확인) GitHub 브랜치: 기능 개발, 버그 수정, 실험을 저장소 안의 분리된 공간에서 안전하게. 다른 사람의 변경과 떨어져(in isolation) 작업. 브랜치는 항상 기존 브랜치에서 만든다. 기본 브랜치(새 리포지토리는 `main`)가 PR의 기본 대상. 보호된 브랜치는 병합 전에 상태 검사, 리뷰 승인 등을 요구하고 강제 push와 삭제를 막을 수 있다. https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-branches
- (2026-11-08 확인) PR: "proposals to merge code changes into a project", 병합 전에 논의하고 검토하는 곳. 탭: Conversation(설명, 타임라인, 댓글, 리뷰), Commits(브랜치가 어떻게 바뀌었는지), Files changed(diff). Draft PR은 병합할 수 없음, Ready for review로 바꾸면 리뷰 요청. https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests
- (2026-11-08 확인) 리뷰 세 종류: Comment(승인도 변경 요청도 아닌 의견), Approve(병합해도 된다), Request changes(병합 전에 고쳐야 할 점). 관리자는 병합 전 승인을 필수로 할 수 있다. https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/about-pull-request-reviews . 리뷰 방법: **Files changed** → 줄에 댓글 → **Review changes** → 요약 → Approve 등 선택 → **Submit review**. "Pull request authors cannot approve their own pull requests." Request changes는 규칙으로 리뷰를 요구할 때만 병합을 막는다. https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/approving-a-pull-request-with-required-reviews
- (2026-11-08 확인) 병합 방법 세 가지: **Create a merge commit**(기본 버튼 Merge pull request, 브랜치의 커밋을 모두 남기고 병합 커밋 하나 추가, 전체 이력을 중시할 때), **Squash and merge**(PR의 커밋을 base에 커밋 하나로, 중간 커밋은 따로 남지 않음, PR이 논리적 변경 하나일 때), **Rebase and merge**(병합 커밋 없이 커밋을 하나씩 얹어 일직선 이력, 새 SHA가 생김, 커밋이 이미 잘 정리됐을 때). https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/about-pull-request-merges . 화면: 병합 버튼 옆 드롭다운에서 고르고 **Confirm merge** / **Confirm squash and merge** / **Confirm rebase and merge**. 보이는 방법은 리포지토리 설정에 따라 다름. 병합 후 브랜치 삭제는 선택. 이슈와 연결된 PR은 병합될 때 이슈를 닫음. https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/merging-a-pull-request
- github.com의 Copilot 진입점: github.com/copilot, 리포지토리의 **Agents** 탭. https://docs.github.com/en/copilot/concepts/copilot-surfaces/copilot-on-github
- Spaces: 모든 플랜. github.com/copilot/spaces → **Create space**. 질문은 크레딧 사용. https://docs.github.com/en/copilot/concepts/context/spaces

## 7. Copilot CLI
- 설치: `npm install -g @github/copilot`(Node 22 이상), `winget install GitHub.Copilot`, `brew install --cask copilot-cli`. Windows는 PowerShell 6 이상. 로그인 `/login`. 모든 플랜 포함. https://docs.github.com/en/copilot/how-tos/set-up/install-copilot-cli
- 실행 `copilot`. Shift+Tab으로 standard → plan → autopilot 전환. `@파일`로 파일 첨부, `!명령`으로 셸 실행. https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference

## 8. 개인정보와 안전장치 (개인 플랜)
- 프로필 사진 → **Copilot settings** → **Suggestions matching public code**: Allow 또는 Block. https://docs.github.com/en/copilot/how-tos/manage-your-account/manage-policies
- **2026-04-24부터 Free, Pro, Pro+ 사용자의 상호작용이 모델 학습에 쓰일 수 있다(기본값).** 끄려면 Copilot settings → **Allow GitHub to use my data for AI model training** → Disabled. Business, Enterprise는 해당 없음. 같은 URL
- 콘텐츠 제외는 Business, Enterprise 기능. Pro에는 없다. https://docs.github.com/en/copilot/concepts/context/content-exclusion
- 코드 참조: 공개 코드 일치를 허용하면 일치한 출처와 라이선스를 보여 준다. 인라인 제안의 1% 미만에서 일치가 생긴다. https://docs.github.com/en/copilot/concepts/completions/code-referencing

## 9. 프롬프트 작성 (GitHub 문서 "Prompt engineering for GitHub Copilot Chat")
- 9가지 전략(문서 순서): Start general, then get specific(넓게 시작해 구체적으로) / Give examples(예시를 준다) / Break complex tasks into simpler tasks(쪼갠다) / Avoid ambiguity(모호함을 피한다) / Provide relevant context(관련 맥락을 준다) / Experiment and iterate(바꿔 가며 반복) / Keep history relevant(대화 기록을 관련 있게, 필요 없으면 새 채팅) / Review Copilot's output(결과를 검토) / Follow good coding practices(좋은 코드 습관을 따른다). https://docs.github.com/en/copilot/using-github-copilot/copilot-chat/prompt-engineering-for-copilot-chat

## 10. GH-300 시험 범위 (2026-08-07 기준)
책임 있는 사용 15~20% / Copilot 기능 사용 25~30% / 데이터와 구조 10~15% / 프롬프트와 맥락 10~15% / 생산성 10~15% / 개인정보, 콘텐츠 제외, 안전장치 10~15%. https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/gh-300

## 11. 2025년 자료가 틀리는 것 (교안에 쓰지 말 것)
- premium request(→ AI Credits), Ask/Edit/Agent 모드(→ 하네스 + 역할 Ask/Agent/Plan), `@workspace`(→ `#codebase`), Copilot 확장 설치(→ 내장), coding agent(→ 클라우드 에이전트), Spark(종료), `.vscode/mcp.json`(→ 호환용), `.chatmode.md`(→ `.agent.md`).

## 시험 대비 장 근거 (2026-11-08 확인)
- 제안 생성 흐름: ① 맥락 수집(HTTPS, 커서 앞뒤 코드, 열린 탭, 파일 이름과 종류, FIM) ② 프록시(GitHub 소유 Azure 테넌트, 프롬프트 해킹 차단) ③ 유해 콘텐츠 필터(혐오 표현, 개인정보) ④ LLM 생성 ⑤ 후처리(유해 내용 제거, XSS·SQL 인젝션 검사, 공개 코드 일치 약 150자 이상 차단 선택) ⑥ 전달. https://learn.microsoft.com/en-us/training/modules/introduction-prompt-engineering-with-github-copilot/3-github-copilot-user-prompt-process-flow
- 출력물 소유: "GitHub does not claim ownership of your Input or Output." 라이선스 판단, 검토·테스트 책임은 사용자. GitHub Terms of Service J.2, J.4. https://docs.github.com/en/site-policy/github-terms/github-terms-of-service
- 조직 정책: Org Settings → Copilot → Policies / Models. https://docs.github.com/en/copilot/how-tos/administer-copilot/manage-for-organization/manage-policies
- 코드 리뷰: Org Settings → Copilot → Code review(리뷰 강도). Rulesets → "Automatically request Copilot code review". 리포지토리 리뷰가 사용자 지정 지침을 쓸지 API로 설정 가능. https://docs.github.com/en/copilot/how-tos/use-copilot-agents/request-a-code-review/configure-automatic-review
- 콘텐츠 제외: 리포지토리/조직 Settings → Copilot → Content exclusion. 조직 예 `"*": - "**/.env"`. IDE 반영 최대 30분, VS Code는 Developer: Reload Window. https://docs.github.com/en/copilot/how-tos/configure-content-exclusion/exclude-content-from-copilot
- 감사 로그: `action:copilot`, `actor:Copilot`. 180일. 로컬 프롬프트 등 클라이언트 세션 데이터는 기록 안 됨. https://docs.github.com/en/copilot/how-tos/administer-copilot/manage-for-organization/review-activity/review-audit-logs
- 좌석 REST: `GET /orgs/{org}/copilot/billing/seats`, `POST/DELETE /orgs/{org}/copilot/billing/selected_users`, `selected_teams`. https://docs.github.com/en/rest/copilot/copilot-user-management
- CLI 명령: `/plan /model /mcp /review /delegate(원격에 PR) /context /compact /init /clear /new`, `/resume`·`--continue`(세션 선택). https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference
- Chat 피드백: 답변 아래 thumbs up/down. 불쾌한 콘텐츠는 copilot-safety@github.com. https://docs.github.com/en/copilot/responsible-use/chat-in-your-ide

## 가상환경 (2026-11-09 확인)
- 만들기 `python -m venv .venv`. 켜기: bash/zsh `source .venv/bin/activate`, cmd `.venv\Scripts\activate.bat`, PowerShell `.venv\Scripts\Activate.ps1`. 끄기 `deactivate`. PowerShell은 `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`가 필요할 수 있음. https://docs.python.org/3/library/venv.html
- VS Code Python 확장은 새 터미널에서 선택한 환경을 자동 활성화(`python-envs.terminal.autoActivationType`, 기본 command). 기본 이름 `.venv`. `.venv` 폴더는 기계마다 새로 만들어야 함. https://code.visualstudio.com/docs/python/environments

- (2026-11-09 확인) github.com/copilot에서 이슈 초안 만들기(public preview): 프롬프트에 OWNER/REPO, 제목·본문·라벨·담당자 초안, 여러 개를 한 번에 요청하면 각각 초안, 검토 후 Create. 새 라벨을 만드는지는 문서에 없음. 플랜별 제공 여부 문서에 없음. https://docs.github.com/en/copilot/how-tos/copilot-on-github/copilot-for-github-tasks/use-copilot-to-create-or-update-issues
- (2026-11-09 강사 확인) Copilot Pro 계정에서 github.com/copilot 이슈 초안 만들기가 동작함. 5-1, 5-3, 6-3 이슈 만들기를 이 방법으로 바꿈.
