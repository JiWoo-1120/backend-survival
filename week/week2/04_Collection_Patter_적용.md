# CRUD
데이터에 대해 취하는 모든 기능은 다음 4개로 정리할 수 있다.
1. Create → POST
2. Read → GET
3. Update → PUT, PATCH
4. Delete → DELETE

CRUD의 중요한 특징을 두가지로 나눈 것이
# CQS
1. Command
Create, Update, Delete → 상태가 변함, 안전하지 않음
2. Query
Read → 상태가 변하지 않음, 안전함, 분산, 캐시 등이 수월함

## 게시물
1. `GET /posts` → 게시물 목록 (Read, Collection) → List (습관적인 표현 중 하나)
2. `GET /posts/{id}` → 게시물 상세 (Read, Element) → Detail (습관적인 표현 중 하나)
3. `POST /posts` → 게시물 생성 (Create) → Post ID는 서버에서 생성함.
4. `PUT 또는 PATCH /posts/{id}` → 게시물 수정 (Update, Element)
5. `DELETE /posts/{id}` → 게시물 삭제 (Delement, Element)

    종종 Bulk update, Bulk delete 등을 하기도 함
    여러개를 지울 때 사용. 이럴 때는 Collection을 활용하고,
    API 스펙 문서에 정확히 기록한다.


## 댓글
그냥 바로 comments로 시작하는 경우:

1. `GET /comments` → 전체 댓글 목록
2. `GET /comments?post_id={post_id}` → 특정 게시물에 대한 댓글 목록
3. `GET /comments/{id}` → 댓글 상세
4. `POST /comments` → 댓글 생성 ⇒ 어떤 게시물에 대해? → Body에 Post ID 정보를 담아줘야 함.
5. `POST /comments?post_id={post_id}` → 특정 게시물에 대한 댓글 생성
6. `PUT 또는 PATCH /comments/{id}` → 댓글 수정
7. `DELETE /comments/{id}` → 댓글 삭제

특정 게시물 아래로 표현하는 경우:

1. `GET /posts/{post_id}/comments` → 특정 게시물에 대한 댓글 목록
2. `GET /posts/{post_id}/comments/{id}` → 특정 게시물에 달린 특정 댓글 상세
3. `POST /posts/{post_id}/comments` → 특정 게시물에 대한 댓글 작성
4. `PUT 또는 PATCH /posts/{post_id}/comments/{id}` → 특정 게시물에 달린 특정 댓글 수정
5. `DELETE /posts/{post_id}/comments/{id}` → 특정 게시물에 달린 특정 댓글 삭제