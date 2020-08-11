# Django

> Django 서버 배포



## django 추가코드

### 0. settings.py

- staticfiles 경로 추가
  - `STATICFILES_DIRS`을 사용하는 경우 동일한 경로 사용불가(이름변경 `ex. staticfiles=>static`)

```python
# settings.py
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
```



- ALLOWED_HOSTS
  - EC2 서버주소를 등록
  - 편하게 배포하기 위하여 `*` 로 등록 후 추후 수정가능

```python
# settings.py
ALLOWED_HOSTS = [
    '.compute.amazonaws.com',
    '*',
]
```



### 1. 의존성 저장

- freeze

```shell
pip freeze > requirements.txt
```



### 2. git push

- 원격저장소에 업로드 (add, commit, push)



## aws

### 0. 준비

- 완성된 django프로젝트
- 해외결제가 가능한 체크카드 or 신용카드
- 여유로운 마음



### 1. https://aws.amazon.com/ko/

- AWS 계정 생성
- 기본정보입력
- 카드정보입력
- 휴대폰인증
- 완료후 로그인



### 2. aws cloud9 

- AWS Management Console 에서 Cloud9 검색

![1](deploy.assets/1.png)



- 생성

![2](deploy.assets/2.png)



- 이름입력

![image-20200703152233821](deploy.assets/image-20200703152233821.png)



- 설정
  - 서버를 사용하지 않을 때 끄려면 default인 30분으로 설정

![4](deploy.assets/4.png)

 

- 생성완료

![5](deploy.assets/5.png)



- cloud9확인

![6](deploy.assets/6.png)



- 파일트리설정

![7](deploy.assets/7.png)



## EC2

> 새로운 탭에서 진행
>
> EC2는 cloud9 생성시 자동생성

### 0. 서비스검색

![8](deploy.assets/8.png)



### 1. 보안그룹

- 생성된 ID 클릭

![9](deploy.assets/9.png)



### 2. 인바운드 설정

- 편집

![10](deploy.assets/10.png)



- 규칙 추가 후 저장

![11](deploy.assets/11.png)



## python in Cloud9

### 0. pyenv & pyenv-virtualenv

- 설치 & 설정
  - 전체 복사 후 **Cloud9** 터미널에서 실행

```shell
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bashrc
exec "$SHELL"

git clone https://github.com/pyenv/pyenv-virtualenv.git $(pyenv root)/plugins/pyenv-virtualenv
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc
exec "$SHELL"

```

![image-20200703153206202](deploy.assets/image-20200703153206202.png)



### 1. python 설치&전역등록

> 프로젝트 진행한 버전에 맞게 설치

```shell
pyenv install 3.7.4
pyenv global 3.7.4
python -V
#=> Python 3.7.4
```



### 2. 가상환경생성

> 가상환경이름 기억!

```
pyenv virtualenv {가상환경이름}
```

![12](deploy.assets/12.png)



## project clone

> 루트폴더와 프로젝트, 두개의 폴더 이름에 주의하며 진행해주세요.
> 두 폴더의 이름을 통일하면 조금더 편하게 설정할 수 있습니다.

### 0. 준비

- `~`로 이동 => `cd ~`
  - 명령어를 작성하는 위치 주의!



- clone

```
git clone {project_remote_url}
```

![image-20200703154338960](deploy.assets/image-20200703154338960.png)



- 편의를 위해 폴더명 변경
  - 프로젝트 전체 폴더의 이름을 프로젝트이름과 동일하게 변경

![image-20200703154456679](deploy.assets/image-20200703154456679.png)



- 폴더구조
  - 프로젝트이름은 변수처럼 사용예정 이름 기억!

```
home
	ubuntu
		{프로젝트이름}
			{프로젝트이름}
			{앱}
			manage.py
```



- 클론한 폴더로 이동

```shell
cd {프로젝트이름}
```



- 가상환경 활성화

```shell
pyenv local {가상환경이름}
```

![image-20200703154545755](deploy.assets/image-20200703154545755.png)



- 라이브러리 설치

```shell
pip install -r requirements.txt
```

- 마이그레이션

```
python manage.py migrate
```

- createsuperuser

```shell
python manage.py createsuperuser
```

- loaddata (fixture가 있는경우)

```shell
python manage.py loaddata {data.json}
```

- collectstatic

```
python manage.py collectstatic
```





## nginx

### 0. 설치

```shell
sudo apt-get update
sudo apt-get install -y nginx
```



### 1. 설정

> vi를 사용하여 터미널에서 파일을 수정합니다.
> 사용법을 숙지하고 진행해주세요.



- 복사할 코드 미리 작성하기
  - 아래의 코드에서 각자의 프로젝트이름에 맞게 수정 후 아래에 붙여넣기
  - staticfiles의 경우 다른 폴더를 썼다면 이름수정

