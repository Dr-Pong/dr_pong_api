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
