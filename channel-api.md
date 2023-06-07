## 채널 관련 API

1.  채널 목록 조회

    ```ts
    GET /channels?page={page}&count={count}&order={'recent' | 'popular'}&keyword={keyword | null}
    response body {
    	channels: [
    		{
    			id: string;
    			title: string; (중복 없음)
    			access: 'public' | 'protected';
    			headCount: number;
    			maxCount: number;
    		},
    	]
    	currentPage: number;
    	totalPage: number;
    }
    response header {
    	200: ok;
    }
    ```

2.  채널 참여자 목록 조회

    ```ts
    GET /channels/{roomId}/participants
    response body {
    	me: {
    		nickname: string;
    		imgUrl: string;
    		roleType: 'owner' | 'admin' | 'normal';
    		isMuted: boolean;
    	}
    	participants: [
    		{
    			nickname: string;
    			imgUrl: string;
    			roleType: 'owner' | 'admin' | 'normal';
    			isMuted: boolean;
    		}...
    	];
    	headCount: number;
    	maxCount: number;
    }
    response header {
    	200: ok;
    }
    ```

3.  채널 생성

    ```ts
    POST /channels
    request body {
    	title: string;
    	access: public | private;
    	password: null | string;
    	maxCount: number;
    }
    response header {
    	200: ok;
    	400: title taken;
    }
    ```

4.  채널 수정

    ```ts
    PATCH /channels/{roomId}
    request body {
    	password: null | string;
    	access: public | private;
    }
    response header {
    	200: ok;
    }
    ```

5.  채널 삭제

    ```ts
    DELETE /channels/{roomId}
    response header {
    	200: ok;
    }
    ```

6.  채널 입장

    ```ts
    POST /channels/{roomId}/participants
    request body {
        password: null | string;
    }
    response header {
    	200: ok;
    	400: full bang | wrong password | private | no bang;
    }
    ```

7.  채널 퇴장

    ```ts
    DELETE /channels/{roomId}/participants
    response header {
    	200: ok;
    	400: no bang;
    }
    ```

8.  채널 초대

    ```ts
    POST /channels/{roomId}/invitation/{nickname}
    response header {
    	200: ok;
    	400: no bang;
    }
    ```

9.  채널 초대 수락->입장

    ```ts
    POST /channels/{roomId}/magicpass
    response header {
    	200: ok;
        400: full bang | no bang;
    }
    ```

10. 채팅 전송

    ```ts
    POST /channels/{roomId}/chats
    response body {
    	message: string;
    }
    response header {
    	200: ok;
    	400: no bang;
    }
    ```

11. 관리자 / owner 권한 (킥 / 벤 / 뮤트)

    ```ts
    POST /channels/{roomId}/admin/{nickname}
    response header {
    	200: ok;
    	400: no bang | error;
    }
    ```

    ```ts
    DELETE /channels/{roomId}/admin/{nickname}
    response header {
    	200: ok;
    	400: no bang | error;
    }
    ```
   
    ```ts
    POST /channels/{roomId}/ban/{nickname}
    response header {
    	200: ok;
    	400: no bang | error;
    }
    ```

    ```ts
    POST /channels/{roomId}/kick/{nickname}
    response header {
    	200: ok;
    	400: no bang | error;
    }
    ```

    ```ts
    POST /channels/{roomId}/mute/{nickname}
    response header {
    	200: ok;
    	400: no bang | error;
    }
    ```

    ```ts
    DELETE /channels/{roomId}/mute/{nickname}
    response header {
    	200: ok;
    	400: no bang | error;
    }
    ```

12. 내가 속해있는 방

    ```ts
    GET /channels/me
    response body {
    	myChannel: {
    		id: string;
    		title: string; (중복 없음)
    		headCount: number;
    		maxCount: number;
    	} | null;
    }
    response header {
    	200: ok;
    }
    ```
    
13. 채팅 내역 불러오기
	```ts
	GET /channels/{roomId}chats?offset={offset}&count={count}
	response body {
		chats: [
			{
				id: number;
				message: string; // system인 경우 'mute', 'unmute', 'setadmin', 'unsetadmin', 'kick', 'ban'
				nickname: string; // system일 경우 당한사람
				createdAt: Date;
				type: 'me' | 'others' | 'system';
			}, ...
		],
		isLastPage: boolean;
	}
	response header {
		200: ok;
	}
	```
	

 
