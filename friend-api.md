## 친구 관련 API
1. 친구 목록 조회
    ```tsx
    GET /users/friends
    response body: {
        users: [
            {
                nickname: string;
                imgUrl: string;
            }, ...
        ] // 정렬 알파벳순
    }
    ```
2. 친구 요청
    ```tsx
    POST /users/friends/pendings/{nickname}
    response header {
        201: created;
        로그인 X;
        없거나 차단한 유저에게 요청;
        400: 기타;
        401: 로그인 리다이렉션;
    }
    ```
3. 친구 요청 목록 조회 (pending list)
    ```tsx
    GET /users/friends
    response body: {
        users: [
            {
                nickname: string;
                imgUrl: string;
            }, ...
        ] // 정렬 알파벳순
    }
    ```
4. 친구 요청 수락
    ```tsx
    POST /users/friends/{nickname}
    ```
5. 친구 요청 거절
    ```tsx
    DELETE /users/friends/pendings/{nickname}
    ```
6. 친구 삭제
    ```tsx
    DELETE /users/friends/{nickname}
    200 OK
    400 - 기타 에러
    401 - 로그인 리다이렉션
    ```
7. DM 대회 내역 - 쿼리 어떻게 할지 고민 필요
    ```tsx
    GET /users/friends/{nickname}/chat?(백엔드 정해지면 쿼리 셋팅하기)
    response body: {
            chats: [
            {
                message: string;
                nickname: string;
                createdAt: Date;
            }, ...
        ]
    }
    ```
8. DM 전송
    ```tsx
    POST /users/friends/{nickname}/chat
    response body: {
        message: string;
    }
    response header: {

    }
    ```

