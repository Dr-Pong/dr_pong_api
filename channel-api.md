## 채널 관련 API
1. 채널 목록 조회
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
	         }, 
	    ]
	    currentPage: number;
	    totalPage: number;
    }
    response header: {
    }
    ```
2. 채널 참여자 목록 조회
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
    response header: {
    }
    ```

4. 채널 생성
    ```tsx
    POST /channels
    request body: {
        title: string;
        password: null | string;
        maxCount: number;
    }
    response header: {
이미 있는 이름
안되는 패스워드
안되는 카운트
    }
    ```

5. 채널 수정
    ```tsx
    PATCH /channels/{roomId}
    request body: {
        password: null | string;
    }
    response header: {
    안되는 비번
    }
    ```

6. 채널 삭제
    ```tsx
    DELETE /channels/{roomId}
    response header: {
    실패
    }
    ```
7. 채널 입장

    ```tsx
    POST /channels/{roomId}/participants
    request body: {
        password: null | string;
    }
    response header: {
    실패
    없는 방
    
    }
    ```
8. 채널 퇴장
    ```tsx
    DELETE /channels/{roomId}/participants
    response header: {
    실패
    없는 방
    
    }
    ```
9. 채널 초대
    ```tsx
    POST /channels/{roomId}/invitation/{nickname}
    response header: {
    실패
    없는 방
    권한 없음(친구 아님?)
    }
    ```
10. 채널 초대 수락->입장
    ```tsx
    POST /channels/{roomId}/magicpass
    response header: {
    실패
    없는 방

    }
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
