# Django

> 다용도의, 안전한, 확장성 있는, 완결성 있는, 쉬운 유지보수, 포터블한
>
> **웹 프레임워크**

* MTV

  > **M**odel : 데이터를 관리 
  >
  > **T**emplate : 중간 관리자
  >
  > **V**iew : 사용자가 보는 화면

## intro

> start Django

1. 장고 설치

   ```bash
   pip install django==2.1.15
   pip list
   ```

2. 프로젝트 생성

   ```bash
   django-admin startproject <프로젝트 명>
   ```

   ```bash
   python manage.py runserver
   ```

3. 프로젝트 생성 시 제공하는 파일

   * manage.py
     * 전체 django와 관련된 모든 명령어를 manage.py를 통해 실행한다.
   * `__init__.py`
     * 현재 `__init__.py`파일이 존재하는 폴더를 하나의 프로젝트, 혹은 패키지로 인식하게 해주는 파일.
   * settings.py
     * 현재 프로젝트의 전체적인 설정 및 관리를 위해 존재하는 파일.
   * urls.py
     * 내 프로젝트에 접근할 수 있는 경로를 설정하기 위한 파일.
   * wsgi.py
     * 추후 배포 때 필요함.