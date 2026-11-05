# 1. 설치할 것

수업 날 아침에 설치를 시작하면 1교시를 놓칩니다. **수업 전날까지** 이 페이지의 설치를 끝내고, 맨 아래 체크리스트를 확인해 주세요. 30분 정도 걸립니다.

!!! abstract "이 페이지에서 할 일"
    - 각자 PC에 **VS Code**, **Git**, **Python 3.12 이상**을 설치합니다.
    - VS Code에 **Python** 확장(Microsoft)을 설치합니다.
    - 확인 명령으로 세 프로그램이 잘 설치됐는지 봅니다.

    **예상 시간** 약 30분 (회사 PC에서 설치 승인을 받아야 하면 더 걸립니다)

| 프로그램 | 버전 | 왜 필요한가 |
|---|---|---|
| VS Code | 최신 (1.116 이상) | 오늘 모든 실습을 하는 편집기. Copilot Chat이 들어 있습니다 |
| Git | 최신 | GitHub 리포지토리를 내 PC로 가져오고(Clone), 커밋을 올립니다(Push) |
| Python | 3.12 이상 | 실습 프로그램(회의실 예약 서비스)을 실행하고 테스트합니다 |

!!! warning "회사 PC라면 먼저 확인하세요"
    회사 PC는 프로그램 설치 권한이 막혀 있거나, 회사망(프록시, 방화벽) 때문에 GitHub와 Copilot 접속이 안 될 수 있습니다. 이 페이지 아래 [회사 PC와 회사망](#company-pc)을 먼저 읽고, 필요하면 IT 담당 부서에 미리 요청합니다.

## STEP 1. VS Code 설치

1. 브라우저에서 아래 주소를 엽니다.

    ```text
    https://code.visualstudio.com/
    ```

2. 내 운영체제에 맞는 **Download** 버튼을 클릭합니다.
3. 받은 설치 파일을 실행합니다.
    - **Windows**: 설치 마법사에서 **Next**를 눌러 진행합니다. **Add to PATH**(경로에 추가) 항목이 보이면 체크된 상태로 둡니다.
    - **Mac**: 받은 파일을 열어 나오는 **Visual Studio Code** 앱을 **응용 프로그램(Applications)** 폴더로 옮깁니다.
4. VS Code를 실행합니다.
5. 이미 VS Code가 설치되어 있었다면 버전을 확인합니다.
    - **Windows**: 위쪽 메뉴 **Help** → **About**
    - **Mac**: 위쪽 메뉴 **Code** → **About Visual Studio Code**

확인: 버전 번호가 **1.116 이상**입니다. 낮으면 **Help** → **Check for Updates**(Mac은 **Code** → **Check for Updates**)로 업데이트하고 VS Code를 다시 시작합니다.

!!! tip "Copilot 확장은 따로 설치하지 않아요"
    VS Code 1.116부터 Copilot Chat이 기본으로 들어 있습니다. 예전 자료에서 "Copilot 확장을 설치하라"는 안내를 보더라도 따라 하지 않습니다.

## STEP 2. Git 설치

=== "Windows"

    1. 브라우저에서 아래 주소를 엽니다.

        ```text
        https://git-scm.com/
        ```

    2. **Download for Windows**를 클릭하고, 64비트용 설치 파일(x64 Setup)을 받습니다.
    3. 설치 파일을 실행합니다. 화면이 여러 번 나오지만 **기본값 그대로 Next**를 눌러 끝까지 진행하고 **Install**을 누릅니다.
    4. 설치가 끝나면 **Finish**를 누릅니다.
    5. 이미 열려 있던 VS Code가 있으면 완전히 닫았다가 다시 엽니다. 그래야 VS Code가 Git을 찾습니다.

=== "Mac"

    1. **응용 프로그램** → **유틸리티** → **터미널**을 엽니다.
    2. 아래 명령을 입력하고 Enter를 누릅니다.

        ```bash
        git --version
        ```

    3. Git이 없으면 "명령어 라인 개발자 도구를 설치하겠습니까?" 같은 창이 뜹니다. **설치**를 누르고 끝날 때까지 기다립니다(몇 분 걸립니다).
    4. 설치가 끝나면 2번 명령을 한 번 더 실행합니다.

확인: 터미널에서 `git --version`을 실행하면 `git version 2.xx.x` 같은 버전이 나옵니다.

## STEP 3. Git에 내 이름과 이메일 등록

커밋할 때 "누가 바꿨는지"가 함께 기록됩니다. 이 정보가 없으면 2교시 커밋에서 오류가 납니다.

1. 터미널(Windows는 **Git Bash** 또는 **명령 프롬프트**, Mac은 **터미널**)을 엽니다.
2. 아래 두 줄을 한 줄씩 실행합니다. 따옴표 안을 내 이름과 GitHub에 가입한 이메일로 바꿉니다.

    ```bash
    git config --global user.name "홍길동"
    git config --global user.email "my-email@example.com"
    ```

3. 아래 명령으로 등록한 값을 봅니다.

    ```bash
    git config --global --list
    ```

확인: 목록에 `user.name=홍길동`, `user.email=...`가 보입니다.

## STEP 4. Python 설치

=== "Windows"

    1. 브라우저에서 아래 주소를 엽니다.

        ```text
        https://www.python.org/downloads/
        ```

    2. 노란 **Download Python 3.1x.x** 버튼을 클릭합니다. 3.12 이상이면 어떤 버전이든 괜찮습니다.
    3. 받은 설치 파일을 실행합니다.
    4. **설치 첫 화면 맨 아래의 Add python.exe to PATH를 반드시 체크합니다.**
    5. **Install Now**를 클릭합니다.
    6. "Setup was successful"이 나오면 **Close**를 누릅니다.

    !!! warning "Add python.exe to PATH를 놓쳤다면"
        `python` 명령을 찾지 못하는 가장 흔한 원인입니다. Windows **설정** → **앱**에서 Python을 제거한 뒤, 이 STEP을 처음부터 다시 하면서 체크하는 것이 가장 빠릅니다.

=== "Mac"

    1. 브라우저에서 아래 주소를 엽니다.

        ```text
        https://www.python.org/downloads/
        ```

    2. 노란 **Download Python 3.1x.x** 버튼을 클릭해 `.pkg` 파일을 받습니다.
    3. 받은 파일을 실행하고 **계속**, **동의**, **설치**를 차례로 눌러 진행합니다. Mac 로그인 암호를 물으면 직접 입력합니다.
    4. 설치가 끝나면 **닫기**를 누릅니다.

확인: 새 터미널을 열고 아래 명령을 실행합니다.

```bash
python --version
```

`Python 3.12.x` 이상이 나오면 됩니다. Mac에서 `command not found`가 나오거나 3.12보다 낮은 버전이 나오면 `python3 --version`으로 다시 확인합니다. Mac에서는 오늘 실습 내내 `python` 대신 `python3`을 쓰면 됩니다.

## STEP 5. VS Code에 Python 확장 설치

1. VS Code를 엽니다.
2. 왼쪽 세로 막대(활동 막대)에서 네모 4개 모양의 **Extensions**(확장) 아이콘을 클릭합니다.
3. 위쪽 검색 칸에 `Python`을 입력합니다.
4. 목록에서 게시자가 **Microsoft**인 **Python**을 찾아 **Install**을 클릭합니다.
5. 설치가 끝나면 버튼이 **Install**에서 톱니바퀴 아이콘 등으로 바뀝니다.

확인: **Extensions** 보기의 **Installed**(설치됨) 목록에 **Python**(Microsoft)이 있습니다. 함께 설치되는 Pylance, Python Debugger 같은 확장도 그대로 둡니다.

!!! tip "VS Code 안에서 버전 확인하기"
    VS Code 위쪽 메뉴 **Terminal** → **New Terminal**을 누르면 아래쪽에 터미널이 열립니다. 여기서 `git --version`, `python --version`(Mac은 `python3 --version`)을 실행해 보세요. VS Code 터미널에서 잘 나오면 실습 준비가 된 것입니다.

## 회사 PC와 회사망 {#company-pc}

**설치 권한이 없을 때**: 설치 파일을 실행했는데 관리자 암호를 묻거나 "관리자에게 문의"가 나오면, IT 담당 부서에 VS Code, Git, Python 설치를 요청합니다. 수업 당일에는 시간이 없으니 미리 요청합니다.

**프록시를 쓰는 회사망**: VS Code는 PC의 시스템 프록시 설정을 그대로 따릅니다. 인증서(SSL) 오류가 나면 회사 프록시 인증서를 운영체제의 신뢰 저장소에 넣어야 하므로 IT 담당 부서에 요청합니다.

**방화벽**: Copilot(개인 플랜)이 동작하려면 아래 주소가 열려 있어야 합니다. IT 담당 부서에 이 목록을 그대로 전달합니다.

```text
github.com/login/*
github.githubassets.com
avatars.githubusercontent.com
*.individual.githubcopilot.com
copilot-proxy.githubusercontent.com
origin-tracker.githubusercontent.com
```

!!! note "그래도 안 되면"
    당일 회사망에서 Copilot이 안 되면 휴대폰 핫스팟으로 연결해 실습을 이어 갈 수 있습니다. 자세한 증상별 해결은 [3. 막혔을 때](3-troubleshooting.md)를 봅니다.

## 수업 전 체크리스트

- [ ] VS Code 버전이 1.116 이상입니다 (**Help** → **About**, Mac은 **Code** → **About Visual Studio Code**).
- [ ] 터미널에서 `git --version`이 버전을 보여 줍니다.
- [ ] `git config --global --list`에 `user.name`과 `user.email`이 있습니다.
- [ ] `python --version`(Mac은 `python3 --version`)이 3.12 이상입니다.
- [ ] VS Code **Extensions**에 **Python**(Microsoft)이 설치되어 있습니다.
- [ ] 다음 페이지 [2. Copilot 로그인과 확인](2-copilot.md)까지 끝냈습니다.
