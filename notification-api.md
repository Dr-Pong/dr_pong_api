## Notifications
1. 친구 요청 개수
    ```ts
    GET /users/notifications/friends
    response body {
	    friendRequest: number; // 친구 요청이 없으면 0 요청 최대50개만 가능
    }
    ```
2. 게임 초대
    ```ts
    GET /users/notifications/games
    response body {
        invitations: [
		{
		    id: string;
		    from: string;
		    createdAt: date;
		},
		...
        ]
    }
    ```
3. 채널 초대
    ```ts
    GET /users/notifications/channels
    response body {
        invitations: [
            {
                id: string;
                channelId: number;
                channelName: string;
                from: string;
                createdAt: date;
            },
            ...
        ]
    }
    ```
4. 게임 초대 삭제
    ```ts
    DELETE /users/notifications/games/{id}
    response header {
	    200: ok;
	    400: error;
    }
    ```
5. 채널 초대 삭제
    ```ts
    DELETE /users/notifications/channels/{id}
    response header {
	    200: ok;
	    400: error;
    }
    ```
