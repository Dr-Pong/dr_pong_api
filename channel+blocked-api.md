## 채팅방 관련 API
1. 채팅방 목록 조회
    ```tsx
    GET /channels?page={page}&count={count}&order={'recent' | 'popular'}&keyword={keyword | null}
    response body: {
	    channels: [
	        {
		    id: number;
		    title: string; (중복 없음)
		    access: 'public' | 'protected'; // private 은 1:1 디엠 으로~~!
		    headCount: string;
		    maxCount: string;
	         }, ...
	    ]
	    currentPage: number;
	    totalPage: number;
    }
    ```
2. 채팅방 참여자 목록 조회
    ```tsx
    GET /channels/{roomId}/participants
    response body: {
        participants: [
            {
                nickname: string;
                imgUrl: string;
                roleType: 'owner' | 'admin' | 'normal';
            }
        ]
        headCount: string;
        maxCount: string;
    }
    ```

4. 채팅방 생성
    ```tsx
    POST /channels
    request body: {
        title: string;
        password: null | string;
        maxCount: number;
    }
    ```

5. 채팅방 수정
    ```tsx
    PATCH /channels/{roomId}
    request body: {
        password: null | string;
    }
    ```

6. 채팅방 삭제
    ```tsx
    DELETE /channels/{roomId}
    ```
7. 채팅방 입장

    ```tsx
    POST /channels/{roomId}/participants
    request body: {
        password: null | string;
    }
    response header: {

    }
    ```
8. 채팅방 퇴장
    ```tsx
    DELETE /channels/{roomId}/participants
    ```
9. 채팅방 초대
    ```tsx
    POST /channels/{roomId}/invitation/{nickname}
    ```
10. 채팅방 초대 수락
    ```tsx
    POST /channels/{roomId}/magicpass
    ```
11. 채팅 전송
    ```tsx
    POST /channels/{roomId}/chat
    response body: {
        message: string;
    }
    response header: {

    }
    ```
12. 관리자 / owner 권한 (킥 / 벤 / 뮤트)
    ```tsx
    POST /channels/{roomId}/ban/{nickname}
    ```

    ```tsx
    POST /channels/{roomId}/kick/{nickname}
    ```

    ```tsx
    POST /channels/{roomId}/mute/{nickname}
    ```

    ```jsx
    DELETE /channels/{roomId}/mute/{nickname}
    ```

## 차단 관련 API
1. 차단 목록 조회
    ```tsx
    GET /blocks
    response body: {
        users: [
            {
                nickname: string;
                imgUrl: string;
            }, ...
        ]
    }
    ```
2. 유저 차단
    ```tsx
    POST /users/blocks/{nickname}
    201 CREATED
    400 - 기타 에러
    401 - 로그인 리다이렉션
    ```
3. 차단 해제
    ```tsx
    DELETE /users/blocks/{nickname}
    200 OK
    400 - 기타 에러
    401 - 로그인 리다이렉션
    ```
