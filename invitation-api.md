1. Game 초대
```ts
POST /invitations/games
    resquest body {
       mode: string;
       nickname: string;
    }
    response header {
        201: ok;
        400: no such user | unavailable(offline / ingame);
    }
```

2. Game 초대 취소
```ts
DELETE /invitations/games
  response header {
    201: ok;
    400: no such user | unavailable(offline / ingame);
  }
```

3. Game 초대 수락
```ts
PATCH invitations/games/{id} // invitation ID
  response body {
     gameId: string;
  }
  response header {
     201: ok;
     400: no bang;
  }
```

4. Game 초대 거절
```ts
  DELETE /invitations/games/{id} // invitation ID
  response header {
    200: ok;
  }
```

5.  채널 초대

    ```ts
    POST /invitations/channels/{roomId}
    request body {
        nickname: string;
    }
    response header {
    	201: ok;
    	400: no bang;
    }
    ```

6.  채널 초대 수락->입장

    ```ts
    PATCH /invitations/channels/{roomId}
    response header {
    	200: ok;
        400: full bang | no bang;
    }
    ```

7. 채널 초대 거절

    ```ts
    DELETE /invitations/channels/{roomId}
    response header {
    	200: ok;
        400: error;
    }
    ```

