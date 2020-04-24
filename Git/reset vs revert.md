# reset vs revert

## 1. reset

- 특정 버전으로 되돌아가는 작업

  ```bash
  $ git reset {커밋해시코드}
  ```

  - `reset` 명령어의 결과는 다음과 같다.

    ```bash
    $ git log --oneline
    275a7e2 ddd
    00d69a4 (origin/master) Update README.md
    $ git reset 00d69a4
    $ git log --oneline
    00d69a4 (origin/master) Update README.md
    ```

  - `reset` 옵션

    - 기본 : 이전 이력의 변경 사항을 WD에 보관
    - `--hard` : 이전 이력의 변경 사항은 모두 삭제. **주의**

## 2. revert

- 특정 시점을 되돌렸다는 커밋을 발생 시킴.

  ```bash
  $ git log --oneline
  275a7e2 ddd
  00d69a4 (origin/master) Update README.md
  $ git revert 275a7e2
  $ git log --oneline
  bca6426 (HEAD -> master) Revert "ddd"
  275a7e2 ddd
  00d69a4 (origin/master) Update README.md
  ```