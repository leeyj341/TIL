REST API를 테스트 할 수 있는 다양한 도구들이 존재합니다.

- [Postman](https://www.getpostman.com/)
- [Insomnia](https://insomnia.rest/)

여기서는 Postman를 사용해 간단하게 REST API를 테스트하는 방법에 대해 소개합니다.

먼저 Postman을 설치한 후 실행하면 아래와 같은 화면을 볼 수 있습니다.

![1](images/1-1610638313049.png)

여기에 테스틑 위한 REST API 정보를 입력합니다. 아래 화면은 로그인을 위한 REST API 정보를 입력하고 실행한 모습입니다.

> 로그인 REST API
>
> - Host: [http://localhost:8080](http://localhost:8080/)
> - Method: POST
> - URL: /api/auth
> - Headers:
>   - Content-Type : application/json
>   - Accept: application/json
> - Body: `{ "principal": "test00@gmail.com", "credentials": "1234" }`

![2](images/2-1610638319407.png)

![3](images/3-1610638322550.png)

API 실행 결과를 확인할 수 있습니다. (그림의 하단)

```json
{
    "success": true,
    "response": {
        "apiToken": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJyb2xlcyI6WyJST0xFX1VTRVIiXSwiaXNzIjoic29jaWFsX3NlcnZlciIsImlhdCI6MTU2MDk1MTkyNywidXNlcktleSI6MSwiZW1haWwiOiJ0ZXN0MDBAZ21haWwuY29tIn0.6UOv2mBuo6dtknjDvENr92rTuA8Zc2fCHHdOFCDVYEeyp4ovxKMvSvHpQm1NSQkgrrOIsRMEtJK5BHfmIMGC3w",
        "user": {
            "seq": 1,
            "email": {
                "address": "test00@gmail.com"
            },
            "loginCount": 1,
            "lastLoginAt": "2019-06-19T22:45:27.169",
            "createAt": "2019-06-19T22:39:45.806"
        }
    }
}
```

로그인 REST API는 퍼블릭 권한이기 때문에 누구나 호출할 수 있지만, 어떤 REST API는 인증된 사용자만 호출할 수 있습니다. 예를 들어 내 정보를 가져오기 위한 REST API는 인증된 사용자만 호출할 수 있습니다.

> 내 정보 조회 REST API
>
> - Host: [http://localhost:8080](http://localhost:8080/)
> - Method: GET
> - URL: /api/user/me
> - Headers:
>   - Accept: application/json

내 정보 조회 REST API를 호출해보면 아래 화면 처럼 401 Unauthorized 오류가 납니다.

![4](images/4-1610638329338.png)

REST API를 호출하는 사용자가 인증된 사용자임을 서버에 알리기 위해 Header에 `api_key` 항목을 추가합니다. `api_key` 헤더 value에는 다음과 같은 값을 입력합니다.

> Bearer {로그인 API의 응답 중 apiToken 항목}
> 예: Bearer eyJ0eXAiOiJ블라블라~~

![5](images/5-1610638334475.png)

API 호출이 성공하고 아래와 같은 JSON 포맷의 결과를 확인할 수 있습니다. (출력값은 실행 시점에 따라 다를 수 있음)

```json
{
    "success": true,
    "response": {
        "seq": 1,
        "email": {
            "address": "test00@gmail.com"
        },
        "loginCount": 1,
        "lastLoginAt": "2019-06-19T22:45:27.169",
        "createAt": "2019-06-19T22:39:45.806"
    }
}
```

