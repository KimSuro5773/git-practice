# Git & Github 복습 문제

---

## 1부: 과거로 돌아가는 세 가지 방법

### Q1. 빈칸 채우기

`git reset`의 세 가지 옵션에 대한 표를 완성하시오.

| 옵션      | 커밋   | staging area | working directory |
| --------- | ------ | ------------ | ----------------- |
| `--soft`  | (  )   | (  )         | (  )              |
| `--mixed` | (  )   | (  )         | (  )              |
| `--hard`  | (  )   | (  )         | (  )              |

---

### Q2. 객관식

`git reset` 옵션을 지정하지 않으면 기본값은 무엇인가?

- A) `--soft`
- B) `--mixed`
- C) `--hard`
- D) `--keep`

---

### Q3. O/X 문제

> `git reset --hard`를 사용하면 되돌린 변경사항을 working directory에서 확인할 수 있다.

---

### Q4. 서술형

이미 원격 저장소에 push한 커밋을 되돌려야 한다. `reset`과 `revert` 중 어떤 것을 사용해야 하며, 그 이유는?

---

### Q5. 명령어 작성

특정 커밋을 되돌리되, 커밋을 바로 만들지 않고 staging area에만 반영하고 싶다. 어떤 명령어를 사용해야 하는가?

```bash
git _______ _______ <커밋해시>
```

---

### Q6. 객관식

`git checkout <커밋해시>`를 실행하면 어떤 상태가 되는가?

- A) 해당 커밋으로 reset 된다
- B) 해당 커밋을 revert 하는 새 커밋이 생긴다
- C) Detached HEAD 상태가 된다
- D) 해당 커밋이 삭제된다

---

### Q7. 명령어 작성

Git 2.23 이후, `checkout`의 역할이 두 가지 명령어로 분리되었다. 각각의 명령어를 작성하시오.

```bash
# 브랜치 전환
git _______ <브랜치명>

# 파일 복원
git _______ <파일경로>
```

---

## 2부: 차원 넘나들기 (Branch)

### Q8. 명령어 작성

새로운 브랜치를 생성하면서 동시에 해당 브랜치로 이동하는 명령어를 작성하시오.

```bash
git _______ _______ <브랜치명>
```

---

### Q9. 객관식

병합되지 않은 브랜치를 삭제하려 할 때, `git branch -d`를 사용하면 어떻게 되는가?

- A) 정상적으로 삭제된다
- B) 경고가 뜨며 삭제되지 않는다
- C) 강제로 삭제된다
- D) 브랜치 이름이 변경된다

---

### Q10. 명령어 작성

브랜치의 이름을 `old-name`에서 `new-name`으로 변경하는 명령어를 작성하시오.

```bash
git branch _______ old-name new-name
```

---

### Q11. O/X 문제

> `git merge`는 항상 병합 커밋을 생성한다.

---

### Q12. 빈칸 채우기

merge와 rebase를 비교한 표를 완성하시오.

| 항목      | merge            | rebase             |
| --------- | ---------------- | ------------------ |
| 히스토리  | (            )   | (              )   |
| 기존 커밋 | (            )   | (              )   |

---

### Q13. 명령어 작성

`feature` 브랜치에서 `main`을 기준으로 rebase 하려고 한다. 올바른 순서로 명령어를 작성하시오.

```bash
git _______ feature
git _______ main
```

---

### Q14. 서술형

merge 충돌이 발생했을 때, 해결 과정을 순서대로 설명하시오.

---

### Q15. 명령어 작성

rebase 도중 충돌이 발생했다. 충돌을 수정한 후 rebase를 계속 진행하는 명령어를 작성하시오.

```bash
git add <충돌파일>
git _______ _______
```

---

### Q16. 객관식

rebase 도중 충돌 해결이 너무 복잡해서 rebase를 취소하고 싶다. 어떤 명령어를 사용해야 하는가?

- A) `git rebase --cancel`
- B) `git rebase --abort`
- C) `git rebase --undo`
- D) `git rebase --reset`

---

## 3부: Github 사용하기

### Q17. 명령어 작성

원격 저장소의 URL을 포함한 상세 정보를 확인하는 명령어를 작성하시오.

```bash
git remote _______
```

---

### Q18. 명령어 작성

`https://github.com/user/repo.git` 주소를 `origin`이라는 이름으로 원격 저장소에 추가하는 명령어를 작성하시오.

```bash
git _______ _______ origin https://github.com/user/repo.git
```

