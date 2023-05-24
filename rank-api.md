
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
