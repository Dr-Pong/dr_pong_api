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


## GameServer to WebServer
```ts

POST /games
request body {
player1: {
		id: number;
		score: number;
		lpChange: number;
	};
player2: {
		id: number;
		score: number;
		lpChange: number;
	};
mode: 'SFINAE' | 'NON-SFINAE';
type: 'rank' | 'normal';
startTime: Date;
endTime: Date;
logs: {
	userId: number;
	event: 'touch' | 'score';
	round: number;
	ball: {
		speed: number;
		direction: {x:number, y:number};
		position: {x:number, y:number};
		spinSpeed: number;
		}
	}[];
}
```


