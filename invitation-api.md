1. Game 초대
```ts
POST /games/invitation
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
DELETE /games/invitation/
  response header {
    201: ok;
    400: no such user | unavailable(offline / ingame);
  }
```

3. Game 초대 수락
```ts
PATCH /games/invitation/{id} // invitation ID
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
  DELETE /games/invitation/{id} // invitation ID
  response header {
    200: ok;
  }
```

