## 차단 관련 API
1. 차단 목록 조회
    ```tsx
    GET /blocks
    response body: {
        users: [
            {
                nickname: string;
                imgUrl: string;
            }, ...
        ]
    }
    ```
2. 유저 차단
    ```tsx
    POST /users/blocks/{nickname}
    201 CREATED
    400 - 기타 에러
    401 - 로그인 리다이렉션
    ```
3. 차단 해제
    ```tsx
    DELETE /users/blocks/{nickname}
    200 OK
    400 - 기타 에러
    401 - 로그인 리다이렉션
    ```
