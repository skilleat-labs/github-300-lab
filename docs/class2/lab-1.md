# 실습 2-1. 인라인 제안과 다음 편집 제안

!!! abstract "이 실습에서 할 일"
    - 새 파일 `booking/format.py`에 **주석으로 의도를 쓰고** 인라인 제안으로 함수 2개를 받습니다.
    - 제안을 받아들이기 전에 다른 제안도 비교해 봅니다.
    - 변수 이름 하나를 바꿔 **다음 편집 제안(NES)**이 관련 줄을 이어서 고쳐 주는 것을 체험합니다.

    **예상 시간** 약 9분. 이 실습은 **크레딧을 쓰지 않습니다.**

## 준비

- `room-practice`가 VS Code에 열려 있어야 합니다.
- 이 실습은 연습용 파일을 새로 만들고, 끝나면 지웁니다. `booking/report.py` 같은 기존 파일은 건드리지 않습니다.

!!! tip "인라인 제안과 NES는 무제한"
    Copilot Pro에서 **인라인 제안**(코드 완성)과 **다음 편집 제안**(NES, Next Edit Suggestions)은 크레딧을 쓰지 않고 무제한입니다. 마음껏 받아 보고 버려도 됩니다.

## STEP 1. 연습 파일 만들기

1. 왼쪽 탐색기에서 `booking` 폴더에 마우스를 올립니다.
2. 폴더 이름 오른쪽에 나타나는 **New File**(새 파일) 아이콘을 클릭합니다. `booking` 폴더를 마우스 오른쪽 버튼으로 클릭해 **New File...**을 골라도 됩니다.
3. 파일 이름에 `format.py`를 입력하고 Enter를 누릅니다.

    ```text
    format.py
    ```

확인: 탐색기의 `booking` 폴더 안에 `format.py`가 생기고, 빈 편집기가 열렸습니다.

## STEP 2. 주석으로 의도를 쓰고 첫 번째 함수 받기

인라인 제안은 **주변 글을 보고** 다음 내용을 추측합니다. 무엇을 원하는지 주석으로 먼저 쓰면 제안이 정확해집니다.

1. `format.py` 첫 줄에 아래 주석을 입력합니다. 한 줄씩 직접 쳐도 되고 붙여 넣어도 됩니다.

    ```python
    # 예약 한 건을 사람이 읽기 좋은 한 줄 문자열로 만든다.
    # 예: "2026-11-10 10:00~11:00 R1 주간 업무 회의 (김민수, 4명)"
    # 예약 r에는 date, start, end, room_id, title, booker, attendees가 있다.
    ```

2. 마지막 주석 끝에서 Enter를 누릅니다.
3. `def format_reservation(r):`를 입력하고 Enter를 누른 뒤 1~2초 기다립니다.
4. 회색 글씨로 함수 본문 제안이 나타나면 읽어 봅니다.
5. 내용이 예시 문장과 비슷하면 **Tab**을 눌러 받아들입니다.

확인: `format_reservation` 함수에 `return`으로 시작하는 문자열 만드는 줄이 생겼습니다. 날짜, 시간, 회의실, 제목, 예약자, 인원이 모두 들어가 있으면 됩니다.

## STEP 3. 다른 제안 비교해 보기

제안이 하나만 있는 것은 아닙니다.

1. 함수 아래에 빈 줄을 두 개 만듭니다.
2. 아래 주석을 입력하고 Enter를 누릅니다.

    ```python
    # 회의실 목록 rooms에서 room_id에 해당하는 회의실 이름을 찾는다. 없으면 "알 수 없는 회의실"을 돌려준다.
    ```

3. 회색 제안이 나오면 **바로 Tab을 누르지 말고** 제안 위에 마우스를 올립니다.
4. 작은 도구 막대가 나타나면, 그 안의 화살표로 다른 제안을 넘겨 봅니다.
5. "없으면 알 수 없는 회의실"까지 처리하는 제안을 골라 **Tab**을 누릅니다.

확인: `rooms`와 `room_id`를 받아 이름을 돌려주는 함수가 생겼고, 못 찾았을 때 `"알 수 없는 회의실"`을 돌려주는 줄이 있습니다.

!!! note "화면이 조금 다를 수 있어요"
    제안이 하나뿐이면 도구 막대에 넘길 화살표가 없을 수 있습니다. 그럴 때는 그대로 받아들이고 다음 STEP으로 넘어갑니다.

!!! warning "Tab 누르기 전에 읽기"
    인라인 제안은 빠른 대신 **검토 없이 들어가기 쉽습니다.** 특히 "없으면 ..." 같은 예외 처리가 빠진 제안이 자주 나옵니다. 받아들이기 전에 주석에 적은 조건이 모두 들어 있는지 눈으로 확인합니다.

## STEP 4. 받은 함수 직접 확인하기

받은 코드가 맞는지 사람이 확인합니다.

1. 터미널을 엽니다(Windows ``Ctrl+` ``, Mac ``⌃` ``).
2. 아래 명령을 한 줄로 붙여 넣고 Enter를 누릅니다.

    === "Windows"

        ```bash
        python -c "from booking.store import load_reservations; from booking.format import format_reservation; print(format_reservation(load_reservations()[0]))"
        ```

    === "Mac"

        ```bash
        python3 -c "from booking.store import load_reservations; from booking.format import format_reservation; print(format_reservation(load_reservations()[0]))"
        ```

