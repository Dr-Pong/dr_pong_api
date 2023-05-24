## Profile
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
