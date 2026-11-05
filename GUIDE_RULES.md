# GH-300 실습 가이드 작성 규칙

GitHub Copilot(GH-300) 1일 과정의 MkDocs 교안 겸 실습 가이드다. 수강생은 **PM, BA, IT기획, 운영 담당자 중심 21명, 일부 개발자**다. 코딩 교육이 아니라 **Copilot을 일에 쓰는 법**을 배운다. 코드는 Copilot이 쓰고, 수강생은 요청하고, 검토하고, 검증한다. 클릭 하나까지 적는다. 수업은 강사 화면(PPT)과 이 가이드를 나란히 보며 진행한다.

## 1. 원천 자료 (이것만 근거로 쓴다)

| 자료 | 경로 | 쓰는 곳 |
|---|---|---|
| 공식 문서 사실 정리 | `FACTS.md` | **모든 기술 내용.** 여기 없는 기능, 메뉴 이름, 단축키, 숫자는 쓰지 않는다 |
| 이론 장표 빌드 스크립트 | `../../ppt-template/build_gh300_theory.js` | 각 교시 `index.md`의 교안 |
| Starter 원본 | `starter/` | 파일 이름, 코드, 실행 결과 |

화면 이름이 FACTS.md에서 "(검색 요약)"인 것은 가이드에 `!!! note "화면이 조금 다를 수 있어요"`를 붙인다.

## 2. 환경

- 각자 PC에 설치한 **VS Code**(1.116 이상, Copilot Chat 내장), **Git**, **Python 3.12 이상**.
- 개인 GitHub 계정 + **Copilot Pro 라이선스**(회사가 지급). 월 AI Credits 1,500. 인라인 제안과 NES는 크레딧을 쓰지 않고, Chat, 에이전트, 코드 리뷰, 클라우드 에이전트는 크레딧을 쓴다. **모델은 Auto**를 기본으로 쓰게 한다(10% 할인, 적당한 모델 자동 선택).
- Chat 기본 설정: Session Target **Copilot**, Agent **Agent** 또는 **Ask**, 모델 **Auto**, Permissions **Manual**. 프롬프트 파일을 쓸 때만 **Local**.

## 3. 과정 구성 (확정)

- 09:00~17:00, 점심 12:00~13:15, 7교시. 1~6교시 50분, 7교시 45분, 쉬는 시간 10분. **모든 교시에 실습.** 이론 약 35%, 실습 약 65%.
- 오전(1~4교시 앞부분): **개인 실습**, 개인 리포지토리 `room-practice`.
- 4교시 끝: 팀 구성. 5~7교시: **팀 실습**, 팀 리포지토리 `room-booking-team<번호>`. 역할 PO, PM, BA, 개발자를 맡지만 **모두가 Copilot으로 같은 과제(스토리 하나씩 구현)를 한다.** 따로 심화 과제는 없다.
- 오전 문서 작업(사용자 스토리)은 3교시에 **짧게(12분)**만 한다. 나머지는 Copilot으로 실제 코드를 바꾸고 돌려 본다.
- 하루의 끝: 팀 리포지토리에 **CI(테스트 자동 실행) + CD(현황판 자동 배포, GitHub Pages)** 가 구성되고, 팀이 만든 기능이 들어간 회의실 예약 현황판이 웹 주소로 열린다.

