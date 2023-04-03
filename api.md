# Api 설계

## Login

## Main

## Layout

```
GET /users/me
{
  nickname: string,
	imgUrl: string,
}
```

## MyPage

업적 미완

```
GET /users/details/{user}

{
	nickname: string,
	imgUrl: string,
	level: number,
	title: string | null,
	statusMessage: string,
	totalStat: {
		winRate: number,
		win: number,
		lose: number,
	},
	seasonStat: {
		winRate: number,
		win: number,
		lose: number,
		bestRecord: number,
	},
	achievements: [string | null],
}
```

```
GET /users/achievements/{user}
{
	achievements: [
		{
			name: string,
			imgUrl: string,
			content: string,
			status: string // ("selected", "achieved", "unachieved"),
		}
	]
}
```

```
GET /users/emojies/{user}
{
	emojies: [
		{
			name: string,
			imgUrl: string,
			selected: boolean,
		}
	]
	// 사용자가 선택한 이모지를 담는 객체 추가 필요
}
```

```
GET /users/titles/{user}
{
	titles: [string],
}
```

```
PATCH /users/details/{user}
{
	imgUrl: multipartFile | null,
	title: string,
	message: string,
}
```

```
PATCH /users/achievements/{user}
{
	achievements: [string]
}
```

```
PATCH /users/emojies/{user}
```

## Rank

```
GET /ranks/season
{
  seasonName: string,
}
```

```
GET /ranks/top?count={count} // top의 count
{
	top: [
		{
			rank: number,
			nickname: string,
			pongPower: number,
			imgUrl: string,
		}
	],
}
```

```
GET /ranks/bottom?offset={offset} // bottom의 시작점
{
	bottom: [
		{
			rank: number,
			nickname: string,
			pongPower: number,
		}
	],
}
```

## RecentGames

```
GET /records/{user}
{
	key: {
		imgUrl: string,
		nickname: string,
	},
}
```

```
GET /records/lists/{user}?lastGameId={lastGameId}?count={count}
{
	records: [
		{
			gameId: number,
			gameType: string, // ("rank", "normal")
			opponent: {
				imgUrl: string,
				nickname: string,
			},
			keyScore: number,
      opponentScore: number,
			playedAt: string, // 게임이 끝난 시간
			result: string, // ("win", "lose", "tie")
		}
	]
}
```

```
GET /records/details?gameId={gameId}
{
	duration: number, // 초
  leftPongPower: number,
	leftChange: number,
	rightPongPower: number,
	rightChange: number,
	rounds: [
		{
			bounces: number,
			isLeftWin: boolean,
		}
	],
}

```

```
GET /records/search?
```
