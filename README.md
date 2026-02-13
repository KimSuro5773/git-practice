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
