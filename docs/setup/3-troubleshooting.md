# 3. 막혔을 때

실습 중에 자주 나오는 문제와 해결 방법을 모았습니다. 각 실습 페이지의 "막히면"에도 그 실습에 맞는 대처가 있습니다.

## 계정과 로그인

??? failure "VS Code에서 Copilot 로그인이 끝나지 않습니다"
    1. 브라우저에서 로그인한 뒤 VS Code로 돌아오는 확인 창을 놓쳤을 수 있습니다. 브라우저 탭을 다시 보고, "VS Code를 열까요?" 같은 창이 있으면 열기를 누릅니다.
    2. 명령 팔레트(Windows `Ctrl+Shift+P`, Mac `⇧⌘P`) → `GitHub Copilot: Sign in`을 실행해 다시 로그인합니다.
    3. 회사망이면 아래 [회사망과 프록시](#network)를 봅니다.

??? failure "VS Code에 다른 GitHub 계정으로 로그인되어 있습니다"
    1. VS Code 왼쪽 아래 **계정** 아이콘(사람 모양)을 클릭합니다.
    2. 지금 로그인된 GitHub 아이디에 마우스를 올리고 **Sign Out**(로그아웃)을 누릅니다.
    3. [2. Copilot 로그인과 확인](2-copilot.md)의 STEP 3대로 라이선스를 받은 계정으로 다시 로그인합니다. 브라우저에서도 그 계정으로 로그인되어 있어야 합니다.

## 라이선스 {#license}

??? failure "Copilot 플랜이 Pro가 아니라 Free로 보입니다"
    구독이 없는 계정으로 로그인하면 Copilot Free가 됩니다.

    1. github.com 오른쪽 위 프로필 사진을 눌러 **라이선스를 받은 계정**인지 확인합니다.
    2. 맞는 계정인데도 Free라면, 라이선스 지급이 아직 반영되지 않은 것입니다. 강사에게 GitHub 아이디를 알려 주세요.
    3. 강사가 지급을 확인한 뒤에는 VS Code에서 로그아웃했다가 다시 로그인합니다.

## 회사망과 프록시 {#network}

??? failure "Copilot이 응답하지 않거나 네트워크 오류가 납니다"
    VS Code는 PC의 시스템 프록시 설정을 따릅니다. 회사 방화벽에서 아래 주소가 막혀 있으면 Copilot이 동작하지 않습니다. IT 담당 부서에 허용을 요청합니다.

    ```text
    github.com/login/*
    github.githubassets.com
    avatars.githubusercontent.com
    *.individual.githubcopilot.com
    copilot-proxy.githubusercontent.com
    origin-tracker.githubusercontent.com
    ```

    수업 중이라 기다릴 수 없으면 휴대폰 핫스팟으로 연결해 이어 갑니다.

??? failure "SSL 또는 인증서 오류가 납니다"
    회사 프록시가 인증서를 바꿔 끼우는 경우입니다. 회사 프록시 인증서를 운영체제의 신뢰 저장소에 넣어야 합니다. IT 담당 부서에 요청합니다.

## Python과 테스트

??? failure "python 명령을 찾을 수 없다고 나옵니다"
    - **Mac**: 터미널 줄 앞에 `(.venv)`가 있는지 봅니다. 없으면 가상환경이 꺼진 것입니다. `source .venv/bin/activate`로 켜면 `python`이 됩니다. `.venv` 폴더가 아직 없으면(가상환경을 만들기 전) `python3`으로 실행합니다.
    - **Windows**: Python을 설치할 때 **Add python.exe to PATH**를 체크하지 않은 경우가 많습니다. Windows **설정** → **앱**에서 Python을 제거하고, 다시 설치하면서 체크합니다. 설치 뒤에는 VS Code를 완전히 닫았다가 다시 엽니다.
    - 확인: VS Code 터미널에서 `python --version`(Mac은 `python3 --version`)이 3.12 이상을 보여 줍니다.

??? failure "Windows에서 python을 치면 Microsoft Store가 열립니다"
    Python이 설치되지 않았거나 PATH에 없는 경우입니다. 위 항목처럼 python.org에서 받은 설치 파일로 **Add python.exe to PATH**를 체크해 다시 설치합니다.

??? failure "No module named pytest 라고 나옵니다"
    가상환경이 꺼져 있거나, 이 리포지토리의 가상환경에 아직 설치하지 않았습니다. 리포지토리 폴더가 열린 VS Code 터미널에서 터미널 줄 앞에 `(.venv)`가 있는지 먼저 봅니다. 없으면 켭니다(Windows `.venv\Scripts\Activate.ps1`, Mac `source .venv/bin/activate`). `.venv` 폴더 자체가 없으면 [실습 1-2 STEP 5](../class1/lab-2.md)처럼 만듭니다. 켠 다음 설치합니다.

    ```bash
    python -m pip install -r requirements-dev.txt
    ```

    설치가 끝나면 `python -m pytest`를 다시 실행합니다.

??? failure "Copilot Agent가 테스트를 돌렸더니 No module named pytest 라고 나옵니다"
    Agent가 연 터미널에 가상환경이 켜지지 않은 경우입니다. 명령 팔레트에서 **Python: Select Interpreter**를 열고 `.venv`가 들어간 Python을 고른 뒤 다시 시킵니다. 또는 Chat에 "가상환경 .venv를 켜고 테스트를 실행해 줘"라고 덧붙입니다.

??? failure "Windows에서 Activate.ps1을 실행하면 '스크립트를 실행할 수 없으므로' 오류가 납니다"
    PowerShell이 스크립트 실행을 막는 설정입니다. Python 문서에 따르면 내 계정에서만 허용하면 됩니다: `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`. 회사 PC라서 막히면 터미널 **+** 옆 **∨**에서 **Command Prompt**를 열고 `.venv\Scripts\activate.bat`로 켭니다.

??? failure "No module named booking 이라고 나옵니다"
    터미널의 현재 폴더가 `room-practice`가 아닙니다. VS Code에서 **File** → **Open Folder**로 `room-practice` 폴더를 연 다음, **Terminal** → **New Terminal**로 터미널을 새로 엽니다.

## Git과 GitHub

??? failure "커밋하려는데 user.name, user.email을 설정하라고 나옵니다"
    Git에 내 이름과 이메일이 등록되지 않았습니다. 터미널에서 아래 두 줄을 실행하고 다시 커밋합니다.

    ```bash
    git config --global user.name "홍길동"
    git config --global user.email "my-email@example.com"
    ```

??? failure "Push(Sync)할 때 로그인 창이 뜨거나 인증에 실패합니다"
    VS Code가 GitHub 로그인을 요청하는 창을 띄우면 허락하고, 열리는 브라우저에서 내 GitHub 계정으로 로그인합니다. 로그인 후 VS Code로 돌아와 다시 **Sync Changes**를 누릅니다. 계정이 여러 개라면 `room-practice`를 만든 계정으로 로그인해야 합니다.

??? failure "Git: Clone 명령이 안 보이거나 Git을 찾을 수 없다고 나옵니다"
    Git이 설치되지 않았거나, Git 설치 전에 열어 둔 VS Code입니다. [1. 설치할 것](1-install.md)의 STEP 2로 Git을 설치하고 VS Code를 완전히 닫았다가 다시 엽니다.

## Copilot 사용

??? failure "AI Credits를 다 썼습니다"
    인라인 제안과 다음 편집 제안(NES)은 크레딧을 쓰지 않으므로 계속 됩니다. Chat과 에이전트는 상위 플랜으로 올리거나, 추가 사용 예산을 정하거나, 다음 달 1일 초기화까지 기다려야 합니다. 수업 중에는 강사에게 알리고 옆 사람 화면으로 함께 진행합니다. 남은 양은 상태 표시줄 Copilot 아이콘 → **Copilot status dashboard**에서 봅니다.

??? failure "같은 질문인데 옆 사람과 Copilot 답이 다릅니다"
    정상입니다. Copilot의 답은 매번 달라집니다. 가이드는 "이런 내용이 나오면 됩니다"라는 기준으로 쓰여 있습니다. 문장이 달라도 각 STEP의 **확인:** 기준을 만족하면 됩니다. 기준을 벗어나면 프롬프트를 더 구체적으로 고쳐 다시 묻습니다.

??? failure "에이전트가 엉뚱한 파일까지 고쳤습니다"
    Chat에서 그 변경을 만든 **내 요청**에 마우스를 올리고 **Restore Checkpoint**를 누릅니다. 그 요청 이전 상태로 파일과 채팅 기록이 돌아갑니다. 단, 이미 실행한 터미널 명령이나 외부 서비스에 한 일은 되돌아가지 않습니다. 되돌린 뒤 "booking/rules.py만 고쳐 줘"처럼 범위를 좁혀 다시 요청합니다.

??? failure "예약 데이터(data/reservations.json)가 바뀌었습니다"
    `python -m booking add`로 예약을 넣으면 `data/reservations.json`에 예약이 추가됩니다. 실습용 데이터는 되돌려 둡니다.

    1. 왼쪽 활동 막대의 **소스 제어** 아이콘(가지 모양)을 클릭합니다. 단축키는 Windows `Ctrl+Shift+G`, Mac `⌃⇧G`입니다.
    2. **Changes** 목록에서 `reservations.json`에 마우스를 올립니다.
    3. 굽은 화살표 모양의 **Discard Changes**(변경 취소)를 클릭합니다. 확인 창이 뜨면 변경을 버리는 버튼을 한 번 더 누릅니다.

    확인: `python -m booking list`에 예약이 #1부터 #5까지 5건만 보입니다.

## VS Code

??? failure "가이드의 단축키(예: 소스 제어 ⌃⇧G)가 동작하지 않습니다"
    - Mac은 `⌘`(Command)와 `⌃`(Control)를 구분합니다. 소스 제어는 `⌃` + Shift + G입니다.
    - 한/영이 한글이면 영문으로 바꾸고 다시 누릅니다.
    - 다른 확장이 같은 키를 쓰는 경우입니다. 명령 팔레트에서 **Preferences: Open Keyboard Shortcuts**를 열고, 검색 칸의 키보드 아이콘(**Record Keys**)을 누른 뒤 그 키를 누릅니다. 원래 명령(예: **View: Show Source Control**) 말고 다른 명령이 있으면 그 줄을 오른쪽 클릭 → **Remove Keybinding**으로 지웁니다.
    - 수업 중에는 단축키 대신 왼쪽 활동 막대의 아이콘을 눌러도 됩니다.

## 그래도 안 되면: Copilot에게 묻기 { #copilot }

오늘의 연습이기도 합니다. 막히면 먼저 Copilot과 함께 해결합니다.

1. 오류 메시지나 터미널 출력을 그대로 복사합니다. 화면 문제라면 캡처 이미지를 Chat 입력 칸에 끌어다 놓아도 됩니다.
2. Chat(Ask)에 붙여 넣고 묻습니다.

    ```text
    실습 중에 아래 오류가 났습니다. 원인을 쉬운 말로 설명하고, 확인할 것과 해결 순서를 하나씩 알려 주세요. 명령을 실행해야 하면 그 명령이 무엇을 하는지도 알려 주세요.
    (오류 메시지 붙여 넣기)
    ```

3. 제안된 명령은 뜻을 읽고 내가 실행합니다. 파일을 지우거나 설치하는 명령은 한 번 더 확인합니다.

Copilot 자체가 답하지 않는 문제(로그인, 라이선스, 네트워크)는 이 페이지의 위쪽 항목을 봅니다.
