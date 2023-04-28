# Api 설계

## Login
```ts
POST /auth/42 | /auth/google
request: {
	"authCode": string;
}
response header: {
	201: created;
	401: unauthorized;
}
response body: {
	"accessToken": string;
}
```
## SignUp
```ts
POST /signup
request: {
	"nickname": string;
	"imgId": number;
}
response header: {
	201: created;
	400: bad request;
	401: unauthorized;
	409: 닉네임 중복;
}
```

## Main

## Layout

```ts
GET /users/me
{
	"nickname": string;
	"imgUrl": string;
	"isSecondAuthOn": boolean;
	"roleType": 'guest' | 'noname' | 'member' | 'admin';
}
response header: {
	200: created;
	401: unauthorized;
}
```

## MyPage

```ts
GET /users/{nickname}/detail
{
	"nickname": string;
	"imgUrl": string;
	"level": number;
	"title": {
		"id": number;
		"title": string;
	} | null;
	"statusMessage": string;
}
response header: {
	200: created;
	401: unauthorized;
}
```

```ts
GET /users/{nickname}/stat
{
	"totalStat": {
		"winRate": number;
		"win": number;
		"ties": number;
		"lose": number;
	};
	"seasonStat": {
		"winRate": number;
		"win": number;
		"ties": number;
		"lose": number;
		"record": number | null;
		"rank": number | null;
	};
	"bestStat": { //역대최고를 
		"record": number | null;
		"rank": number | null;
	};
}
response header: {
	200: created;
	401: unauthorized;
}
```
```ts
GET /users/images
{
	"images": [
		{
			"id": number;
			"imgUrl": stirng;
		}
	]
}
response header: {
	200: created;
	401: unauthorized;
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
		} | null
	]
}
response header: {
	200: created;
	401: unauthorized;
}
```

```ts
GET /users/{nickname}/emojis?selected={true} // selected만 줌
{
	"emojis": [
		{
			"id": number;
			"name": string;
			"imgUrl": string;
			"status": string // ("selected", "achieved", "unachieved");
		} | null
	]
}
response header: {
	200: created;
	401: unauthorized;
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
response header: {
	200: created;
	401: unauthorized;
}
```

```ts
PATCH /users/{nickname}/detail
request: {
	"imgId": number | null;
	"title": number | null;
	"message": string;
}
response header: {
	202: created;
	401: unauthorized;
}
```

```ts
PATCH /users/{nickname}/achievements
request: {
	"achievements": [number | null]
}
response header: {
	202: created;
	401: unauthorized;
}
```

```ts
PATCH /users/{nickname}/emojis
request: {
	"emojis": [number | null]
}
response header: {
	202: created;
	401: unauthorized;
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
