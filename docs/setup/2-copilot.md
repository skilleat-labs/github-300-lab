# 2. Copilot 로그인과 확인

오늘 과정은 회사가 지급한 **Copilot Pro** 라이선스로 진행합니다. 이 페이지에서 내 GitHub 계정에 Pro가 붙어 있는지 확인하고, VS Code에서 그 계정으로 로그인합니다.

!!! abstract "이 페이지에서 할 일"
    - github.com에서 내 계정의 Copilot 플랜이 **Pro**인지 확인합니다.
    - VS Code에서 같은 GitHub 계정으로 Copilot에 로그인합니다.
    - **AI Credits**가 무엇이고, 무엇을 할 때 줄어드는지 알아 둡니다.

    **예상 시간** 약 10분

## STEP 1. github.com 로그인

1. 브라우저에서 `https://github.com`을 엽니다.
2. 오른쪽 위 **Sign in**을 눌러 개인 GitHub 계정으로 로그인합니다. 이미 로그인되어 있으면 다음 STEP으로 갑니다.
3. 오른쪽 위 **프로필 사진**을 클릭해 내 아이디가 맞는지 확인합니다.

확인: 프로필 메뉴 맨 위에 **강사에게 알려 준 GitHub 아이디**가 보입니다. Copilot Pro는 그 아이디에 지급됩니다.

!!! warning "계정이 여러 개라면"
    회사 계정과 개인 계정이 따로 있으면, 라이선스를 받은 계정으로 로그인했는지 꼭 확인합니다. 다른 계정으로 로그인하면 Copilot이 **Free**로 보입니다.

## STEP 2. Copilot 플랜 확인

1. 오른쪽 위 **프로필 사진** → **Settings**(설정)를 클릭합니다.
2. 왼쪽 메뉴에서 **Billing & licensing**(결제와 라이선스)을 클릭합니다.
3. Copilot 항목에서 플랜 이름을 봅니다.
4. 같은 내용은 **프로필 사진** → **Copilot settings**(Copilot 설정)에서도 볼 수 있습니다.

확인: 플랜이 **Copilot Pro**로 보입니다.

!!! note "화면이 조금 다를 수 있어요"
    GitHub 설정 화면은 자주 바뀝니다. 메뉴 위치가 달라도 **Billing & licensing** 또는 **Copilot settings** 중 한 곳에서 플랜 이름을 찾으면 됩니다. Pro가 아니라 **Free**로 보이면 [3. 막혔을 때](3-troubleshooting.md#license)를 봅니다.

## STEP 3. VS Code에서 Copilot 로그인

1. VS Code를 엽니다.
2. 아래쪽 상태 표시줄 오른편의 **Copilot 아이콘**에 마우스를 올립니다.
3. 나오는 창에서 **Use AI Features**(AI 기능 사용)를 클릭합니다.
4. 로그인 방법에서 **GitHub**로 로그인을 고릅니다.
5. 브라우저가 열리면 STEP 1에서 확인한 계정으로 로그인하고, VS Code 연결을 허락합니다.
6. 브라우저에 VS Code로 돌아가라는 안내가 나오면 VS Code 창으로 돌아갑니다. "VS Code를 열까요?" 같은 브라우저 확인 창이 뜨면 열기를 누릅니다.

확인: 상태 표시줄의 Copilot 아이콘에 경고 표시가 없고, 왼쪽 아래 **계정** 아이콘(사람 모양)을 누르면 내 GitHub 아이디가 보입니다.

!!! tip "다른 로그인 방법"
    **Use AI Features**가 보이지 않으면 명령 팔레트(Windows `Ctrl+Shift+P`, Mac `⇧⌘P`)를 열고 `GitHub Copilot: Sign in`을 입력해 실행합니다. 왼쪽 아래 **계정** 아이콘에서 GitHub로 로그인해도 됩니다.

## STEP 4. 사용량 보기 (Copilot status dashboard)

1. 상태 표시줄의 **Copilot 아이콘**을 클릭합니다.
2. **Copilot status dashboard**(Copilot 상태 화면)가 열립니다.
3. 이번 달 사용량이 % 로 보이는지 확인합니다.

확인: 사용량 표시가 보입니다. 처음에는 0%에 가깝습니다.

github.com에서는 **Settings**의 Copilot 사용량 페이지에서 이번 결제 주기에 쓴 AI Credits를 볼 수 있습니다.

## AI Credits 알아 두기

Copilot Pro는 매월 **AI Credits 1,500**을 줍니다(기본 1,000 + 유연 500). 1 크레딧은 0.01달러이고, 모델과 주고받은 글의 양에 따라 줄어듭니다. 매월 1일 00:00(UTC)에 다시 채워지고, 남은 크레딧은 다음 달로 넘어가지 않습니다.

| 기능 | 크레딧 |
|---|---|
| 인라인 제안(코드 완성) | **쓰지 않음** (무제한) |
| 다음 편집 제안(NES) | **쓰지 않음** (무제한) |
| Chat (Ask, Agent, `/plan`) | 씀 |
| 에이전트, 클라우드 에이전트 | 씀 |
| 코드 리뷰 | 씀 (1회 약 150크레딧, Balanced 기준) |

오늘 수업의 크레딧 규칙은 세 가지입니다.

1. **모델은 Auto**를 씁니다. Auto는 작업에 맞는 모델을 고르고, 모델 비용을 10% 할인받습니다.
2. 같은 질문을 여러 번 반복하지 않습니다. 답이 마음에 들지 않으면 프롬프트를 고쳐서 한 번 더 묻습니다.
3. 코드 리뷰와 클라우드 에이전트는 **팀당 정해진 횟수만** 합니다. 강사가 안내합니다.

!!! tip "크레딧이 떨어지면"
    상위 플랜으로 올리거나, 추가 사용 예산을 정하거나, 다음 달 초기화까지 기다려야 합니다. 수업 중에는 강사에게 먼저 알려 주세요. 인라인 제안과 NES는 크레딧이 없어도 계속 됩니다.

## 다 됐는지 확인

- [ ] github.com의 **Billing & licensing** 또는 **Copilot settings**에서 플랜이 **Copilot Pro**입니다.
- [ ] VS Code에서 같은 GitHub 계정으로 로그인되어 있습니다.
- [ ] **Copilot status dashboard**에서 사용량을 볼 수 있습니다.
- [ ] 크레딧을 쓰는 기능과 쓰지 않는 기능을 구분할 수 있습니다.
