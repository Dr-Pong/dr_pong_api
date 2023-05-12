# Api 설계

## Login
```ts
POST /auth/42 | /auth/google
request body: {
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

## Authentication
```ts
GET /auth/tfa
request body: {
}
response body: {
	redirectionUrl: string;
	qrCode: string;
	secretKey: string;
}
response header: {
	201: created;
	401: unauthorized; // no token
}
```
```ts
DELETE /auth/tfa
response body: {
}
response header: {
	200: OK!
	401: unauthorized; // no token
}
````
```ts
POST /auth/tfa/otp
request body: {
	password: string; 
}
response header: {
	200: OK;
	40~:
}
response body: {
	accessToken: string;
}
````
## User
```ts
GET /users/me
{
	"nickname": string;
	"imgUrl": string;
	"tfaRequired": boolean; // 수정
	"roleType": 'guest' | 'noname' | 'member' | 'admin';
}
response header: {
	200: OK;
}
```
```ts
GET /users/{nickname}/tfa
response body: {
	tfaOn: boolean;
}
```
```ts
GET /users/{nickname}/detail
{
	"nickname": string;
	"image": {
		"id": number;
		"url": string;
	};
	"level": number;
	"title": {
		"id": number;
		"title": string;
	} | null;
	"statusMessage": string;
}
response header: {
	200: OK;
}
```

```ts
GET /users/{nickname}/stats/total
{
	"winRate": number;
	"wins": number;
	"ties": number;
	"loses": number;
}
response header: {
	200: OK;
}
```

```ts
GET /users/{nickname}/stats/season
{
	"winRate": number;
	"wins": number;
	"ties": number;
	"loses": number;
}
response header: {
	200: OK;
}
```

```ts
GET /users/{nickname}/ranks/total
{
	"record": number | null;
	"rank": number | null;
	"tier": 'doctor' | 'master' | 'bachelor' | 'student' | 'egg';
}
response header: {
	200: OK;
}
```

```ts
GET /users/{nickname}/ranks/season
{
	"record": number | null;
	"rank": number | null;
	"tier": 'doctor' | 'master' | 'bachelor' | 'student' | 'egg';
}
response header: {
	200: OK;
}
```
```ts
GET /users/images
{
	"images": [
		{
			"id": number;
			"url": stirng;
		}
	]
}
response header: {
	200: OK;
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
	200: OK;
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
	200: OK;
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
	200: OK;
}
```

```ts
PATCH /users/{nickname}/image
request: {
	"id": number;
}
response header: {
	202: accepted;
	401: unauthorized;
}
```

```ts
PATCH /users/{nickname}/title
request: {
	"id": number | null;
}
response header: {
	202: accepted;
	401: unauthorized;
}
```

```ts
PATCH /users/{nickname}/message
request: {
	"message": string;
}
response header: {
	202: accepted;
	401: unauthorized;
}
```

```ts
PATCH /users/{nickname}/achievements
request: {
	"ids": [number | null]
}
response header: {
	202: accepted;
	401: unauthorized;
}
```

```ts
PATCH /users/{nickname}/emojis
request: {
	"ids": [number | null]
}
response header: {
	202: accepted;
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
			"lp" : number;
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
			"lp": number;
		}
	];
}
```

## Record

```ts
GET /users/{nickname}/records?count={count}&lastGameId={lastGameId}
{
	"records": [
		{
			"gameId": number;
			"gameType": string; // ("rank", "normal")
			"playedAt": string; // 게임이 끝난 시간
			"me": {
				"imgUrl": string;
				"nickname": string;
				"score": number;
			};
			"you": {
				"imgUrl": string;
				"nickname": string;
				"score": number;
			};
			"result": string; // ("win", "lose", "tie")
		}
	]
	"isLastPage": boolean;
}

```

```ts
GET /users/{nickname}/records/{gameId}
{
	"duration": number; // 초
	"me": {
		"lp": number;
		"lpChange": number;
	}
	"you": {
		"lp": number;
		"lpChange": number;
	}
	"rounds": [
		{
			"bounces": number;
			"meWin": boolean;
		}
	];
}

```

```ts
GET /records/search?
```
