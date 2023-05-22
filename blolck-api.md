## 차단 관련 API

1. 차단 목록 조회
   ```ts
   GET /blocks
   response body {
       users: [
           {
               nickname: string;
               imgUrl: string;
           }, ...
       ];
   }
   ```
2. 유저 차단
   ```ts
   POST /users/blocks/{nickname}
   response header {
   	200: ok;
   	400: error;
   }
   ```
3. 차단 해제
   ```ts
   DELETE /users/blocks/{nickname}
   response header {
   	200: ok;
   	400: error;
   }
   ```