```
server_name *.compute.amazonaws.com;

location / {
		uwsgi_pass unix:///home/ubuntu/{프로젝트이름}/tmp/{프로젝트이름}.sock;
		include uwsgi_params;
}

location /static/ {
	alias /home/ubuntu/{프로젝트이름}/staticfiles/;
}
```

- 결과 붙여넣기 위한 빈칸

```
server_name *.compute.amazonaws.com;

location / {
		uwsgi_pass unix:///home/ubuntu/epiaproject/tmp/epiaproject.sock;
		include uwsgi_params;
}

location /static/ {
	alias /home/ubuntu/epiaproject/staticfiles/;
}
```



- 파일 수정

```shell
sudo vi /etc/nginx/sites-enabled/default
```



- 아래의 표시된 부분 수정
  - `i` 버튼으로 수정모드로 전환
  - 아래의 부분으로 방향키를 이용하여 이동
  - 수정
  - `esc` 로 수정모드 빠져나오기
  - `:wq` 명령어로 저장 후 종료

![16](deploy.assets/16.png)



- 수정 결과
  - 주석부분을 지워도 무방

![17](deploy.assets/17.png)



## uWSGI

### 0. 설치

```shell
pip install uwsgi
```

> 파이썬에서 사용하는 웹서버라고 생각하면 됨 Apache 같은 존재

### 1. 폴더&파일 생성

- 프로젝트 폴더 이동 (기존의 위치와 동일)

```
cd ~/{프로젝트이름}
```



- uwsgi 설정, 로그 저장할 폴더 생성 (파일트리에서 생성해도 무방)

```shell
mkdir tmp
mkdir -p log/uwsgi
mkdir -p .config/uwsgi/
```



- uwsgi 설정파일 생성 (파일트리에서 생성해도 무방)

```shell
touch .config/uwsgi/{프로젝트이름}.ini
```

![image-20200703160243254](deploy.assets/image-20200703160243254.png)



### 3. 수정

- `.config/uwsgi/{프로젝트이름}.ini` 설정파일 수정

```
# {프로젝트이름}/.config/uwsgi/{프로젝트이름}.ini

[uwsgi]
chdir = /home/ubuntu/{프로젝트이름}
module = {프로젝트이름}.wsgi:application
home = /home/ubuntu/.pyenv/versions/{가상환경이름}

uid = ubuntu
gid = ubuntu

socket = /home/ubuntu/{프로젝트이름}/tmp/{프로젝트이름}.sock
chmod-socket = 666
chown-socket = ubuntu:ubuntu

enable-threads = true
master = true
vacuum = true
pidfile = /home/ubuntu/{프로젝트이름}/tmp/{프로젝트이름}.pid
logto = /home/ubuntu/{프로젝트이름}/log/uwsgi/@(exec://date +%%Y-%%m-%%d).log
log-reopen = true
```



- 결과

![image-20200703160504672](deploy.assets/image-20200703160504672.png)



### 4. daemon

- 설정파일 생성 (파일트리에서 생성해도 무방)

```shell
touch .config/uwsgi/uwsgi.service
```



- `.config/uwsgi/uwsgi.service` 설정파일 수정

```
[Unit]
Description=uWSGI Service
After=syslog.target

[Service]
User=ubuntu
ExecStart=/home/ubuntu/.pyenv/versions/{가상환경이름}/bin/uwsgi -i /home/ubuntu/{프로젝트이름}/.config/uwsgi/{프로젝트이름}.ini

Restart=always
KillSignal=SIGQUIT
Type=notify
StandardError=syslog
NotifyAccess=all

[Install]
WantedBy=multi-user.target
```



- 결과

![image-20200703160645560](deploy.assets/image-20200703160645560.png)



- 심볼릭링크 생성

```shell
sudo ln -s ~/{프로젝트이름}/.config/uwsgi/uwsgi.service /etc/systemd/system/uwsgi.service
```



- 등록

```shell
# daemon reload
sudo systemctl daemon-reload

# uswgi daemon enable and restart
sudo systemctl enable uwsgi
sudo systemctl restart uwsgi.service

# check daemon
sudo systemctl | grep nginx
sudo systemctl | grep uwsgi

# nginx restart
sudo systemctl restart nginx
sudo systemctl restart uwsgi
```



- 아래의 에러 상황에서 80번 포트 프로세스 종료

![image-20200703160835890](deploy.assets/image-20200703160835890.png)



```shell
sudo lsof -t -i tcp:80 -s tcp:listen | sudo xargs kill
```



- 최종확인
  - EC2대시보드에서 DNS혹은 IP확인

![22](deploy.assets/22.png)