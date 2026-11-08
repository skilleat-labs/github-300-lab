# 실습 4-4. 팀 구성

!!! abstract "이 실습에서 할 일"
    - 팀 번호와 역할(PO, PM, BA, 개발자)을 받습니다.
    - PO가 템플릿으로 팀 리포지토리 `room-booking-team<번호>`를 만들고 팀원을 초대합니다. 팀원은 수락하고 각자 VS Code로 가져옵니다.
    - PO가 6교시 배포에 대비해 Pages 설정을 미리 바꿔 둡니다.

**소요 시간** 약 10분  **실습 장소** 팀 리포지토리 `room-booking-team<번호>`  **관련 교안** [5교시 역할 카드](../class5/index.md#role-cards)

## 준비

### 팀과 역할 받기

강사가 팀 번호와 역할을 정해 줍니다. 21명 기준 예시입니다.

| 팀 | 인원 | 역할 |
|---|---|---|
| 1~3팀 | 4명 | PO, PM, BA, 개발자 각 1명 |
| 4~6팀 | 3명 | PO(PM 겸임), BA, 개발자 각 1명 |

!!! warning "3인 팀"
    3인 팀은 **PO가 PM을 겸합니다.** 5~7교시 페이지에서 "PM"이라고 적힌 일은 PO가 합니다. 팀 백로그도 S4를 빼고 3개만 합니다.

!!! tip "역할은 '누가 결정하고, 정리하고, 검토하나'입니다"
    역할이 개발자가 아니어도 코드를 씁니다. 정확히는 **모두가 Copilot에게 시켜서** 스토리 하나씩 구현합니다. 역할은 그 외에 누가 우선순위를 결정하는지(PO), 이슈와 병합을 정리하는지(PM), 인수 조건으로 검토하는지(BA), 기술 위험을 보는지(개발자)를 나눈 것입니다.

받은 내용을 메모해 둡니다. 이 페이지부터 `<번호>`는 내 팀 번호, `<PO아이디>`는 우리 팀 PO의 GitHub 아이디로 바꿔 읽습니다.

```text
우리 팀 번호:
내 역할:
PO 아이디:
PM 아이디:
BA 아이디:
개발자 아이디:
```

### 전체 순서

| 순서 | 누가 | 무엇을 |
|---|---|---|
| 1 | PO | 템플릿으로 `room-booking-team<번호>` 만들기 (Public) |
| 2 | PO | **Collaborators**로 팀원 초대 |
| 3 | PO | **Settings** → **Pages** → Source를 **GitHub Actions**로 |
| 4 | 팀원 | 초대 수락 |
| 5 | 모두 | VS Code에서 **Git: Clone**으로 가져오기 |

## STEP 1. (PO) 팀 리포지토리 만들기

1. 브라우저 주소창에 Starter 템플릿 주소를 입력합니다.

    ```text
    https://github.com/skilleat-labs/meeting-room-starter
    ```

2. 오른쪽 위 초록 **Use this template**(이 템플릿 사용) → **Create a new repository**를 클릭합니다.
3. **Owner**(소유자)가 내 아이디인지 봅니다.
4. **Repository name**에 팀 번호를 넣어 입력합니다. 예: 3팀이면 `room-booking-team3`

    ```text
    room-booking-team<번호>
    ```

5. **Public**(공개)을 고릅니다. 무료 계정에서 Pages를 쓰려면 Public이어야 합니다.
6. **Create repository**를 클릭합니다.

확인: 주소가 `github.com/<PO아이디>/room-booking-team<번호>`이고 `booking`, `docs`, `tests` 폴더가 보입니다.

## STEP 2. (PO) 팀원 초대하기

1. 팀 리포지토리에서 **Settings**(설정) 탭을 클릭합니다.
2. 왼쪽 메뉴 **Collaborators**(협업자)를 클릭합니다. 비밀번호나 인증 확인 창이 뜨면 본인이 직접 확인합니다.
3. **Add people**(사람 추가)을 클릭합니다.
4. 팀원 아이디를 입력하고 목록에서 고른 뒤 **Add 아이디 to this repository**를 클릭합니다. 역할을 묻는 화면이 나오면 **Write**(쓰기)를 고릅니다.
5. 팀원 수만큼 반복합니다. (4인 팀 3명, 3인 팀 2명)
6. 팀원에게 "초대 보냈습니다"라고 말로 알립니다.

확인: **Collaborators** 목록에 팀원이 모두 `Pending invite`(초대 대기) 또는 이름으로 보입니다.

## STEP 3. (PO) Pages 설정 미리 바꿔 두기

6교시 미션 6-2에서 팀이 Copilot으로 배포 워크플로를 만듭니다. 그때 바로 배포되도록 설정만 먼저 바꿔 둡니다. 지금은 웹페이지가 열리지 않는 것이 정상입니다.

1. **Settings** → 왼쪽 메뉴 **Pages**를 클릭합니다.
2. **Build and deployment**(빌드와 배포) 아래 **Source**(소스)를 **GitHub Actions**로 바꿉니다.
3. 아래에 추천 워크플로 카드가 나와도 누르지 않습니다. 6-2에서 Copilot으로 만듭니다.

확인: **Source**가 **GitHub Actions**로 보입니다.

## STEP 4. (팀원) 초대 수락하기

1. PO가 "초대 보냈습니다"라고 하면 GitHub 가입 이메일을 열거나 아래 주소로 이동합니다.

    ```text
    https://github.com/<PO아이디>/room-booking-team<번호>/invitations
    ```

2. **Accept invitation**(초대 수락)을 클릭합니다.

확인: 팀 리포지토리가 열리고, 파일을 열었을 때 연필 아이콘(편집)이 보입니다.

## STEP 5. (모두) VS Code로 가져오기

PO도 포함해 모두 각자 PC로 가져옵니다.

1. 팀 리포지토리 화면에서 초록 **Code** → **HTTPS** 주소 옆 복사 아이콘을 클릭합니다.
2. VS Code에서 명령 팔레트를 엽니다. Windows는 ++ctrl+shift+p++, Mac은 ++cmd+shift+p++
3. `Git: Clone`을 입력하고 고릅니다.
4. 복사한 주소를 붙여 넣고 ++enter++를 누릅니다.
5. 저장 위치로 `문서/copilot-lab` 폴더를 고릅니다. `room-practice`와 나란히 놓입니다.
6. 오른쪽 아래 **Open**(열기)을 클릭합니다. "작성자를 신뢰하느냐"는 창이 뜨면 **Yes, I trust the authors**를 누릅니다.
7. 터미널을 열고 테스트를 실행합니다.

    === "Windows"

        ```bash
        python -m pytest
        ```

    === "Mac"

        ```bash
        python3 -m pytest
        ```

확인: VS Code 탐색기 맨 위에 `ROOM-BOOKING-TEAM<번호>`가 보이고, `4 passed`가 나옵니다.

!!! tip "창을 헷갈리지 않게"
    오후에는 팀 리포지토리 창만 씁니다. 개인 `room-practice` 창은 닫아도 됩니다. 7-1에서 다시 엽니다.

!!! note "오전에 만든 것은 따라오지 않아요"
    팀 리포지토리는 템플릿에서 새로 만들었기 때문에 Starter와 같은 상태입니다. 2교시에 고친 18시 버그, 4교시에 넣은 겹침 검사, 3교시의 지침 파일과 프롬프트 파일은 **없습니다.** 그래서 5교시에 팀이 S1~S4로 다시 만듭니다. 한 번 해 본 일이라 막히지 않습니다.

## 다 됐는지 확인

- [ ] 팀 번호와 역할을 메모했다
- [ ] (PO) `room-booking-team<번호>`를 Public으로 만들었다
- [ ] (PO) 팀원 모두 Collaborators에 있다
- [ ] (PO) Pages Source가 **GitHub Actions**다
- [ ] (팀원) 초대를 수락했다
- [ ] (모두) VS Code에 팀 리포지토리를 가져왔고 테스트 4개가 통과한다

## 막히면

??? failure "Use this template 버튼이 안 보여요"
    로그인이 안 되어 있거나 주소가 틀린 경우입니다. 오른쪽 위에 내 프로필 사진이 보이는지, 주소가 `skilleat-labs/meeting-room-starter`인지 확인합니다.

??? failure "초대 주소를 열었더니 404가 떠요"
    PO가 아직 초대하지 않았거나 PO 아이디를 잘못 넣은 것입니다. PO의 **Collaborators** 목록에 내 아이디가 있는지 함께 봅니다.

??? failure "Pages 메뉴에 GitHub Actions가 없어요"
    리포지토리가 Private이면 무료 계정에서 Pages를 못 씁니다. **Settings** → **General** 맨 아래 **Danger Zone** → **Change visibility**로 Public으로 바꿉니다. 이 작업은 PO가 직접 확인하고 합니다.

??? failure "Clone할 때 로그인 창이 떠요"
    GitHub 계정으로 허용합니다. 1-2에서 로그인한 계정과 같아야 합니다.

??? failure "5명 이상이거나 2명이에요"
    강사에게 알립니다. 2명이면 다른 팀에 합류하고, 5명이면 한 명이 다른 팀으로 가거나 BA를 두 명으로 둡니다.