| 교시 | 주제 | 교육 목표 | 실습 페이지 |
|---|---|---|---|
| 1 | GitHub 리마인드와 Copilot 시작 | GitHub 협업 흐름을 다시 떠올리고, VS Code에서 Copilot을 켜고 안전하게 설정할 수 있다 | 1-1 환경 점검과 Copilot 설정, 1-2 템플릿으로 내 리포지토리 만들고 VS Code로 가져오기, 1-3 Copilot에게 첫 질문 |
| 2 | Copilot 기본기 | 인라인 제안, 인라인 채팅, Chat의 역할(Ask, Agent)을 구분해 쓰고, 결과를 검증해 버그를 고칠 수 있다 | 2-1 인라인 제안과 다음 편집 제안, 2-2 코드 설명 듣기(/explain, 인라인 채팅), 2-3 버그 잡기(/fix)와 커밋 |
| 3 | 프롬프트와 맥락 설계 | 좋은 프롬프트 구조로 요구사항을 정리하고, 지침 파일과 프롬프트 파일로 Copilot의 답을 일관되게 만들 수 있다 | 3-1 회의록에서 사용자 스토리 뽑기(zero-shot과 few-shot), 3-2 지침 파일 만들기, 3-3 프롬프트 파일 만들기 |
| 4 | 에이전트로 기능 만들기 | Plan과 Agent로 기능을 구현하고, 변경을 검토하고 테스트로 검증해 PR로 반영할 수 있다 | 4-1 브랜치와 계획(/plan), 4-2 에이전트로 구현하고 테스트, 4-3 PR과 CI, 4-4 팀 구성 |
| 5 | 팀 실습 ① 요구에서 구현까지 | 역할에 따라 Copilot으로 요구를 정리하고 나눠 각자 기능을 구현할 수 있다 | 미션 5-1 요구 정리와 분배, 미션 5-2 스토리 구현 |
| 6 | 팀 실습 ② 검토와 CI/CD | Copilot 코드 리뷰와 사람 검토로 변경을 반영하고, Copilot으로 배포 워크플로를 만들어 현황판을 자동 배포할 수 있다 | 미션 6-1 PR과 리뷰, 미션 6-2 Copilot으로 배포 자동화(Pages), 미션 6-3 변경 요청 처리 |
| 7 | 책임 있는 사용과 보안 (45분) | Copilot 결과의 보안 위험을 찾아 고치고, 클라우드 에이전트에 일을 맡기며, 팀의 사용 규칙을 정할 수 있다 | 7-1 클라우드 에이전트에 이슈 맡기기(먼저 맡기고 넘어감), 7-2 보안 검토(XSS), 7-3 팀 사용 규칙, Copilot PR 확인, 오늘의 정리 |

### 교시별 진행 시간

| 교시 | 이론 | 실습 |
|---|---|---|
| 1 | 25분 (GitHub 리마인드 15분 + Copilot 소개 10분) | 25분 |
| 2 | 15분 | 35분 |
| 3 | 15분 | 35분 |
| 4 | 15분 | 4-1 7분, 4-2 11분, 4-3 7분, 팀 구성 10분 |
| 5 | 10분 | 40분 |
| 6 | 15분 | 6-1 14분, 6-2 11분, 6-3 10분 |
| 7 | 15분 | 7-1 5분, 7-2 12분, 7-3 8분, 정리 5분 |

## 4. 이름 규칙 (모든 페이지 공통, 바꾸지 않는다)

| 대상 | 이름 |
|---|---|
| Starter 템플릿 | `skilleat-labs/meeting-room-starter` (주소 `https://github.com/skilleat-labs/meeting-room-starter`, 강사가 수업 전에 만듦) |
| 개인 리포지토리 | `room-practice` (Public. Pages를 쓰려면 무료 계정은 Public이어야 함) |
| 팀 리포지토리 | `room-booking-team1` ~ `room-booking-team6` (PO가 템플릿으로 만듦, Public) |
| 개인 실습 폴더 | 각자 PC의 `문서/copilot-lab/room-practice` (VS Code Clone 위치) |
| 개인 브랜치 | 2-3은 main에 바로 커밋. 4교시 `overlap-check` |
| 팀 브랜치 | `story-<이슈번호>` 예 `story-3`, 6-2 `add-pages`, 6-3 `cr-001`, 7-3 `team-rules` |
| 팀 라벨 | `스토리`, `변경요청` |
| 지침 파일 | `.github/copilot-instructions.md` |
| 프롬프트 파일 | `.github/prompts/story.prompt.md` (이름 `/story`) |
| 사용자 스토리 문서 | `docs/03_사용자스토리.md` (3-1) |
| 배포 워크플로 | `.github/workflows/pages.yml` (이름 "현황판 배포", 6-2에서 Copilot으로 만듦) |
| 테스트 워크플로 | `.github/workflows/ci.yml` (이름 "테스트", job `test`, Starter에 들어 있음) |
| 변경 요청 | CR-001 "현황판이 회의실 앞 태블릿과 사외에서도 보입니다. 연락처는 빼고, 예약자는 성과 '○○'로만 보여 주세요. 예: 김○○" |

