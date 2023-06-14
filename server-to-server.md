## GateWay to WebServer

```ts
POST /users
request body {
    id: number;
    nickname: string;
    imgId: number;
    imgUrl: string;
}
response{
  201: created;
}

```

## GateWay to ChatServer
```ts
POST /users
request body {
    id: number;
    nickname: string;
    imgId: number;
    imgUrl: string;
}
response{
  201: created;
}
```

```ts
PATCH /users/{nickname}/image
request body {
	id: number;
}
response header {
	202: accepted;
	401: unauthorized;
}
```