---

### Q19. 객관식

원격에 새로운 커밋이 있고, 로컬에도 새로운 커밋이 있을 때 `git pull --rebase`를 실행하면 어떻게 되는가?

- A) 병합 커밋이 생성된다
- B) 로컬 커밋이 원격 커밋 뒤로 재배치된다
- C) 원격 커밋이 삭제된다
- D) 충돌이 무조건 발생한다

---

### Q20. O/X 문제

> `git push --force`는 협업 시 안전하게 사용할 수 있다.

---

### Q21. 명령어 작성

`feature` 브랜치를 원격에 최초로 push하면서 추적 관계를 설정하는 명령어를 작성하시오.

```bash
git push _______ _______ feature
```

---

### Q22. 명령어 작성

로컬과 원격의 브랜치 목록을 모두 확인하는 명령어를 작성하시오. (2가지)

```bash
git branch _______
git branch _______
```

---

### Q23. 명령어 작성

원격에 있는 `develop` 브랜치를 로컬에 받아와서 전환하는 명령어를 작성하시오.

```bash
git switch _______ _______
```

---

### Q24. 명령어 작성

원격 저장소 `origin`에서 `feature` 브랜치를 삭제하는 명령어를 작성하시오.

```bash
git push _______ _______ feature
```

---

### Q25. 시나리오 문제

다음 상황에서 어떤 명령어를 사용해야 하는지 순서대로 작성하시오.

> 팀원이 원격 `main` 브랜치에 새로운 커밋을 push했다.
> 나도 로컬 `main`에서 새로운 커밋을 만들었다.
> 히스토리를 깔끔하게 유지하면서 원격의 변경사항을 가져오고 싶다.

```bash
git _______
```

---

## 정답

<details>
<summary>정답 보기 (클릭하여 펼치기)</summary>

### Q1.

| 옵션      | 커밋   | staging area | working directory |
| --------- | ------ | ------------ | ----------------- |
| `--soft`  | 되돌림 | 유지         | 유지              |
| `--mixed` | 되돌림 | 되돌림       | 유지              |
| `--hard`  | 되돌림 | 되돌림       | 되돌림            |

### Q2. **B) `--mixed`**

### Q3. **X** - `--hard`는 변경사항이 완전히 사라지므로 working directory에서 확인할 수 없다.

### Q4.
`revert`를 사용해야 한다. `reset`은 커밋 이력을 제거하므로 이미 push한 커밋에 사용하면 원격과 로컬의 이력이 달라져 문제가 발생한다. `revert`는 취소하는 새로운 커밋을 만들어 기존 이력을 보존하므로 안전하다.

### Q5. `git revert --no-commit <커밋해시>`

### Q6. **C) Detached HEAD 상태가 된다**

### Q7.
```bash
git switch <브랜치명>
git restore <파일경로>
```

### Q8. `git switch -c <브랜치명>`

### Q9. **B) 경고가 뜨며 삭제되지 않는다** (강제 삭제하려면 `-D`를 사용)

### Q10. `git branch -m old-name new-name`

### Q11. **X** - Fast-forward가 가능하면 별도의 병합 커밋 없이 포인터만 이동한다.

### Q12.

| 항목      | merge            | rebase                   |
| --------- | ---------------- | ------------------------ |
| 히스토리  | 병합 커밋이 남음 | 직선으로 깔끔하게 정리   |
| 기존 커밋 | 변경 없음        | 커밋 해시가 변경됨       |

### Q13.
```bash
git switch feature
git rebase main
```

### Q14.
1. 충돌이 발생한 파일을 열어 원하는 내용으로 수정한다.
2. 수정 완료 후 `git add <충돌파일>`로 staging 한다.
3. `git commit`으로 병합 커밋을 생성한다.

### Q15. `git rebase --continue`

### Q16. **B) `git rebase --abort`**

### Q17. `git remote -v`

### Q18. `git remote add origin https://github.com/user/repo.git`

### Q19. **B) 로컬 커밋이 원격 커밋 뒤로 재배치된다**

### Q20. **X** - `--force`는 원격의 커밋을 덮어쓰므로 협업 시 다른 사람의 작업을 날릴 수 있다.

### Q21. `git push -u origin feature`

### Q22.
```bash
git branch --all
git branch -a
```

### Q23. `git switch -t origin/develop`

### Q24. `git push origin --delete feature`

### Q25. `git pull --rebase`

</details>