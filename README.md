# 간단한 git guide

---

## repository 에 작업 / 수정 사항 올리는 법

1. 클론 → 2) 파일 수정 → 3) `add` → `commit` → `push`

```bash
# 최초 1회 (사용자 정보 설정)
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# 저장소 가져오기
git clone https://github.com/<ORG>/<REPO>.git
cd <REPO>

# 작업 후 반영
git add <파일>     # 또는 .(add . 시 디렉토리의 모든 파일 올라감, 파일은 경로까지 전부 적어주기,
# 여러 파일 올릴시 띄어쓰기 후 적으면 됨)
ex) git add . / git add /src/launch
git commit -m "<메시지>"
ex) git commmit -m "first commit"
git push origin main
```

> 브랜치로 작업하고 싶다면:

```bash
git checkout -b <branch>
git push -u origin <branch>
```

---

## 원격 변경 내려받기 (fetch / pull)

### 가장 최신 브랜치로 변경하는 방법

```bash
git pull origin main
```

### 미리 보기(fetch) 후 무엇이 바뀌는지 확인

```bash
git fetch origin
# 변경 커밋 요약 그래프
git log --oneline --graph --decorate --left-right HEAD...origin/main
# 변경 파일 목록만
git diff --name-only HEAD origin/main
```

### 로컬 수정이 있을 때 안전하게 갱신하는 방법

```bash
git status                 # 수정 있나 확인
git stash push             # 내 변경 임시보관(새 파일까지 보관하려면 -u)
git pull origin main       # 원격 변경을 합치기(merge 방식)
git stash pop              # 내 변경 복원(여기서도 충돌 날 수 있음)
```

### 로컬을 원격 상태로 강제 맞추기 — 되돌리기 어려움

```bash
git fetch origin
git reset --hard origin/main
```

---

* 팀 전용 리포(예시):

  * `robocup-2026-ros-pkgs`
  * `robocup-2026-turtlebot`
  * `robocup-2026-sim`
*
---

## 간단 파일 레퍼런스 템플릿

```
====================
편집자 :
최종 수정일  : YYYY-MM-DD
작업 상태 : (초안/진행중/검토요청/완료)
역할 & 발행되는 토픽 :
====================
```

### 예시

```
====================
편집자 : 이다빈
최종 수정일  : 2025-09-16
작업 상태 : 진행중
역할 & 발행되는 토픽 : /cmd_vel, /scan, /tf
====================
```

---

## 협업 간단 규칙

* 대용량(>50MB)·가중치·비밀키는 업로드 금지.
  
---

## 치트시트(자주 쓰는 명령)

```bash
# 현재 상태 확인
git status
# 파일 변경 확인
git diff
# 원격 주소 확인
git remote -v
# 모든 원격 최신화 + 정리
git fetch --all --prune
```
