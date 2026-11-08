# 실습 1-2. 내 리포지토리 만들고 VS Code 익히기

!!! abstract "이 실습에서 할 일"
    - Starter 템플릿으로 오늘 오전 내내 쓸 개인 리포지토리 `room-practice`를 만듭니다.
    - VS Code의 **Git: Clone**으로 내 PC에 가져오고, 테스트와 프로그램을 한 번씩 실행합니다.
    - 파일 탐색기로 프로젝트 구조를 둘러봅니다.

    **예상 시간** 약 11분

## 준비

- [실습 1-1](lab-1.md)을 끝냈어야 합니다.
- 오늘 실습 프로그램은 총무팀이 요청한 **회의실 예약 서비스**입니다. 지금은 공유 엑셀로 예약하고 있고, 이 서비스를 Copilot과 함께 고쳐 나갑니다.

## STEP 1. Starter 템플릿으로 리포지토리 만들기

1. 브라우저 주소창에 아래 주소를 입력하고 Enter를 누릅니다.

    ```text
    https://github.com/skilleat-labs/meeting-room-starter
    ```

2. 파일 목록 위쪽 오른편의 초록색 **Use this template**(이 템플릿 사용) 버튼을 클릭합니다.
3. 펼쳐진 메뉴에서 **Create a new repository**(새 리포지토리 만들기)를 클릭합니다.
4. 아래 표대로 입력합니다.

    | 항목 | 값 |
    |---|---|
    | **Include all branches** | 체크하지 않음 |
    | **Owner** | 내 GitHub 아이디 |
    | **Repository name** | `room-practice` |
    | 공개 범위 | **Public** |

    ```text
    room-practice
    ```

5. 맨 아래 초록색 **Create repository** 버튼을 클릭합니다.

확인: 화면 위쪽에 `내아이디 / room-practice`가 보이고, 그 아래 작은 글씨로 `generated from skilleat-labs/meeting-room-starter`가 보입니다.

!!! note "왜 Public으로 만드나요?"
    6교시에 현황판을 GitHub Pages로 배포합니다. 무료 계정은 Public 리포지토리여야 Pages를 쓸 수 있습니다. 실습 데이터의 이름과 연락처는 모두 가짜입니다.

## STEP 2. 리포지토리 주소 복사하기

1. `room-practice` 화면에서 초록색 **Code** 버튼을 클릭합니다.
2. **HTTPS** 탭이 선택된 상태에서 주소 오른쪽의 **복사** 아이콘(겹친 네모)을 클릭합니다.

확인: `https://github.com/내아이디/room-practice.git` 형태의 주소가 복사되었습니다.

## STEP 3. VS Code에서 Git: Clone

1. VS Code로 돌아옵니다.
2. 명령 팔레트를 엽니다. Windows는 `Ctrl+Shift+P`, Mac은 `⇧⌘P`입니다.
3. `Git: Clone`을 입력하고 목록에서 **Git: Clone**을 클릭합니다.
4. 위쪽 입력 칸에 STEP 2에서 복사한 주소를 붙여 넣고 Enter를 누릅니다.
5. 저장 위치를 고르는 창이 열립니다. **문서**(Documents) 폴더 안에 `copilot-lab` 폴더를 새로 만들고, 그 폴더를 고른 다음 **Select as Repository Destination**(리포지토리 위치로 선택)을 클릭합니다.
6. 오른쪽 아래에 "복제한 리포지토리를 열까요?" 알림이 뜨면 **Open**을 클릭합니다.

확인: VS Code 창 제목과 왼쪽 탐색기 맨 위에 `ROOM-PRACTICE`가 보입니다. 내 PC에는 `문서/copilot-lab/room-practice` 폴더가 생겼습니다.

## STEP 4. 작성자 신뢰 확인

처음 여는 폴더면 "이 폴더의 파일 작성자를 신뢰합니까?"라는 창이 뜹니다.

1. 내가 방금 만든 리포지토리이므로 **Yes, I trust the authors**(예, 작성자를 신뢰합니다)를 클릭합니다.

확인: 창이 닫히고 파일 목록이 보입니다. 화면 위쪽에 **Restricted Mode**(제한 모드) 표시가 없습니다.

!!! warning "모르는 폴더는 신뢰하지 마세요"
    신뢰하면 그 폴더의 설정과 작업이 실행될 수 있습니다. 출처를 모르는 코드를 열 때는 **No**를 고르는 습관을 들입니다.

## STEP 5. 터미널 열고 테스트 도구 설치

