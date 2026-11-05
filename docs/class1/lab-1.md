# 실습 1-1. 환경 점검과 Copilot 설정

!!! abstract "이 실습에서 할 일"
    - VS Code에서 Copilot에 로그인되어 있는지, 플랜이 Pro인지 확인합니다.
    - github.com의 Copilot 설정에서 **공개 코드와 일치하는 제안 차단**, **내 데이터의 모델 학습 사용 끄기**를 합니다.
    - Chat을 열고 오늘 쓸 기본값(Session Target **Copilot**, 역할 **Ask**, 모델 **Auto**)을 맞춥니다.

    **예상 시간** 약 7분

## 준비

- [시작 전 준비](../setup/1-install.md)의 설치를 끝냈어야 합니다.
- 브라우저에서 github.com에 라이선스를 받은 계정으로 로그인해 둡니다.

## STEP 1. VS Code의 Copilot 로그인 확인

1. VS Code를 엽니다.
2. 아래쪽 상태 표시줄 오른편의 **Copilot 아이콘**에 마우스를 올립니다.
3. **Use AI Features**(AI 기능 사용) 버튼이 보이면 아직 로그인 전입니다. 클릭해서 GitHub로 로그인합니다. 방법은 [2. Copilot 로그인과 확인](../setup/2-copilot.md)의 STEP 3과 같습니다.
4. 왼쪽 아래 **계정** 아이콘(사람 모양)을 클릭해 로그인된 GitHub 아이디를 봅니다.

확인: 계정 메뉴에 라이선스를 받은 내 GitHub 아이디가 보입니다.

## STEP 2. 사용량 화면 열어 보기

1. 상태 표시줄의 **Copilot 아이콘**을 클릭합니다.
2. **Copilot status dashboard**가 열리면 이번 달 사용량(%)을 봅니다.

확인: 사용량 표시가 보입니다. 오늘 하루 동안 이 숫자가 얼마나 늘어나는지 쉬는 시간마다 한 번씩 봅니다.

!!! tip "크레딧을 쓰는 것과 쓰지 않는 것"
    회색 글씨로 나오는 **인라인 제안**과 **다음 편집 제안(NES)**은 크레딧을 쓰지 않습니다. **Chat**, **에이전트**, **코드 리뷰**는 크레딧(월 1,500)을 씁니다.

## STEP 3. github.com에서 Copilot 설정 열기

1. 브라우저에서 `https://github.com`을 엽니다.
2. 오른쪽 위 **프로필 사진**을 클릭합니다.
3. 메뉴에서 **Copilot settings**(Copilot 설정)를 클릭합니다.
4. 화면 위쪽에서 플랜 이름을 봅니다.

