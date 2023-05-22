# Api 설계

```ts
GET /users/{nickname}/detail
response body {
	nickname: string;
	image: {
		id: number;
		url: string;
	};
	level: number;
	title: {
		id: number;
		title: string;
	} | null;
	statusMessage: string;
}
response header {
	200: OK;
}
```

```ts
GET /users/{nickname}/stats/total
response body {
	winRate: number;
	wins: number;
	ties: number;
	loses: number;
}
response header {
	200: OK;
}
```

```ts
GET /users/{nickname}/stats/season
response body {
	winRate: number;
	wins: number;
	ties: number;
	loses: number;
}
response header {
	200: OK;
}
```

```ts
GET /users/{nickname}/ranks/total
response body {
	record: number | null;
	rank: number | null;
	tier: 'doctor' | 'master' | 'bachelor' | 'student' | 'egg';
}
response header {
	200: OK;
}
```

```ts
GET /users/{nickname}/ranks/season
response body {
	record: number | null;
	rank: number | null;
	tier: 'doctor' | 'master' | 'bachelor' | 'student' | 'egg';
}
response header {
	200: OK;
}
```

```ts
GET /users/images
response body {
	images: [
		{
			id: number;
			url: string;
		}
	]
}
response header {
	200: OK;
}
```

```ts
GET /users/{nickname}/achievements?selected={true} // selected만 줌
response body {
	achievements: [
		{
			id: number;
			name: string;
			imgUrl: string;
			content: string;
			status: 'selected' | 'achieved' | 'unachieved';
		} | null
	]
}
response header {
	200: OK;
}
```

```ts
GET /users/{nickname}/emojis?selected={true} // selected만 줌
response body {
	emojis: [
		{
			id: number;
			name: string;
			imgUrl: string;
			status: 'selected' | 'achieved' | 'unachieved';
		} | null
	]
}
response header {
	200: OK;
}
```

```ts
GET /users/{nickname}/titles
response body {
	titles: [
		{
			id: number;
			title: string;
		}
	]
}
response header {
	200: OK;
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

```ts
PATCH /users/{nickname}/title
request body {
	id: number | null;
}
response header {
	202: accepted;
	401: unauthorized;
}
```

```ts
PATCH /users/{nickname}/message
request body {
	message: string;
}
response header {
	202: accepted;
	401: unauthorized;
}
```

```ts
PATCH /users/{nickname}/achievements
request body {
	ids: [number | null];
}
response header {
	202: accepted;
	401: unauthorized;
}
```

```ts
PATCH /users/{nickname}/emojis
request body {
	ids: [number | null];
}
response header {
	202: accepted;
	401: unauthorized;
}
```

## Rank

```ts
GET /seasons/current
response body {
	seasonName: string;
}
```

```ts
GET /ranks/top?count={count} // count: top의 개수
response body {
	top: [
		{
			rank: number;
			nickname: string;
			lp : number;
			imgUrl: string;
		}
	];
}
```

```ts
GET /ranks/bottom?count={count}&offset={offset} // offset: bottom rank의 시작 번호
response body {
	bottom: [
		{
			rank: number;
			nickname: string;
			lp: number;
		}
	];
}
```

## Record

```ts
GET /users/{nickname}/records?count={count}&lastGameId={lastGameId}
response body {
	records: [
		{
			gameId: number;
			gameType: 'rank' | 'normal';
			playedAt: string; // 게임이 끝난 시간
			me: {
				imgUrl: string;
				nickname: string;
				score: number;
			};
			you: {
				imgUrl: string;
				nickname: string;
				score: number;
			};
			result: 'win', 'lose', 'tie';
		}
	]
	isLastPage: boolean;
}

```

```ts
GET /users/{nickname}/records/{gameId}
response body {
	duration: number; // 초
	me: {
		lp: number;
		lpChange: number;
	}
	you: {
		lp: number;
		lpChange: number;
	}
	rounds: [
		{
			bounces: number;
			meWin: boolean;
		}
	];
}

```