1. Windows는 ``Ctrl+` ``, Mac은 ``⌃` ``(Control과 숫자 1 왼쪽 키)를 누릅니다. 위쪽 메뉴 **Terminal** → **New Terminal**을 눌러도 됩니다.
2. 아래쪽에 터미널이 열리고, 현재 폴더가 `room-practice`인지 봅니다.
3. 아래 명령을 붙여 넣고 Enter를 누릅니다.

    === "Windows"

        ```bash
        python -m pip install -r requirements-dev.txt
        ```

    === "Mac"

        ```bash
        python3 -m pip install -r requirements-dev.txt
        ```

확인: 마지막 줄에 `Successfully installed ... pytest ...` 또는 `Requirement already satisfied`가 나옵니다.

!!! tip "명령은 Windows, Mac 탭에서 고릅니다"
    Mac은 `python` 대신 `python3`을 씁니다. 명령 위의 **Windows**, **Mac** 탭에서 내 OS를 한 번 고르면, 가이드의 모든 페이지에서 같은 탭이 선택됩니다. 글 속에 `python`이라고만 쓴 곳도 Mac은 `python3`으로 읽습니다. 예: `python3 -m pip install -r requirements-dev.txt`. 오늘 가이드의 `python`은 모두 `python3`으로 바꿔 읽으면 됩니다.

## STEP 6. 테스트 실행

=== "Windows"

    ```bash
    python -m pytest
    ```

=== "Mac"

    ```bash
    python3 -m pytest
    ```

확인: 아래처럼 **4 passed**가 나옵니다.

```text
....                                                                     [100%]
4 passed
```

!!! note "테스트가 뭔가요?"
    `tests/test_rules.py`에 "이런 예약은 통과, 이런 예약은 막기" 같은 확인 4개가 들어 있습니다. 코드를 바꾼 뒤 이 명령을 다시 돌려 기존 기능이 깨지지 않았는지 봅니다. GitHub에서도 커밋할 때마다 같은 테스트가 자동으로 돕니다(워크플로 이름 "테스트").

## STEP 7. 프로그램 실행해 보기

1. 회의실 목록을 봅니다.

    === "Windows"

        ```bash
        python -m booking rooms
        ```

    === "Mac"

        ```bash
        python3 -m booking rooms
        ```

    ```text
    R1 소회의실 A (4명, 3층)
    R2 소회의실 B (4명, 3층)
    R3 중회의실 (8명, 5층)
    R4 대회의실 (16명, 7층)
    ```

2. 11월 10일 예약을 봅니다.

    === "Windows"

        ```bash
        python -m booking list --date 2026-11-10
        ```

    === "Mac"

        ```bash
        python3 -m booking list --date 2026-11-10
        ```

    ```text
    #1 2026-11-10 10:00~11:00 R1 주간 업무 회의 (김민수, 4명)
    #2 2026-11-10 13:00~15:00 R3 신규 서비스 킥오프 (이지은, 7명)
    ```

확인: 두 명령의 결과가 위와 같습니다.

## STEP 8. VS Code 화면 익히기

처음 쓰는 분은 천천히 해 봅니다. 이미 익숙하면 건너뜁니다.

| 이름 | 어디에 | 하는 일 |
|---|---|---|
| **Activity Bar** (활동 막대) | 맨 왼쪽 아이콘 줄 | 탐색기, 소스 제어 같은 보기 바꾸기 |
| **Primary Side Bar** (기본 사이드바) | 왼쪽 | 파일 목록 |
| **Editor** (편집기) | 가운데 | 파일을 읽고 고치기 |
| **Secondary Side Bar** (보조 사이드바) | 오른쪽 | 기본으로 Chat 보기가 있는 곳 |
| **Panel** (패널) | 아래 | 터미널 |
| **Status Bar** (상태 표시줄) | 맨 아래 줄 | 브랜치 이름, Copilot 아이콘 |

1. Windows `Ctrl+B`, Mac `⌘B`를 두 번 눌러 왼쪽 사이드바를 닫았다가 엽니다.
2. Windows `Ctrl+P`, Mac `⌘P`를 누르고 `rules`를 입력해 Enter를 누릅니다. 파일 이름으로 바로 열립니다.
3. Windows `Ctrl+Shift+P`, Mac `⇧⌘P`를 누릅니다. 명령 팔레트(모든 명령을 찾는 입력 칸)가 열립니다. **Esc**로 닫습니다.
4. **File** → **Auto Save**를 켭니다. 저장을 잊어 Copilot과 내가 다른 내용을 보는 일을 줄입니다.
5. Windows `Ctrl+Alt+I`, Mac `⌃⌘I`로 Chat 보기를 엽니다.

