# Api 설계

## Login

## Main

## Layout

```ts
GET /users/me
{
	"nickname": string;
	"imgUrl": string;
}
```

## MyPage

업적 미완

```ts
GET /users/details/{user}
{
	"nickname": string;
	"imgUrl": string;
	"level": number;
	"title": string | null;
	"statusMessage": string;
}
```

```ts
GET /users/stats/{user}
{
	"totalStat": {
		"winRate": number;
		"win": number;
		"lose": number;
	};
	"seasonStat": {
		"winRate": number;
		"win": number;
		"lose": number;
		"bestRecord": number;
	};
}
```

```ts
GET /users/achievements/{user}?selected={true} // selected만 줌
{
	"achievements": [
		{
			"id": number;
			"name": string;
			"imgUrl": string;
			"content": string;
			"status": string // ("selected"; "achieved"; "unachieved");
		}
	]
}
```

```ts
GET /users/emojies/{user}?selected={true} // selected만 줌
{
	"emojies": [
		{
			"id": number;
			"name": string;
			"imgUrl": string;
			"selected": boolean;
		}
	]
}
```

```ts
GET /users/titles/{user}
{
	"titles": [
		{
			"id": number;
			"title": string;
		}
	]
}
```

```ts
PATCH /users/details/{user}
{
	"imgUrl": file(formData) | null;
	"title": number;
	"message": string;
}
```

```ts
PATCH /users/achievements/{user}
{
	"achievements": [number]
}
```

```ts
PATCH /users/emojies/{user}
{
	"emojies": [number]
}
```

## Rank

```ts
GET /ranks/season
{
  "seasonName": string;
}
```

```ts
GET /ranks/top?count={count} // count: top의 개수
{
	"top": [
		{
			"rank": number;
			"nickname": string;
			"pongPower": number;
			"imgUrl": string;
		}
	];
}
```

```ts
GET /ranks/bottom?offset={offset} // offset: bottom rank의 시작 번호
{
	"bottom": [
		{
			"rank": number;
			"nickname": string;
			"pongPower": number;
		}
	];
}
```

## RecentGames

```ts
GET /records/{user}
{
	"key": {
		"imgUrl": string;
		"nickname": string;
	};
}
```

```ts
GET /records/lists/{user}?lastGameId={lastGameId}?count={count}
{
	"records": [
		{
			"gameId": number;
			"gameType": string; // ("rank"; "normal")
			"opponent": {
				"imgUrl": string;
				"nickname": string;
			};
			"keyScore": number;
			"opponentScore": number;
			"playedAt": string; // 게임이 끝난 시간
			"result": string; // ("win"; "lose"; "tie")
		}
	]
}
```

```ts
GET /records/details?gameId={gameId}
{
	"duration": number; // 초
	"leftPongPower": number;
	"leftChange": number;
	"rightPongPower": number;
	"rightChange": number;
	"rounds": [
		{
			"bounces": number;
			"isLeftWin": boolean;
		}
	];
}

```

```ts
GET /records/search?
```
