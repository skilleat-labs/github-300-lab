# 실습 7-1. 보안 검토 (XSS)

!!! abstract "이 실습에서 할 일"
    - 개인 리포지토리 `room-practice`에서 회의 제목에 스크립트를 넣어 현황판의 보안 문제(XSS)를 직접 재현합니다.
    - Copilot에게 보안 검토를 맡기고, 제안을 검토해 Agent로 고칩니다. Copilot 결과도 놓친 곳이 없는지 사람이 확인합니다.
    - 다시 열어 스크립트가 글자로만 보이는지 확인하고, 테스트를 추가해 커밋합니다.

**소요 시간** 약 10분  **실습 장소** 개인 리포지토리 `room-practice` (VS Code)  **관련 교안** [7교시 교안](index.md)

## 준비

- 팀 리포지토리가 아니라 **개인 리포지토리**에서 합니다. 팀원끼리 같은 파일을 동시에 고쳐 충돌이 나지 않게 하려는 것입니다.
- VS Code에서 **File** → **Open Recent**(또는 **Open Folder**)로 `문서/copilot-lab/room-practice`를 엽니다.
- 상태 표시줄 브랜치가 `main`인지 보고, 동기화 아이콘을 눌러 최신으로 맞춥니다.

!!! info "XSS가 뭔가요?"
    XSS(Cross-Site Scripting, 사이트 간 스크립트)는 사용자가 입력한 글자에 스크립트가 섞여 있을 때, 웹페이지가 그것을 글자가 아니라 **실행할 코드**로 처리해서 생기는 보안 문제입니다. 현황판은 누구나 회의 제목을 적을 수 있고, 회의실 앞 태블릿과 사외에서도 열립니다. 제목 하나로 보는 사람의 브라우저에서 무엇이든 실행될 수 있다는 뜻입니다.

## STEP 1. 문제 재현하기

1. 터미널에서 회의 제목에 스크립트를 넣어 예약합니다. 따옴표를 그대로 복사합니다.

    ```text
    python -m booking add --room R1 --title "<script>alert('예약')</script>" --date 2026-11-13 --start 10:00 --end 11:00 --booker 홍길동 --attendees 2
    ```

    ```text
    [예약 완료] #6 2026-11-13 10:00~11:00 R1 <script>alert('예약')</script>
    ```

2. 현황판을 만듭니다.

    ```text
    python build_site.py
    ```

3. 탐색기에서 `site/index.html` 오른쪽 클릭 → **Reveal in File Explorer**(Mac은 **Reveal in Finder**) → `index.html`을 더블클릭해 브라우저로 엽니다.

확인: 브라우저에 **"예약"이라는 알림창**이 뜹니다. 이것이 보안 문제가 재현된 것입니다. 알림창의 **확인**을 누릅니다.

!!! warning "알림창은 가장 순한 예입니다"
    지금은 알림창만 띄웠지만, 같은 자리에 다른 스크립트를 넣으면 화면을 바꾸거나 다른 사이트로 보내는 일도 할 수 있습니다. 실습 밖의 서비스에서는 절대 시도하지 않습니다.

## STEP 2. Copilot에게 보안 검토 맡기기

1. Chat **+**(**New Chat**) → Session Target **Copilot**, Agent **Ask**를 고릅니다.
2. **+**(**Add Context**) → **Files & Folders**로 `build_site.py`를 추가합니다.
3. Chat에 붙여 넣기

    ```text
    build_site.py를 보안 관점에서 검토해 주세요.
    이 현황판은 회의실 앞 태블릿과 사외에서도 열리는 웹페이지입니다.
    - 보안 위험을 위험도 순서로 알려 주세요.
    - 각 위험마다 근거가 되는 코드 줄과, 어떻게 악용될 수 있는지 한 줄씩 써 주세요.
    - 고치는 방법을 제안해 주세요. 아직 코드는 바꾸지 마세요.
    ```

4. 답을 읽고 아래를 찾습니다.
    - 사용자가 입력한 값(제목 등)을 HTML에 그대로 넣는다는 지적 (XSS)
    - 고치는 방법으로 Python 표준 라이브러리 `html.escape()`
    - 연락처를 공개한다는 개인정보 지적이 함께 나올 수도 있습니다

확인: 답에 XSS와 `html.escape()`가 있습니다.

## STEP 3. Copilot 제안도 검토하기

Copilot의 보안 검토도 **검토 대상**입니다. 제안이 회의 제목(`title`)만 말하고 끝날 때가 많습니다.

1. `build_site.py`에서 `rows +=`로 시작하는 부분을 엽니다.
2. `{r.` 로 시작하는 값을 모두 찾습니다. 사람이 입력할 수 있는 값은 아래 4개입니다.

    | 값 | 어디서 들어오나 | escape 필요 |
    |---|---|---|
    | `r.title` | `--title` | 예 |
    | `r.booker` | `--booker` | 예 |
    | `r.team` | `--team` | 예 |
    | `r.phone` | `--phone` | 예 |

3. Copilot 제안이 4개를 모두 다루는지 봅니다. 빠진 것이 있으면 메모합니다.

확인: 제안에서 빠진 필드를 찾았거나, 4개를 모두 다룬다는 것을 확인했습니다.