확인: 플랜이 **Copilot Pro**로 보입니다. Free로 보이면 [막혔을 때](../setup/3-troubleshooting.md#license)를 봅니다.

!!! note "화면이 조금 다를 수 있어요"
    Copilot 설정 화면의 배치는 자주 바뀝니다. 메뉴 이름으로 찾으면 됩니다.

## STEP 4. 공개 코드와 일치하는 제안 차단

Copilot의 제안이 공개 리포지토리의 코드와 그대로 일치하는 경우가 드물게(인라인 제안의 1% 미만) 있습니다. 회사 업무에서는 라이선스 문제를 피하려고 이런 제안을 막아 둡니다.

1. Copilot settings 화면에서 **Suggestions matching public code**(공개 코드와 일치하는 제안) 항목을 찾습니다.
2. 오른쪽 드롭다운을 클릭합니다.
3. **Block**(차단)을 고릅니다.

확인: **Suggestions matching public code**가 **Block**으로 보입니다.

## STEP 5. 내 데이터의 모델 학습 사용 끄기

2026년 4월 24일부터 Free, Pro, Pro+ 사용자의 Copilot 사용 내용은 **기본값으로 모델 학습에 쓰일 수 있습니다.** 오늘은 회사 업무를 연습하는 자리이므로 강사 안내에 따라 끕니다.

1. 같은 화면에서 **Allow GitHub to use my data for AI model training**(내 데이터를 AI 모델 학습에 쓰도록 허용) 항목을 찾습니다.
2. 오른쪽 드롭다운을 클릭합니다.
3. **Disabled**(사용 안 함)를 고릅니다.

확인: **Allow GitHub to use my data for AI model training**이 **Disabled**로 보입니다.

!!! warning "Pro에는 콘텐츠 제외 기능이 없어요"
    특정 파일을 Copilot이 아예 읽지 못하게 막는 **콘텐츠 제외**(Content exclusion)는 Business, Enterprise 플랜 기능입니다. 개인 Pro 계정으로 회사 코드를 다룰 때는 민감한 파일을 Chat에 첨부하지 않는 습관이 더 중요합니다. 7교시에 다시 다룹니다.

## STEP 6. Chat 열기

1. VS Code로 돌아옵니다.
2. Windows는 `Ctrl+Alt+I`, Mac은 `⌃⌘I`를 누릅니다.
3. 오른쪽(또는 옆)에 **Chat** 보기가 열립니다.

확인: 아래쪽에 질문을 입력하는 칸이 있는 Chat 보기가 보입니다.

## STEP 7. 오늘의 기본값 맞추기

Chat에는 세 가지 선택기가 있습니다. 하나씩 확인합니다.

| 선택기 | 뜻 | 오늘 기본값 |
|---|---|---|
| **Session Target** | 어떤 하네스(Copilot이 일하는 방식)로 대화할지 | **Copilot** |
| **Agent** 선택기 (역할) | **Ask**(질문, 설명. 파일을 고치지 않음), **Agent**(변경을 구현하고 검증), **Plan**(계획) | 지금은 **Ask** |
| 모델 | 어떤 언어 모델을 쓸지 | **Auto** |

1. Chat 보기 위쪽의 **+**(**New Chat**, 새 채팅)를 클릭합니다.
2. **Session Target** 컨트롤에서 **Copilot**을 고릅니다. 이미 Copilot이면 그대로 둡니다.
3. 입력 칸 근처의 **Agent** 선택기를 클릭하고 **Ask**를 고릅니다.
4. 모델 선택기를 클릭하고 **Auto**를 고릅니다.

확인: 새 채팅의 Session Target이 **Copilot**, 역할이 **Ask**, 모델이 **Auto**입니다.

!!! note "화면이 조금 다를 수 있어요"
    VS Code는 매달 업데이트되어 선택기의 위치와 모양이 바뀔 수 있습니다. 이름(**Session Target**, **Ask**, **Auto**)으로 찾으면 됩니다. 활성 하네스 이름은 채팅 제목 앞에 표시됩니다.

!!! tip "왜 Auto인가요?"
    **Auto**는 작업에 맞는 모델을 자동으로 고르고, 모델 비용을 10% 할인받습니다. 오늘은 모델을 바꾸지 않고 Auto로 진행합니다.

## STEP 8. 첫 인사 보내기

Chat 입력 칸에 붙여 넣고 Enter를 누릅니다.

```text
안녕하세요. 지금 어떤 역할(Ask, Agent, Plan)로 대화하고 있는지와, 이 역할로 할 수 있는 일을 두 줄로 알려 주세요.
```

확인: 한국어 답이 돌아옵니다. Ask 역할이라 파일은 고치지 않는다는 내용이 들어 있으면 됩니다. 문장은 사람마다 다릅니다.

## 다 됐는지 확인

- [ ] VS Code 계정 메뉴에 내 GitHub 아이디가 보입니다.
- [ ] Copilot settings에서 플랜이 **Copilot Pro**입니다.
- [ ] **Suggestions matching public code**가 **Block**입니다.
- [ ] **Allow GitHub to use my data for AI model training**이 **Disabled**입니다.
- [ ] Chat이 열리고, Session Target **Copilot**, 역할 **Ask**, 모델 **Auto**입니다.
- [ ] Chat에서 한국어 답을 받았습니다.

## 막히면

??? failure "상태 표시줄에 Copilot 아이콘이 없습니다"
    VS Code 버전이 낮을 수 있습니다. **Help** → **About**(Mac은 **Code** → **About Visual Studio Code**)에서 1.116 이상인지 확인하고, 낮으면 업데이트 후 다시 시작합니다. 상태 표시줄 자체가 안 보이면 **View** → **Appearance** → **Status Bar**를 켭니다.

??? failure "Copilot settings 메뉴가 프로필 메뉴에 없습니다"
    **프로필 사진** → **Settings**로 들어가 왼쪽 메뉴에서 **Copilot** 항목을 찾습니다. 그래도 없으면 라이선스가 없는 계정일 수 있으니 [라이선스 문제](../setup/3-troubleshooting.md#license)를 봅니다.

??? failure "Allow GitHub to use my data for AI model training 항목이 없습니다"
    회사 조직이 관리하는 Business, Enterprise 라이선스 계정은 이 항목이 해당되지 않아 보이지 않을 수 있습니다. 화면을 강사에게 보여 주고 플랜을 같이 확인합니다.

??? failure "Ctrl+Alt+I(⌃⌘I)를 눌러도 Chat이 열리지 않습니다"
    다른 프로그램이 같은 단축키를 쓰고 있을 수 있습니다. 명령 팔레트(Windows `Ctrl+Shift+P`, Mac `⇧⌘P`)를 열고 `Chat`을 입력해 Chat 보기를 여는 명령을 고릅니다.

??? failure "Chat에 로그인하라는 안내만 나옵니다"
    STEP 1의 로그인이 끝나지 않은 상태입니다. 상태 표시줄 Copilot 아이콘 → **Use AI Features**로 로그인하거나, 명령 팔레트에서 `GitHub Copilot: Sign in`을 실행합니다.
