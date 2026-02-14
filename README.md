# Git & Github 개인 공부 저장소

## 과거로 돌아가는 세 가지 방법

### 1. reset

특정 커밋 시점으로 되돌리며, **그 이후의 커밋 이력을 제거**한다.

```bash
# --soft: 커밋만 되돌리고, 변경사항은 staging area에 유지
git reset --soft <커밋해시>

# --mixed (기본값): 커밋을 되돌리고, 변경사항은 working directory에 유지
git reset --mixed <커밋해시>
git reset <커밋해시>

# --hard: 커밋을 되돌리고, 변경사항도 모두 삭제
git reset --hard <커밋해시>
```

| 옵션      | 커밋   | staging area | working directory |
| --------- | ------ | ------------ | ----------------- |
| `--soft`  | 되돌림 | 유지         | 유지              |
| `--mixed` | 되돌림 | 되돌림       | 유지              |
| `--hard`  | 되돌림 | 되돌림       | 되돌림            |

> **주의:** `--hard`는 변경사항이 완전히 사라지므로 신중하게 사용해야 한다.

---

### 2. revert

특정 커밋의 변경사항을 **취소하는 새로운 커밋**을 만든다. 기존 이력이 보존된다.

```bash
# 특정 커밋을 되돌리는 새 커밋 생성
git revert <커밋해시>

# 커밋 메시지 편집 없이 바로 revert
git revert --no-edit <커밋해시>

# revert 결과를 커밋하지 않고 staging area에만 반영
git revert --no-commit <커밋해시>
```

> **팁:** 이미 원격 저장소에 push한 커밋을 되돌릴 때는 `reset` 대신 `revert`를 사용하는 것이 안전하다.

---

### 3. checkout

특정 커밋 시점의 상태를 **임시로 확인**하거나, 특정 파일을 되돌린다.

```bash
# 특정 커밋 시점으로 이동 (Detached HEAD 상태)
git checkout <커밋해시>

# 원래 브랜치로 돌아오기
git checkout <브랜치명>

# 특정 파일만 해당 커밋 시점으로 되돌리기
git checkout <커밋해시> -- <파일경로>

# 작업 중인 파일의 변경사항 취소 (마지막 커밋 상태로 복원)
git checkout -- <파일경로>
```

> **참고:** Git 2.23 이후부터는 `checkout`의 역할이 `switch`(브랜치 전환)와 `restore`(파일 복원)로 분리되었다.
>
> ```bash
> git switch <브랜치명>       # 브랜치 전환
> git restore <파일경로>      # 파일 복원
> ```

## 차원 넘나들기 (Branch)

### 1. 브랜치 생성, 삭제, 이름 변경

```bash
# 브랜치 목록 확인
git branch

# 새 브랜치 생성
git branch <브랜치명>

# 브랜치 생성과 동시에 이동
git switch -c <브랜치명>

# 브랜치 이름 변경
git branch -m <기존이름> <새이름>

# 브랜치 삭제 (병합된 브랜치만 삭제 가능)
git branch -d <브랜치명>

# 브랜치 강제 삭제 (병합되지 않은 브랜치도 삭제)
git branch -D <브랜치명>
```

> **참고:** `-d`는 병합되지 않은 브랜치를 삭제하려 하면 경고가 뜬다. 정말 삭제하려면 `-D`를 사용한다.

---

### 2. 브랜치 병합

#### merge

두 브랜치의 변경사항을 **병합 커밋**을 만들어 합친다.

```bash
# main 브랜치에서 feature 브랜치를 병합
git switch main
git merge <브랜치명>
```

- 병합 이력이 커밋으로 남아 히스토리를 추적하기 쉽다.
- Fast-forward가 가능하면 별도의 병합 커밋 없이 포인터만 이동한다.

#### rebase

현재 브랜치의 커밋들을 **대상 브랜치 끝으로 재배치**한다.

```bash
# feature 브랜치에서 main을 기준으로 rebase
git switch <브랜치명>
git rebase main
```

- 커밋 히스토리가 깔끔한 직선으로 정리된다.
- 이미 원격에 push한 커밋은 rebase하지 않는 것이 원칙이다.

| 항목      | merge                    | rebase                   |
| --------- | ------------------------ | ------------------------ |
| 히스토리  | 병합 커밋이 남음         | 직선으로 깔끔하게 정리   |
| 기존 커밋 | 변경 없음                | 커밋 해시가 변경됨       |
| 사용 시점 | 협업 브랜치, 공개 브랜치 | 개인 작업 브랜치 정리 시 |

---

### 3. 충돌 해결 및 중단

브랜치 병합 시 같은 파일의 같은 부분을 다르게 수정했다면 **충돌(conflict)**이 발생한다.

#### 충돌 발생 시 파일 형태

```
<<<<<<< HEAD
현재 브랜치의 내용
=======
병합 대상 브랜치의 내용
>>>>>>> <브랜치명>
```

#### merge 충돌 해결

```bash
# 1. 충돌 파일을 열어 원하는 내용으로 수정
# 2. 수정 완료 후 staging
git add <충돌파일>

# 3. 병합 커밋 생성
git commit
```

#### rebase 충돌 해결

```bash
# 1. 충돌 파일을 열어 원하는 내용으로 수정
# 2. 수정 완료 후 staging
git add <충돌파일>

# 3. rebase 계속 진행
git rebase --continue
```

> rebase는 커밋 단위로 재배치하므로, 여러 커밋에서 충돌이 발생하면 각 커밋마다 충돌을 해결해야 한다.

#### 병합 중단

충돌 해결이 어렵거나 병합을 취소하고 싶을 때 사용한다.

```bash
# merge 중단 (병합 이전 상태로 복원)
git merge --abort

# rebase 중단 (rebase 이전 상태로 복원)
git rebase --abort
```
