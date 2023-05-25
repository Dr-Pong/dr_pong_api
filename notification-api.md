## Notifications
1. 친구 요청 개수
    ```ts
    GET /users/notifications/friends
    response body {
	    friendRequest: number; // 친구 요청이 없으면 0
    }
    ```
2. 게임 초대
    ```ts
    GET /users/notifications/games
    response body {
	    invitations: [
		    {
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
			    channelId: number;
			    channelName: string;
			    from: string;
			    createdAt: date;
		    },
		    ...
	    ]
    }
    ```
