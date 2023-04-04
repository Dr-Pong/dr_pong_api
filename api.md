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

```ts
GET /users/details/{nickname}
{
	"nickname": string;
	"imgUrl": string;
	"level": number;
	"title": string | null;
	"statusMessage": string;
}
```

```ts
GET /users/stats/{nickname}
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
GET /users/achievements/{nickname}?selected={true} // selected만 줌
{
	"achievements": [
		{
			"id": number;
			"name": string;
			"imgUrl": string;
			"content": string;
			"status": string // ("selected", "achieved", "unachieved");
		}
	]
}
```

```ts
GET /users/emojies/{nickname}?selected={true} // selected만 줌
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
GET /users/titles/{nickname}
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
PATCH /users/details/{nickname}
{
	"imgUrl": file(formData) | null;
	"title": number;
	"message": string;
}
```

```ts
PATCH /users/achievements/{nickname}
{
	"achievements": [number]
}
```

```ts
PATCH /users/emojies/{nickname}
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
	"keyPlayer": {
		"imgUrl": string;
		"nickname": string;
	};
}
```

```ts
GET /records/lists/{user}?count={count}&lastGameId={lastGameId}
{
	"records": [
		{
			"gameId": number;
			"gameType": string; // ("rank", "normal")
			"playedAt": string; // 게임이 끝난 시간
			"result": string; // ("win", "lose", "tie")
			"opponent": {
				"imgUrl": string;
				"nickname": string;
			};
			"keyPlayerScore": number;
			"opponentScore": number;
		}
	]
}
```

```ts
GET /records/details?gameId={gameId}
{
	"duration": number; // 초
	"keyPlayerPongPower": number;
	"KeyPlayerChange": number;
	"opponentPongPower": number;
	"opponentChange": number;
	"rounds": [
		{
			"bounces": number;
			"isKeyPlayerWin": boolean;
		}
	];
}

```

```ts
GET /records/search?
```
