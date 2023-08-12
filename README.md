```
gql 및 useQuery는 @apollo/client에서 가져옴
이들은 GraphQL 쿼리를 정의하고 실행하는 데 사용
```

- GraphQL 쿼리

```javascript
const GET_MOVIE = gql`
  query getMovie($movieId: ID!) {
    movie(id: $movieId) {
      id
      title
      medium_cover_image
      rating
      isLiked @client
    }
  }
`;
```

```
gql 템플릿 리터럴을 사용하여 정의된 GraphQL 쿼리

제목, 표지 이미지, 등급, 좋아요 여부를 포함한
영화 세부 정보를 서버에서 가져옴

@client 지시문은 isLiked 가 Apollo 클라이언트
캐시에서 관리하는 로컬 필드임을 나타냄

캐시의 로컬 'isLiked' 필드를 관리하여
사용자가 서버에서 실제 변형을 수행하지 않고도
영화를 좋아하거나 싫어할 수 있도록 함
```

- RESTFul 차이

```
REST API와 달리 GraphQL API는
단일 엔드포인트를 노출하고
클라이언트가 쿼리 자체에서
데이터 요구 사항을 지정

- 효율적인 데이터 가져오기
- 유연성 및 버전 관리
- 네트워크 요청 감소
- 성찰 및 문서화
- 실시간 업데이트(구독)
- 프론트엔드 기반 개발
- 강력한 형식의 스키마
```

- EX

```javascript
query {
  user(id: "123") {
    id
    name
    email
  }
}

// Equivalent REST Endpoint
// GET /users/123
```

```javascript
query {
  user(id: "123") {
    id
    name
    posts {
      id
      title
    }
  }
}

// Equivalent REST Endpoint
// GET /users/123
// GET /users/123/posts
```

```javascript
query {
  user(id: "123") {
    id
    name
  }
  posts {
    id
    title
  }
}

// Equivalent REST Endpoint
// GET /users/123
// GET /posts
```

```javascript
mutation {
  createUser(input: { name: "John", email: "john@example.com" }) {
    id
    name
  }
}

// Equivalent REST Endpoint
// POST /users
// Body: { "name": "John", "email": "john@example.com" }
```

```javascript
subscription {
  newPost {
    id
    title
  }
}
```

> apollo 로 useQuery 사용

> 후속 렌더링에서 동일한 쿼리가 다시 실행되면 Apollo Client는 네트워크 요청을 하기 전에 먼저 캐시를 확인

```
Apollo Client와 React Query 모두 강점이 있습니다. GraphQL 중심 애플리케이션을 구축 중이고 포괄적인 GraphQL 도구가 필요한 경우 Apollo 클라이언트는 탁월한 선택입니다. API 유형에 관계없이 데이터 가져오기에 대한 보다 통합된 접근 방식을 찾고 있다면 React Query가 더 적합할 수 있습니다. 프로젝트의 아키텍처 및 요구 사항에 더 잘 맞는 라이브러리를 선택할 수 있습니다.
```
