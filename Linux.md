# 빅테이터 플랫폼 구축

> 실제 현업에서는 여러 대의 서버를 구축해 클러스터링 하지만 우리는 할 수 없기에 가상머신을 4대 구축해 클러스터링 한다.

## 가상머신(cent OS)

### 머신 복제 후 ip 확인

* `ifconfig`명령어를 통해 4대의 서버에 설정된 ip를 확인.
  * hadoop**01** ip : 192.168.111.129
  * hadoop**02** ip : 192.168.111.131
  * hadoop**03** ip : 192.168.111.128
  * hadoop**04** ip : 192.168.111.130

* `ssh ip주소`를 통해 다른 가상머신에 연결해보고

* `exit`을 통해 연결을 해제한다.

### 머신 4대를 클러스터링

#### 방화벽 해제

* `systemctl list-units --type=service`

  > 특정 서비스를 확인한다.

* `systemctl status firewalld`

  > 방화벽 상태 확인

* `systemctl stop firewalld`

  > 방화벽 작동 중지

  * `systemctl disable firewalld`명령으로 완벽 중지

#### hostname 변경

* `hostnamectl set-hostname (설정할 이름)`

#### DNS 설정

* etc -> hosts 파일 등록

  >192.168.111.129 hadoop01
  >192.168.111.131 hadoop02
  >192.168.111.128 hadoop03
  >192.168.111.130 hadoop04

* `/etc/init.d/network restart`

  > 네트워크 프로세스를 restart
  >
  > => ip가 아닌 도메인으로 접속하기 위해

* 설정 확인

* 4대에 모두 적용되도록 hadoop1에서 2,3,4에 직접 접속

  > !! 반드시 1에서 접속해야함

  * **`scp`** copy할 파일(위치까지 명시) copy받을 서버의 위치

    > `scp /etc/hosts root@hadoop02:/etc/hosts`

  * `ssh 서버` "실행할 명령문"

    > 원격 서버에 실행명령
    >
    > `ssh hadoop04 "/etc/init.d/network restart"`

* 암호화된 통신을 위해서 공개키 생성 후 배포

  * `su hadoop`

    > hadoop계정으로 변경
    >
    > `su -` : root계정 홈 디렉토리

  * `ssh-keygen -t rsa`

    > ssh 키 생성 명령어

  * `ssh-copy-id -i id_rsa.pub hadoop@hadoop02`

    > 생성된 공개키 배포

## JDK

> www.oracle.com 에서 8u231 linux x64 rpm 다운

* STS의 Remote Systems를 이용해 옮기거나 직접 드래그해서 옮길 수 있다.

* `rpm -Uvh 설치할파일이름.rpm`

  > 위 명령어를 통해 rpm파일 설치가 가능하다
  >
  > **U** : 원래 있던 게 있으면 **upgrade**하겠다는 옵션
  >
  > **v** : 설치과정을 보겠다는 옵션 (**view**)
  >
  > **h** : 설치진행과정을 특수문자 "#"으로 표시한다.
  >
  > [기타 옵션 참고](https://itdexter.tistory.com/303)

* 

