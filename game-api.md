## GAME 관련 API

1. Game 초대
```ts
POST /games/invitation/{nickname}/{mode}
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
POST /games/invitation/{id} // invitation ID
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

5. Queue 입장
```ts
  POST /games/queue/{type}/{mode}
  response header {
    201: ok;
  }
```

6. Queue 퇴장
```ts
  DELETE /games/queue
  response header {
    200: ok;
  }
```