### 팀 백로그 (5교시, 이슈 4개. 3인 팀은 S4를 뺀다)

| 번호 | 스토리 | 바꿀 곳 | 완료 기준(인수 조건 예) |
|---|---|---|---|
| S1 | 같은 회의실, 같은 날짜에 시간이 겹치는 예약을 막는다 | `booking/rules.py` | 10:00~11:00이 있으면 10:30~11:30은 "이미 예약된 시간"으로 실패. 11:00~12:00은 성공(맞닿음은 겹침 아님) |
| S2 | 회의실 정원을 넘는 예약을 막는다 | `booking/rules.py` | 소회의실 A(정원 4)에 5명이면 "정원을 넘었습니다"로 실패 |
| S3 | 예약을 취소할 수 있다 | `booking/service.py`, `booking/__main__.py` | `python -m booking cancel --id 3`이면 #3이 목록에서 사라지고 "[취소 완료]" 출력. 없는 번호면 "[취소 실패] 없는 예약 번호입니다" |
| S4 | 18:00에 끝나는 예약이 되게 고친다 | `booking/rules.py` | 17:00~18:00 성공, 17:30~18:30 실패 |

- S1과 S2와 S4는 같은 파일을 고쳐 **병합 충돌**이 날 수 있다. 실제 일처럼 두고, 6-1에서 충돌 해결(VS Code 병합 편집기 또는 github.com Resolve conflicts) 방법을 적는다.
- 2교시에 개인 리포지토리에서 S4(18시 버그)를, 4교시에 S1(겹침)을 혼자 해 봤다. 팀에서는 같은 일을 역할극 흐름으로 다시 하는 것이라 막히지 않는다.

## 5. Starter 내용 (`starter/`가 원본, 실행 결과는 실제로 돌려 확인한 것)

```
README.md                     실행, 테스트 방법
pyproject.toml                pytest 설정 (pythonpath ".", testpaths "tests")
requirements-dev.txt          pytest
.gitignore                    __pycache__, .venv, .pytest_cache, site/
.vscode/settings.json         pytest 켬
.github/workflows/ci.yml      "테스트": PR과 main push 때 python 3.12로 pytest. job 이름 test
docs/00_현업요청.md            총무팀 최수연 대리 요청. 불편 5가지, 바라는 점 5가지
docs/01_킥오프_회의록.md       결정 4개(겹침, 정원, 현황판, 취소), 결정 못 한 것 3개
                                (최대 예약 시간 2시간 vs 4시간, 노쇼 자동 취소 10분 vs 15분, 현황판 연락처 공개)
                                비범위: 메신저 알림, 로그인
docs/02_현행_업무.md           엑셀 흐름, 회의실 표, 운영 규칙(09:00~18:00, 18:00에 끝나는 예약 가능, 30분 단위)
data/rooms.json                R1 소회의실 A 4명 3층, R2 소회의실 B 4명 3층, R3 중회의실 8명 5층, R4 대회의실 16명 7층
data/reservations.json         예약 5건 (#1 11/10 10:00~11:00 R1 주간 업무 회의 김민수 4명 ... #5 11/12 16:00~17:30 R1 디자인 리뷰)
booking/models.py              Room, Reservation (id, room_id, title, booker, team, phone, date, start, end, attendees)
booking/store.py               JSON 읽기, 쓰기, next_id
booking/rules.py               validate(): 없는 회의실, 시작>=끝, 운영 시간, 30분 단위.
                                버그: end >= 18:00이면 실패 (18:00 종료가 막힘)
                                빠진 것: "# TODO: 같은 회의실, 같은 날짜에 시간이 겹치는 예약은 막아야 한다 (현업 요청 1번)", 정원 검사
booking/service.py             reserve(), list_reservations(). cancel 없음
booking/report.py              이용률 보고서. 중첩 if, 한 글자 변수(t, c, a, b, lv). 리팩터링 재료
booking/__main__.py            python -m booking list [--date], add, rooms, report
build_site.py                  data → site/index.html 현황판. 함정: 제목, 예약자를 이스케이프하지 않음(XSS), 연락처를 그대로 공개(개인정보)
tests/test_rules.py            테스트 4개 (정상, 없는 회의실, 끝<시작, 운영 시간 전). 모두 통과
```

