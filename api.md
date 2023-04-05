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
GET /users/{nickname}/detail
{
	"nickname": string;
	"imgUrl": string;
	"level": number;
	"title": string | null;
	"statusMessage": string;
}
```

```ts
GET /users/{nickname}/stat
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
GET /users/{nickname}/achievements?selected={true} // selected만 줌
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
GET /users/{nickname}/emojies?selected={true} // selected만 줌
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
GET /users/{nickname}/titles
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
PATCH /users/detail
{
	"imgUrl": file(formData) | null;
	"title": number;
	"message": string;
}
```

```ts
PATCH /users/achievements
{
	"achievements": [number]
}
```

```ts
PATCH /users/emojies
{
	"emojies": [number]
}
```

## Rank

```ts
GET /seasons/current
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
GET /ranks/bottom?count={count}&offset={offset} // offset: bottom rank의 시작 번호
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
GET /records/key/{nickname}
{
	"keyPlayer": {
		"imgUrl": string;
		"nickname": string;
	};
}
```

```ts
GET /records/list?count={count}&nickname={nickname}&lastGameId={lastGameId}
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
GET /records/{gameId}/detail
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
