## 채널 관련 API

1.  채널 목록 조회

    ```json
    GET /channels?page={page}&count={count}&order={'recent' | 'popular'}&keyword={keyword | null}
    response body: {
    		channels: [
    				{
    			id: number;
    			title: string; (중복 없음)
    			access: 'public' | 'protected';
    			headCount: string;
    			maxCount: string;
    					},
    		]
    		currentPage: number;
    		totalPage: number;
    }
    response header: {
    		200: ok;
    }
    ```

2.  채널 참여자 목록 조회

    ```json
    GET /channels/{roomId}/participants
    	response body: {
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
    			]
    			headCount: string;
    			maxCount: string;
    	}
    	response header: {
    			200: ok;
    	}
    ```

3.  채널 생성

    ```json
    POST /channels
    	request body: {
    		title: string;
    		access: public | private;
    		password: null | string;
    		maxCount: number;
    	}
    	response header: {
    		200: ok;
    		400: title taken;
    	}
    ```

4.  채널 수정

    ```json
    PATCH /channels/{roomId}
    request body: {
    		password: null | string;
    		access: public | private;
    }
    response header: {
    		200: ok;
    }
    ```

5.  채널 삭제

    ```json
    DELETE /channels/{roomId}
    response header: {
    		200: ok;
    }
    ```

6.  채널 입장

    ```json
    POST /channels/{roomId}/participants
    request body: {
        password: null | string;
    }
    response header: {
    		200: ok;
    		400: full bang | wrong password | private | no bang;
    }
    ```

7.  채널 퇴장

    ```json
    DELETE /channels/{roomId}/participants
    response header: {
    		200: ok;
    		400: no bang;
    }
    ```

8.  채널 초대

    ```json
    POST /channels/{roomId}/invitation/{nickname}
    response header: {
    		200: ok;
    		400: no bang;
    }
    ```

9.  채널 초대 수락->입장

    ```json
    POST /channels/{roomId}/magicpass
    response header: {
    	200: ok;
        400: full bang | no bang;
    }
    ```

10. 채팅 전송

    ```json
    POST /channels/{roomId}/chat
    response body: {
    	message: string;
    }
    response header: {
    	200: ok;
    		400: no bang;
    }
    ```

11. 관리자 / owner 권한 (킥 / 벤 / 뮤트)

    ```json
    POST /channels/{roomId}/ban/{nickname}
    response header {
    	200: ok;
    	400: no bang | error;
    }
    ```

    ```json
    POST /channels/{roomId}/kick/{nickname}
    response header {
    	200: ok;
    	400: no bang | error;
    }
    ```

    ```json
    POST /channels/{roomId}/mute/{nickname}
    response header {
    	200: ok;
    	400: no bang | error;
    }
    ```

    ```json
    DELETE /channels/{roomId}/mute/{nickname}
    response header {
    	200: ok;
    	400: no bang | error;
    }
    ```

12. 내가 속해있는 방

    ```json
    GET /channels/me
    response body: {
    	myChannel: {
    		id: number;
    		title: string; (중복 없음)
    		headCount: string;
    		maxCount: string;
    	} | null;
    }
    response header {
    	200: ok;
    }
    ```
