# 실습 4-3. PR과 CI

!!! abstract "이 실습에서 할 일"
    - 브랜치 `overlap-check`를 GitHub에 올리고 PR(Pull Request, 병합 요청)을 엽니다.
    - PR 설명을 Copilot의 **Summary**로 만들고, 자동 테스트(CI) "테스트"가 초록 체크인지 확인합니다.
    - 혼자 쓰는 리포지토리이므로 직접 병합하고, VS Code의 main을 최신으로 맞춥니다.

**소요 시간** 약 9분  **실습 장소** VS Code와 github.com의 `room-practice`  **관련 교안** [4교시 교안](index.md)

## 준비

- 4-2에서 `overlap-check` 브랜치에 커밋했어야 합니다. 소스 제어 버튼이 **Publish Branch**로 보이면 준비된 것입니다.

!!! info "CI가 뭔가요?"
    CI(Continuous Integration, 지속적 통합)는 코드를 올릴 때마다 테스트를 자동으로 돌리는 것입니다. Starter에 `.github/workflows/ci.yml`이 이미 들어 있습니다. 이름은 **테스트**이고, PR을 열거나 main에 push하면 GitHub Actions가 Python 3.12로 `python -m pytest`를 실행합니다. 내 PC에서 통과한 테스트가 다른 컴퓨터에서도 통과하는지 확인하는 장치입니다.

## STEP 1. 브랜치를 GitHub에 올리기

1. 왼쪽 활동 막대의 **소스 제어** 아이콘을 클릭합니다.
2. 파란 **Publish Branch**(브랜치 게시) 버튼을 클릭합니다.
3. GitHub 로그인 확인 창이 뜨면 본인이 직접 허용합니다.
4. 오른쪽 아래에 "Create Pull Request" 같은 알림이 떠도 누르지 않고 닫습니다. PR은 github.com에서 엽니다.

확인: 상태 표시줄 브랜치 이름 옆에 구름 아이콘 대신 동기화 아이콘이 보이고, 소스 제어 버튼이 사라졌습니다.

!!! tip "이미 Publish한 브랜치에 커밋을 더 했다면"
    버튼이 **Sync Changes**(변경 동기화)로 바뀝니다. 그 버튼을 누르면 Push됩니다.

## STEP 2. github.com에서 PR 만들기

1. 브라우저에서 내 리포지토리를 엽니다.

    ```text
    https://github.com/<내아이디>/room-practice
    ```

2. 위쪽에 노란 띠 **overlap-check had recent pushes**가 보입니다. **Compare & pull request**(비교하고 PR 만들기)를 클릭합니다.
3. 띠가 없으면 **Pull requests** 탭 → **New pull request** → **compare**를 `overlap-check`로 고르고 **Create pull request**를 클릭합니다.
4. 위쪽이 `base: main` ← `compare: overlap-check`인지 봅니다.
5. 제목 칸에 입력합니다.

    ```text
    겹치는 예약 막기 (현업 요청 1번)
    ```

확인: PR 작성 화면에 제목이 들어가 있고, 아래에 바뀐 파일 2개(`rules.py`, `test_rules.py`)가 보입니다.

## STEP 3. Copilot으로 PR 설명 쓰기

1. 설명(Description) 칸 위쪽 도구 모음에서 Copilot 아이콘을 클릭합니다.
2. **Summary**(요약)를 클릭합니다.
3. 잠시 기다리면 설명 칸에 바뀐 내용 요약이 들어갑니다.
4. 요약을 읽고 사실과 다른 문장을 고칩니다. 예를 들어 "정원 검사도 추가했다"처럼 하지 않은 일이 적혀 있으면 지웁니다.
5. 맨 아래에 한 줄을 직접 덧붙입니다.

    ```text
    직접 확인: 10:30-11:30은 실패, 11:00-12:00(맞닿음)은 성공
    ```

6. 초록 **Create pull request**를 클릭합니다.

확인: PR이 열렸고, 설명에 Copilot 요약과 직접 확인 한 줄이 있습니다.

!!! note "화면이 조금 다를 수 있어요"
    PR 요약 메뉴의 위치와 이름은 공식 문서 검색 요약으로 확인한 것입니다. Copilot 아이콘이 안 보이면 PR을 먼저 만든 뒤 설명 편집(연필) 화면이나 댓글 칸의 도구 모음에서 찾습니다. Copilot Free 계정에서는 이 기능이 없습니다.

!!! warning "요약도 검토 대상입니다"
    Copilot이 쓴 요약은 그럴듯하지만 틀릴 수 있습니다. PR 설명은 리뷰하는 사람이 가장 먼저 읽는 글이라, 하지 않은 일이 적혀 있으면 리뷰가 엉뚱한 곳으로 갑니다.

## STEP 4. CI "테스트" 확인하기

1. PR 화면 아래쪽 검사 영역을 봅니다. **테스트 / test**가 노란 원(실행 중)으로 보입니다.
2. 1분쯤 기다립니다.
3. 초록 체크로 바뀌면 **Details**(자세히)를 클릭합니다.
4. 로그에서 `python -m pytest -v` 단계를 펼쳐 내가 추가한 테스트 이름이 `PASSED`로 보이는지 봅니다.
5. 브라우저 뒤로 가기로 PR 화면으로 돌아옵니다.

확인: PR 아래쪽에 **All checks have passed**(모든 검사 통과)와 초록 체크가 보입니다.

## STEP 5. 직접 병합하기

