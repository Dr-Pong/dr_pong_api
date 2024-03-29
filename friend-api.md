## 친구 관련 API

1.  친구 목록 조회

    ```ts
    GET /users/friends
    response body {
    	users: [
    		{
    			nickname: string;
    			imgUrl: string;
    		}, ...
    	] // 정렬 알파벳순
    }
    response header {
    	200: ok;
    }
    ```

2.  친구 요청

    ```ts
    POST /users/friends/pendings/{nickname}
    response header {
    	201: ok;
    	400: error;
    } // 요청을 둘다 보냈을 경우 친구 수락
    ```

3.  친구 요청 목록 조회 (pending list)

    ```ts
    GET /users/friends/pendings
    response body {
    	users: [
    		{
    			nickname: string;
    			imgUrl: string;
    		}, ...
    	] // 정렬 알파벳순
    }
    response header {
    	200: ok;
    }
    ```

4.  친구 요청 수락

    ```ts
    POST /users/friends/{ nickname };
    response header {
    	201: ok;
    }
    ```

5.  친구 요청 거절

    ```ts
    DELETE /users/friends/pendings/{ nickname };
    response header {
    	200: ok;
    }
    ```

6.  친구 삭제

    ```ts
    DELETE /users/friends/{nickname}
    response header {
    	200: ok;
    }
    ```

7.  DM 대화 내역 - 쿼리 어떻게 할지 고민 필요

    ```ts
    GET /users/friends/{nickname}/chats?offset={offset}&count={count}
    response body {
	    chats: [
			{
				id: number;
				message: string;
				nickname: string;
				time: Date;
				type: 'me' | 'others';
			}, ...
		],
    	isLastPage: boolean;
    }
    response header {
	    200: ok;
    }
    ```

8.  DM 전송

    ```ts

    POST /users/friends/{nickname}/chats
    request body {
    	message: string;
    }
    response header {
    	201: ok;
    	400: not friend;
    }
    ```

9.  진행 중인 DM 목록 받기

    ```ts
    GET /users/friends/chatlist
    response body {
    	chatList: [
    		{
    			nickname: string;
    			imgUrl: string;
    			newChats: number;
    		}
    	]...;
    }
    ```

10. 진행 중인 DM 리스트에서 특정 방 삭제

    ```ts
    DELETE /users/friends/chats/{nickname}
    response header {
    	200: ok;
    }
    ```

11. 새로운 DM 유무 확인

    ```ts
    GET /users/friends/chats/new
    response body {
        hasNewChat: boolean;
    }
    ```

12. 관계 조회 api

    ```ts
    /users/{nickname}/relations/{targetnickname}
    respone body : {
	status: "none" | "blocked" | "friend" | "me";
    }
    ```