확인: `2026-11-10 10:00~11:00 R1 주간 업무 회의 (김민수, 4명)`과 비슷한 한 줄이 나옵니다. 오류가 나면 Copilot이 만든 코드에 문제가 있는 것입니다. 터미널의 오류 줄을 복사해 Chat(Ask)에 붙여 넣고 "원인과 고치는 방법을 알려 주세요"라고 묻습니다.

!!! tip "함수 이름이 다르면"
    Copilot이 함수 이름을 바꿔 제안했다면 명령의 `format_reservation`을 그 이름으로 바꿔 실행합니다.

## STEP 5. 다음 편집 제안(NES) 체험하기

**다음 편집 제안**은 내가 방금 한 수정을 보고 "이것도 같이 고쳐야 하지 않나요?"라고 다음 수정 위치와 내용을 제안하는 기능입니다.

1. `format_reservation(r)` 함수의 첫 줄에서 매개변수 이름 `r`을 더블클릭해 선택합니다.
2. `reservation`으로 바꿔 입력합니다. 함수 첫 줄이 `def format_reservation(reservation):`가 됩니다.
3. 잠시 기다리면 함수 본문의 `r.date`, `r.start` 같은 줄 근처에 수정 제안 표시가 나타납니다.
4. **Tab**을 누르면 제안 위치로 이동하고, 한 번 더 **Tab**을 누르면 제안을 받아들입니다.
5. 본문의 `r.`이 모두 `reservation.`으로 바뀔 때까지 반복합니다.

확인: 함수 본문에 `r.`이 남아 있지 않고, 모두 `reservation.`으로 바뀌었습니다. STEP 4의 명령을 다시 실행해도 같은 결과가 나옵니다.

!!! note "화면이 조금 다를 수 있어요"
    NES의 표시 모양(화살표, 강조 등)은 VS Code 버전에 따라 다릅니다. 제안이 나오지 않으면 나머지 `r.`을 직접 고칩니다. 실습 목표는 "이런 기능이 있다"를 경험하는 것입니다.

## STEP 6. 연습 파일 지우기

이 파일은 연습용입니다. **커밋하지 않고 지웁니다.**

1. 탐색기에서 `booking/format.py`를 마우스 오른쪽 버튼으로 클릭합니다.
2. **Delete**(삭제)를 고르고, 확인 창에서 휴지통으로 옮기는 버튼을 누릅니다.
3. 왼쪽 활동 막대의 **소스 제어** 아이콘(Windows `Ctrl+Shift+G`, Mac `⌃⇧G`)을 클릭합니다.

확인: 소스 제어의 **Changes** 목록이 비어 있습니다.

## 다 됐는지 확인

- [ ] 주석으로 의도를 쓰고 인라인 제안으로 함수 2개를 받았습니다.
- [ ] 제안 위에 마우스를 올려 다른 제안이 있는지 봤습니다.
- [ ] 받은 함수를 터미널에서 직접 실행해 확인했습니다.
- [ ] 변수 이름을 바꾼 뒤 NES 제안을 **Tab**으로 받아 봤습니다.
- [ ] `format.py`를 지웠고, **Changes** 목록이 비어 있습니다.
- [ ] Copilot status dashboard의 사용량이 이 실습 동안 늘지 않은 것을 확인했습니다.

## 막히면

!!! tip "먼저 Copilot과 함께 해결합니다"
    오류 메시지나 막힌 상황을 Chat(Ask)에 붙여 넣고 원인과 해결 순서를 묻습니다. 아래는 자주 막히는 경우입니다. 묻는 방법은 [막혔을 때](../setup/3-troubleshooting.md#copilot)에 있습니다.

??? failure "회색 제안이 나오지 않습니다"
    `def format_reservation(r):` 다음 줄에서 띄어쓰기 4칸을 넣고 `return`까지 직접 입력해 봅니다. 그래도 안 나오면 상태 표시줄 Copilot 아이콘에서 로그인 상태를 확인합니다.

??? failure "제안이 주석 예시와 다르게 나옵니다"
    정상입니다. Copilot 제안은 매번 다릅니다. 받아들인 뒤 고쳐도 되고, **Esc**로 거절하고 주석을 더 구체적으로 써서 다시 받아도 됩니다.

??? failure "STEP 4에서 No module named booking 오류가 납니다"
    터미널의 현재 폴더가 `room-practice`가 아닙니다. **File** → **Open Folder**로 `room-practice`를 다시 열고 새 터미널에서 실행합니다. Mac은 `python3`으로 실행합니다.

??? failure "STEP 4에서 AttributeError가 납니다"
    Copilot이 없는 속성 이름(예: `r.room`)을 썼을 수 있습니다. 예약에 있는 속성은 `id, room_id, title, booker, team, phone, date, start, end, attendees`입니다. 틀린 이름을 고칩니다. 바로 이런 것을 잡는 것이 검토입니다.

??? failure "NES 제안이 나오지 않습니다"
    매개변수 이름을 바꾼 직후 잠시 기다려 봅니다. 그래도 안 나오면 직접 고치고 넘어갑니다. NES는 바꾼 내용에서 다음 수정이 뚜렷할 때 주로 나옵니다.