혼자 쓰는 리포지토리이므로 리뷰 없이 직접 병합합니다. 팀 실습(6교시)에서는 리뷰와 승인을 받은 뒤 병합합니다.

1. 초록 **Merge pull request**(PR 병합)를 클릭합니다.
2. **Confirm merge**(병합 확인)를 클릭합니다.
3. 보라색 **Merged** 표시가 나오면 **Delete branch**(브랜치 삭제)를 클릭합니다. GitHub의 브랜치만 지워지고 코드는 main에 남습니다.
4. **Actions** 탭을 클릭합니다. main에 push된 것으로 **테스트**가 한 번 더 실행되는 것을 봅니다.

확인: PR 제목 아래 보라색 **Merged**, **Actions** 탭에 **테스트** 실행 기록 2개(PR 때, 병합 때)가 보입니다.

!!! info "병합 버튼 옆 화살표의 세 가지"
    초록 버튼 옆 **▼**를 누르면 병합 방법이 보입니다. 셋 다 코드는 똑같이 main에 들어가고, main에 기록이 남는 모양만 다릅니다.

    | 방법 | main에 남는 기록 |
    |---|---|
    | **Create a merge commit** (기본) | 브랜치의 커밋이 모두 남고 병합 커밋이 하나 더 생깁니다. **오늘은 이것** |
    | **Squash and merge** | PR의 커밋을 커밋 하나로 합칩니다 |
    | **Rebase and merge** | 병합 커밋 없이 커밋을 main 끝에 일렬로 붙입니다 |

    버튼 이름이 **Merge pull request**가 아니면 **▼**에서 **Create a merge commit**을 고릅니다. 보이는 방법은 리포지토리 설정에 따라 다를 수 있습니다.

!!! note "팀에서는 병합 전에 리뷰가 있습니다"
    오늘 오후에는 다른 팀원이 **Files changed** → **Review changes**에서 **Comment**(의견), **Approve**(병합해도 됨), **Request changes**(고친 뒤 병합) 중 하나로 리뷰합니다. 작성자는 자기 PR을 승인할 수 없습니다. 고칠 점을 받으면 같은 브랜치에 커밋하고 **Sync Changes**를 누릅니다. 새 PR을 열지 않아도 같은 PR에 이어 붙습니다.

## STEP 6. VS Code를 main으로 돌아와 최신으로 맞추기

1. VS Code 상태 표시줄의 브랜치 이름 `overlap-check`를 클릭합니다.
2. 목록에서 `main`을 고릅니다.
3. 소스 제어의 **Sync Changes** 버튼, 또는 상태 표시줄 브랜치 이름 옆 동기화 아이콘을 클릭합니다. 확인 창이 뜨면 **OK**를 누릅니다.
4. `booking/rules.py`를 열어 겹침 검사 코드가 있는지 봅니다.
5. 터미널에서 테스트를 돌려 봅니다.

    === "Windows"

        ```bash
        python -m pytest
        ```

    === "Mac"

        ```bash
        python3 -m pytest
        ```

확인: 브랜치가 `main`이고, `rules.py`에 겹침 검사가 있고, 테스트가 모두 통과합니다.

!!! tip "오늘 오후에 그대로 씁니다"
    브랜치 → `/plan` → Agent 구현 → 검토 → 직접 검증 → 커밋 → PR → CI → 병합. 5~6교시 팀 실습은 이 흐름을 역할을 나눠 다시 합니다.

## 다 됐는지 확인

- [ ] `overlap-check` 브랜치를 Publish했다
- [ ] PR 설명을 Copilot **Summary**로 만들고 직접 고쳤다
- [ ] PR에서 **테스트 / test**가 초록 체크다
- [ ] PR을 병합했고 보라색 **Merged**가 보인다
- [ ] VS Code가 main이고, 겹침 검사 코드가 들어 있다

## 막히면

!!! tip "먼저 Copilot과 함께 해결합니다"
    오류 메시지나 막힌 상황을 Chat(Ask)에 붙여 넣고 원인과 해결 순서를 묻습니다. 아래는 자주 막히는 경우입니다. 묻는 방법은 [막혔을 때](../setup/3-troubleshooting.md#copilot)에 있습니다.

??? failure "Publish Branch를 눌렀더니 로그인 창이 계속 떠요"
    1-2에서 로그인한 GitHub 계정과 같은 계정으로 허용해야 합니다. 브라우저에서 다른 계정으로 로그인되어 있으면 로그아웃하고 다시 시도합니다.

??? failure "테스트 / test가 빨간 X예요"
    **Details**를 눌러 빨간 줄을 찾습니다. 대부분 내 PC에서 실패하던 테스트입니다. VS Code에서 `overlap-check` 브랜치로 고친 뒤 커밋하고 **Sync Changes**를 누르면 PR에 커밋이 추가되고 검사가 다시 돕니다.

??? failure "검사 영역에 테스트가 안 보여요"
    리포지토리에 `.github/workflows/ci.yml`이 있는지 봅니다. 템플릿으로 만들었다면 들어 있습니다. **Actions** 탭에 "워크플로를 켜라"는 안내가 있으면 초록 버튼으로 켭니다.

??? failure "Merge pull request 버튼이 회색이에요"
    검사가 아직 실행 중일 수 있습니다. 노란 원이 초록 체크가 될 때까지 기다립니다.

??? failure "main으로 바꿨는데 rules.py에 겹침 검사가 없어요"
    아직 Pull하지 않은 것입니다. STEP 6의 3번처럼 동기화 아이콘을 누릅니다.