확인: 파일 열기, 터미널, Chat 보기를 단축키로 열 수 있습니다. 전체 목록은 [VS Code와 Copilot 한 장 정리](../appendix/vscode-copilot.md)에 있습니다.

## STEP 9. 프로젝트 구조 둘러보기

왼쪽 활동 막대의 **Explorer**(탐색기, 종이 두 장 모양) 아이콘을 누르고, 폴더를 하나씩 펼쳐 봅니다.

| 폴더, 파일 | 무엇인가 | 오늘 쓰는 곳 |
|---|---|---|
| `docs/` | 현업 요청(`00_현업요청.md`), 킥오프 회의록(`01_킥오프_회의록.md`), 현행 업무(`02_현행_업무.md`), 월간 집계 업무(`04_월간집계_업무.md`) | 1-3, 2-3, 3교시, 7-2 |
| `booking/` | 예약 프로그램. `rules.py`(예약 규칙 검사), `service.py`(예약하기, 목록), `report.py`(이용률 보고서), `__main__.py`(명령 처리) | 2교시부터 계속 |
| `data/` | `rooms.json`(회의실 4개), `reservations.json`(예약 5건), `room_usage_2026-10.csv`(10월 사용 기록) | 프로그램이 읽고 씀, 7-2 |
| `tests/` | `test_rules.py`(테스트 4개) | 코드를 바꿀 때마다 |
| `build_site.py` | 예약 현황판 웹페이지 만들기 | 6, 7교시 |
| `.github/workflows/` | `ci.yml`(GitHub에서 테스트 자동 실행) | 2-3, 4교시 |

1. `docs/00_현업요청.md`를 클릭해 열고 처음 몇 줄을 읽습니다.
2. `booking/rules.py`를 열고 맨 아래쪽의 `# TODO:` 줄을 찾습니다.

확인: `rules.py`에서 "같은 회의실, 같은 날짜에 시간이 겹치는 예약은 막아야 한다"는 TODO 주석을 찾았습니다.

## 다 됐는지 확인

- [ ] github.com에 `내아이디/room-practice`(Public)가 있습니다.
- [ ] VS Code에서 `room-practice` 폴더가 열려 있고 신뢰했습니다.
- [ ] `python -m pytest`가 **4 passed**입니다.
- [ ] `python -m booking rooms`와 `python -m booking list --date 2026-11-10`이 위 결과와 같습니다.
- [ ] 왼쪽 사이드바, 파일 열기(`Ctrl+P` / `⌘P`), 명령 팔레트, Chat 보기를 열어 봤습니다.
- [ ] `docs/`, `booking/`, `data/`, `tests/`가 각각 무엇인지 말할 수 있습니다.

## 막히면

??? failure "Use this template 버튼이 안 보입니다"
    로그인이 안 되어 있거나 주소가 틀린 경우입니다. 오른쪽 위에 프로필 사진이 있는지, 주소가 정확히 `https://github.com/skilleat-labs/meeting-room-starter`인지 확인합니다. 창이 좁으면 버튼이 아래로 밀려 있을 수 있으니 창을 넓혀 봅니다.

??? failure "The repository room-practice already exists 라고 나옵니다"
    같은 이름의 리포지토리가 이미 있습니다. 강사에게 알리고, 안내에 따라 이름 뒤에 숫자를 붙여 만듭니다. 이후 실습의 `room-practice`는 바꾼 이름으로 읽습니다.

??? failure "Git: Clone이 목록에 없거나 Git을 찾을 수 없다고 나옵니다"
    Git이 설치되지 않았거나 Git 설치 전에 열어 둔 VS Code입니다. [설치할 것](../setup/1-install.md)의 STEP 2를 확인하고 VS Code를 완전히 닫았다가 다시 엽니다.

??? failure "Clone할 때 GitHub 로그인 창이 뜹니다"
    VS Code가 GitHub 접근을 허락해 달라는 창입니다. 허락하고, 열리는 브라우저에서 내 계정으로 로그인한 뒤 VS Code로 돌아옵니다.

??? failure "python 명령을 찾을 수 없거나 Microsoft Store가 열립니다"
    Mac은 `python3`으로 실행합니다. Windows는 Python 설치 때 **Add python.exe to PATH**를 체크하지 않은 경우입니다. [막혔을 때](../setup/3-troubleshooting.md)의 Python 항목을 봅니다.

??? failure "No module named booking 이라고 나옵니다"
    터미널의 현재 폴더가 `room-practice`가 아닙니다. VS Code에서 **File** → **Open Folder**로 `문서/copilot-lab/room-practice`를 열고 터미널을 새로 엽니다.