실제 실행 결과 (가이드에 그대로 쓴다):

```text
$ python -m pytest
....                                                                     [100%]
4 passed

$ python -m booking rooms
R1 소회의실 A (4명, 3층)
R2 소회의실 B (4명, 3층)
R3 중회의실 (8명, 5층)
R4 대회의실 (16명, 7층)

$ python -m booking list --date 2026-11-10
#1 2026-11-10 10:00~11:00 R1 주간 업무 회의 (김민수, 4명)
#2 2026-11-10 13:00~15:00 R3 신규 서비스 킥오프 (이지은, 7명)

$ python -m booking add --room R2 --title 마감회의 --date 2026-11-10 --start 17:00 --end 18:00 --booker 홍길동 --attendees 2
[예약 실패]
 - 운영 시간(09:00~18:00) 밖입니다.

$ python -m booking add --room R1 --title 겹침 --date 2026-11-10 --start 10:30 --end 11:30 --booker 홍길동 --attendees 2
[예약 완료] #6 2026-11-10 10:30~11:30 R1 겹침        ← 겹치는데 예약됨 (S1 대상)

$ python build_site.py
[완료] site/index.html 에 예약 5건을 썼습니다.
```

- Windows에서는 `python`, Mac에서는 `python3`일 수 있다. 가이드는 `python`으로 쓰고 "Mac에서 안 되면 python3"을 1-2에 한 번 안내한다.
- 실습 중 `add`로 데이터가 바뀐다. 되돌리려면 VS Code 소스 제어에서 `data/reservations.json` 변경을 **Discard Changes**.
- 참고 정답(강사용): 18시 버그는 `end >= to_minutes(CLOSE_TIME)`를 `end > ...`로. 겹침은 같은 room_id, 같은 date, id가 다른 예약 중 `start < 기존end and 기존start < end`. XSS는 `html.escape()`. 이 정답으로 테스트 8개가 통과하는 것을 확인했다.

## 6. 문체

- 존댓말 "~합니다/~해요" 섞지 않고 **"~합니다"** 기본, 팁은 "~해요" 허용. 한 문장에 한 동작.
- 버튼, 메뉴 이름은 화면의 영어 그대로 **굵게**. 처음 나올 때 괄호로 뜻.
- 프롬프트는 복사할 수 있게 ```` ```text ```` 블록에 넣고, 위에 "Chat에 붙여 넣기" 한 줄.
- 각 실습 페이지 구조: 제목 → `!!! abstract "이 실습에서 할 일"` (목표 2~3줄, 예상 시간) → STEP 1, 2, ... (각 STEP 끝에 "확인:" 한 줄) → `!!! tip`/`!!! warning` 필요한 곳 → 마지막에 "다 됐는지 확인" 체크리스트 → "막히면" (`??? failure "증상"` 접는 블록 3~6개).
- **Copilot 답은 매번 달라진다**는 것을 전제로 쓴다. "Copilot이 이렇게 답합니다"라고 단정하지 말고 "이런 내용이 나오면 됩니다"와 확인 기준을 준다.
- 크레딧: 코드 리뷰(1회 약 150크레딧, Balanced 기준)와 클라우드 에이전트는 **팀당 정해진 횟수만** 한다고 적는다.
- 코드 검토 기준은 특정 문자열이 아니라 동작과 테스트로 쓴다. 테스트 개수로 합격을 정하지 않는다.
- 금지: `@workspace`, Edit 모드, premium request, coding agent(→ 클라우드 에이전트), Copilot 확장 설치 안내, Spark.
- 가운뎃점(·) 쓰지 않는다. 쉼표로.
