# Stash

> 작업 내역을 임시 저장 할 수 있음.

## 기본 명령어

```bash
# 1. stash 공간에 작업내역 저장
$ git stash
Saved working directory and index state WIP on master

# 2. stash list 보기
$ git stash list
stash@{0}: WIP on master: a8cd8e9 Init

# 3. 임시 공간 내용 가져오기
$ git stash pop
```

## 예시

- 로컬에서 작업하고 있던 중, `pull` 을 받아서 원격 저장소에 새로운 내용을 반영 해야 하는 경우

```bash
$ git pull origin master
From https://github.com/edutak/big-iot-1001
 * branch            master     -> FETCH_HEAD
error: Your local changes to the following files woule:
        README.md
# 1. 커밋하거나 => 버전으로 남겨도 되는 경우
# 2. stash => 작업 중일 때
Please commit your changes or stash them before you merge
Aborting
Updating a8cd8e9..00d69a4
```

- 해결 방법

  ```bash
  $ git stash
  $ git pull origin master
  From https://github.com/edutak/big-iot-1001
   * branch            master     -> FETCH_HEAD
  Updating a8cd8e9..00d69a4
  Fast-forward
   README.md | 112 ++++++++++++++++++++++++++++++++++++--
   1 file changed, 104 insertions(+), 8 deletions(-)
  # 만약 동일 파일 수정이 있으면, conflict를 발생시킨다.
  $ git stash pop
  Auto-merging README.md
  CONFLICT (content): Merge conflict in README.md
  The stash entry is kept in case you need it again.
  ```