## STEP 4. Agent로 고치기

1. Agent 선택기를 **Agent**로 바꿉니다.
2. Chat에 붙여 넣기

    ```text
    build_site.py의 XSS를 고쳐 주세요.
    - Python 표준 라이브러리 html.escape()를 써 주세요.
    - 사용자가 입력하는 값 title, booker, team, phone을 모두 escape해 주세요.
    - 화면 모양과 다른 동작은 바꾸지 마세요.
    ```

3. 승인 요청을 읽고 승인합니다.
4. diff를 읽고 `html.escape`가 4곳에 모두 들어갔는지 봅니다.

확인: `build_site.py`에 `import html`(또는 비슷한 import)과 escape 4곳이 있습니다.

## STEP 5. 다시 열어 확인하기

1. 현황판을 다시 만듭니다.

    ```text
    python build_site.py
    ```

2. 브라우저의 현황판 탭에서 새로 고침합니다. Windows ++f5++, Mac ++cmd+r++

확인: 알림창이 뜨지 않고, 회의 칸에 `<script>alert('예약')</script>`가 **글자 그대로** 보입니다.

!!! tip "브라우저 개발자 도구로 더 확인하려면 (선택)"
    페이지에서 오른쪽 클릭 → 페이지 소스 보기를 열면 `&lt;script&gt;`처럼 바뀌어 있습니다. `<`가 `&lt;`로 바뀌어 브라우저가 코드가 아닌 글자로 그립니다.

## STEP 6. 테스트 추가하고 정리하기

1. Chat에 붙여 넣기

    ```text
    /tests build_site.py의 XSS 방지를 확인하는 테스트를 tests/ 폴더에 추가해 주세요.
    - 제목과 예약자에 <script>가 들어간 예약으로 HTML을 만들었을 때 결과에 <script>가 없고 &lt;script&gt;가 있어야 합니다.
    - 실제 data/reservations.json과 site/ 폴더는 건드리지 않게 해 주세요.
    - 테스트를 쉽게 하려고 build_site.py를 바꿔야 하면 무엇을 왜 바꾸는지 먼저 설명해 주세요.
    ```

2. 승인 요청을 읽고 승인합니다. `build_site.py` 구조를 바꾸자고 하면 설명을 읽고 동작이 같은지 판단합니다.
3. 터미널에서 실행합니다.

    ```text
    python -m pytest
    ```

4. 실습용 예약을 되돌립니다. **소스 제어**에서 `data/reservations.json` → **Discard Changes**
5. 바뀐 파일이 `build_site.py`와 테스트 파일뿐인지 보고 커밋합니다.

    ```text
    현황판 XSS 방지 (html.escape)
    ```

6. **Sync Changes**로 올립니다.

확인: 테스트가 모두 통과하고, 커밋이 GitHub에 올라갔고, `data/reservations.json`은 바뀌지 않았습니다.

!!! note "팀 리포지토리는요?"
    팀 리포지토리의 `build_site.py`에도 같은 문제가 남아 있을 수 있습니다. 6-3에서 CR-001을 구현하며 escape했는지 확인해 보세요. 고쳐야 하면 같은 흐름(이슈 → 브랜치 → PR)으로 반영합니다.

## 다 됐는지 확인

- [ ] 제목에 스크립트를 넣어 알림창이 뜨는 것을 재현했다
- [ ] Copilot Ask로 보안 검토를 받고 XSS와 `html.escape()`를 확인했다
- [ ] Copilot 제안이 `title` 외에 `booker`, `team`, `phone`도 다루는지 검토했다
- [ ] 고친 뒤 스크립트가 글자로만 보였다
- [ ] XSS 테스트를 추가했고 모두 통과한다
- [ ] 데이터 변경을 되돌리고 커밋했다

## 막히면

??? failure "알림창이 처음부터 안 떠요"
    `python build_site.py`를 예약을 넣은 **뒤에** 실행했는지 봅니다. 또 브라우저에서 예전 `index.html`을 보고 있을 수 있으니 새로 고침합니다.

??? failure "터미널에서 add 명령이 따옴표 오류로 실패해요"
    명령 전체를 그대로 복사했는지 봅니다. 제목은 큰따옴표 `"`로 감싸고, 안의 `'예약'`은 작은따옴표입니다.

??? failure "고쳤는데도 알림창이 떠요"
    `python build_site.py`를 다시 실행하지 않았거나, 새로 고침하지 않은 것입니다. 그래도 뜨면 `title`에 escape가 실제로 들어갔는지 diff를 다시 봅니다.

??? failure "테스트가 실제 data 파일을 바꿔 버렸어요"
    **소스 제어**에서 `data/reservations.json`을 **Discard Changes**로 되돌리고, Chat에 "테스트는 임시 데이터만 써야 합니다. 실제 data 파일을 건드리지 않게 고쳐 주세요"라고 요청합니다.

??? failure "Copilot이 escape 대신 직접 replace로 바꿨어요"
    `replace("<", "&lt;")`처럼 직접 바꾸면 빠뜨리는 글자가 생기기 쉽습니다. "표준 라이브러리 html.escape()로 바꿔 주세요"라고 요청합니다.
