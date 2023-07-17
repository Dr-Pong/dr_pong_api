## GAME 관련 API

1. Queue 입장
```ts
  POST /games/queue/{type}
  request body {
    mode: string;
  }
  response header {
    201: ok;
  }
```

2. Queue 퇴장
```ts
  DELETE /games/queue
  response header {
    200: ok;
  }
```
