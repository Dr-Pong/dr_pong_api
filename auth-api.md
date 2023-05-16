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
