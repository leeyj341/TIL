# Git status를 통해 정리하기

## CLI 기초 명령어

```bash
# list (파일 목록)
$ ls
# change directory
$ cd
# 빈 파일 생성
$ touch <파일명>
```

## 상황

### 1. `add`

```bash
$ touch a.txt
$ git status
On branch master

No commits yet
# 트래킹X. 새로 생성된 파일.
Untracked files:
  # 커밋을 하기 위한 곳에 포함시키려면
  # Staging area로 이동시키려면, git add
  (use "git add <file>..." to include in what will be committed)
        a.txt
# WD O, Staging area X
nothing added to commit but untracked files present (use "git add" to track)
```

```bash
$ git add a.txt
$ git status

On branch master

No commits yet
# 커밋될 변경사항들(staging area 0)
Changes to be committed:
  # unstage를 위해서 활용할 명령어(add 취소)
  (use "git rm --cached <file>..." to unstage)
        new file:   a.txt
```

### 2. `commit`

```bash
$ git commit -m 'Create a.txt'
[master (root-commit) 9f5239b] Create a.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 a.txt
```

* 커밋 내역 확인

  ```bash
  $ git log
  commit 9f5239b277cb0d29a41bf6a17dcfd72203215e00 (HEAD -> master)
  Author: leeyj341 <leeyj3794@gmail.com>
  Date:   Thu Apr 23 10:37:29 2020 +0900
  
      Create a.txt
      
  $ git log --oneline
  9f5239b (HEAD -> master) Create a.txt
  ```

### 3. 추가 파일 변경 상태

```bash
$ touch b.txt
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   a.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        b.txt

no changes added to commit (use "git add" and/or "git commit -a")

$ git add a.txt
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   a.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        b.txt
```

### 4. 커밋 메시지 변경

> **주의!!** 커밋 메시지 변경시 해시값 자체가 변경되어, 이미 원격저장소에 push한 이력에 대해서는 메시지 변경을 하면 안된다.

```bash
$ git commit --amend
```

* `vim` 텍스트 편집기가 실행된다.
  * `i`: 편집 모드
  * `esc`: 편집 모드를 종료하고, 명령 모드에서
    * `:wq` 
      * `write + quit`

```bash
[master f8d1289] a.txt 추가
 Date: Thu Apr 23 10:48:37 2020 +0900
 1 file changed, 5 insertions(+)
```

#### 4-1. 특정 파일을 빼놓고 커밋했을 때

```bash
$ git add <omit_file>
$ git commit --amend
```

* 빠뜨린 파일을 add 한 이후에 `commit --amend`를 하면, 해당 파일까지 포함하여 재커밋이 이뤄진다.

### 5. 작업 내용을 이전 버전으로 되돌리기

* a.k.a 작업하던 내용 버리기

```bash
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  # WD 변경사항을 버리기 위해서는 restore!
  (use "git restore <file>..." to discard changes in working directory)
        modified:   a.txt

no changes added to commit (use "git add" and/or "git commit -a")

$ git restore a.txt
$ git status
On branch master
nothing to commit, working tree clean
```

### 6. 특정 파일/폴더 삭제 커밋

> 해당 명령어는 실제 파일이 삭제되는 것은 아니지만, git에서 삭제되었다라는 이력을 남기는 것.

```bash
$ git rm --cached b.txt
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    b.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        b.txt

# 주의!! 해당 파일이 물리적으로 삭제되는 것은 아니다.
```

* 일반적으로는 `.gitignore`와 함께 활용한다.

  1. `.gitignore`에 해당 파일 등록
  2. `git rm --cached`를 통해 삭제 커밋

  * 이렇게 작업을 하면, 실제 파일은 삭제되지 않지만 이후로 git으로 전혀 관리되지 않는다.