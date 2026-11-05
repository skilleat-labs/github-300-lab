# Starter 파일 보기

템플릿 `skilleat-labs/meeting-room-starter`에 들어 있는 파일입니다. 실습 중에 원래 모습을 확인하고 싶을 때 봅니다. 아래 코드는 Starter 원본 그대로입니다.

## 폴더 구조

```text
meeting-room-starter/
├── README.md                    실행, 테스트 방법
├── pyproject.toml               pytest 설정
├── requirements-dev.txt         pytest
├── .gitignore                   __pycache__, .venv, .pytest_cache, site/
├── .vscode/settings.json        VS Code에서 pytest 켬
├── .github/workflows/ci.yml     자동 테스트 "테스트" (job test)
├── docs/
│   ├── 00_현업요청.md            총무팀 최수연 대리의 요청
│   ├── 01_킥오프_회의록.md       결정한 것 4개, 결정하지 못한 것 3개
│   └── 02_현행_업무.md           엑셀 흐름, 회의실 표, 운영 규칙
├── data/
│   ├── rooms.json               회의실 4개 (R1~R4)
│   └── reservations.json        예약 5건
├── booking/
│   ├── models.py                Room, Reservation
│   ├── store.py                 JSON 읽기, 쓰기
│   ├── rules.py                 예약 검사 validate()
│   ├── service.py               reserve(), list_reservations()
│   ├── report.py                이용률 보고서
│   └── __main__.py              python -m booking 명령
├── build_site.py                예약 현황판 site/index.html 만들기
└── tests/
    └── test_rules.py            테스트 4개
```

## 명령 한눈에 보기

| 명령 | 하는 일 |
|---|---|
| `python -m pytest` | 테스트 실행 (처음엔 4 passed) |
| `python -m booking rooms` | 회의실 목록 |
| `python -m booking list --date 2026-11-10` | 그 날짜 예약 목록 |
| `python -m booking add --room R1 --title 회의 --date 2026-11-10 --start 10:00 --end 11:00 --booker 홍길동 --attendees 2` | 예약하기. `data/reservations.json`이 바뀝니다 |
| `python -m booking report` | 회의실 이용률 보고서 |
| `python build_site.py` | 현황판 `site/index.html` 만들기 |

!!! tip "데이터 되돌리기"
    `add`로 바뀐 `data/reservations.json`은 VS Code **소스 제어**에서 **Discard Changes**로 되돌립니다. Mac에서 `python`이 안 되면 `python3`로 실행합니다.

## booking/rules.py

예약 검사 규칙입니다. 2교시 18시 버그(S4), 4교시 겹침 검사(S1), 5교시 정원 검사(S2)가 모두 이 파일의 `validate()`에서 일어납니다. TODO 주석과 `end >=` 비교를 찾아보세요.

```python
--8<-- "starter/booking/rules.py"
```

## booking/service.py

예약하기와 목록 보기입니다. 취소(`cancel`)는 아직 없습니다. 5교시 S3에서 추가합니다.

```python
--8<-- "starter/booking/service.py"
```

## build_site.py

예약 현황판을 만드는 스크립트입니다. 제목과 예약자를 그대로 HTML에 넣고(7-1 XSS), 연락처를 그대로 보여 줍니다(6-3 CR-001).

```python
--8<-- "starter/build_site.py"
```

## .github/workflows/ci.yml

자동 테스트 워크플로 "테스트"입니다. PR을 열거나 main에 push하면 Python 3.12로 테스트를 실행합니다.

```yaml
--8<-- "starter/.github/workflows/ci.yml"
```

## docs/01_킥오프_회의록.md

5교시 PO, BA가 근거로 쓰는 회의록입니다. "결정하지 못한 것" 3개를 Copilot이 마음대로 정하지 않는지 확인합니다.

```markdown
--8<-- "starter/docs/01_킥오프_회의록.md"
```
