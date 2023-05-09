1. 친구 추가
    
    ```tsx
    POST /users/friends/{nickname}
    201 CREATED
    - 로그인 x
    - 없는 && 차단한 유저 상대로 추가
    400 - 기타 에러
    401 - 로그인 리다이렉션
    ```
    
2. 친구 삭제
    
    ```tsx
    DELETE /users/friends/{nickname}
    200 OK
    400 - 기타 에러
    401 - 로그인 리다이렉션
    ```
    
3. 유저 차단
    
    ```tsx
    POST /users/blocks/{nickname}
    201 CREATED
    400 - 기타 에러
    401 - 로그인 리다이렉션
    ```
    
4. 유저 차단 해제
    
    ```tsx
    DELETE /users/blocks/{nickname}
    200 OK
    400 - 기타 에러
    401 - 로그인 리다이렉션
    ```
