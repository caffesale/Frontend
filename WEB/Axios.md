# Axios란?

Axios는 fetch, ajax와 마찬가지로 비동기, 서버와의 통신을 처리하기 위한 서드파티 라이브러리이다. 여기에서는 fetch api와 비교해 어떤 차이점이 있는지를 주로 기술한다.

## Axios / fetch 요청방식
[출처](https://axios-http.com/kr/docs/post_example)

```javascript
// Axios는 fetch와 마찬가지로 인자에 url, 객체를 담아 요청할수도 있지만 방법이 좀 더 다양하다.

const axios = require('axios');

//GET

axios.get('/user?ID=12345')
  .then(function (response) {
    // 성공 핸들링
    console.log(response);
  })
  
//POST

axios.post('/user', {
    firstName: 'Fred',
    lastName: 'Flintstone'
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
  
//여러 POST요청을 한꺼번에 하기

function getUserAccount() {
  return axios.get('/user/12345');
}

function getUserPermissions() {
  return axios.get('/user/12345/permissions');
}

Promise.all([getUserAccount(), getUserPermissions()])
  .then(function (results) {
    const acct = results[0];
    const perm = results[1];
  });
```
## 데이터 형식

```javascript
// fetch는 json포맷으로 받아오지 않기에 response에 대해 .json()처리를 해 주어야 한다. 

fetch(url)
  .then((response) => response.json())
  
// axios는 기본 값으로 json 타입이 설정되어 있다.

axion(url)
  .then(response => response.data)
```

## 인터셉터

```javascript
// axios는 요청이 보내지거나 받아지기 직전에 인터셉터를 추가해 임의의 작업을 수행시킬 수 있다. 

// 요청 인터셉터 추가하기
axios.interceptors.request.use(function (config) {
    // 요청이 전달되기 전에 작업 수행
    return config;
  }, function (error) {
    // 요청 오류가 있는 작업 수행
    return Promise.reject(error);
  });

// 응답 인터셉터 추가하기
axios.interceptors.response.use(function (response) {
    // 2xx 범위에 있는 상태 코드는 이 함수를 트리거 합니다.
    // 응답 데이터가 있는 작업 수행
    return response;
  }, function (error) {
    // 2xx 외의 범위에 있는 상태 코드는 이 함수를 트리거 합니다.
    // 응답 오류가 있는 작업 수행
    return Promise.reject(error);
  });
```

## 요청 취소
```javascript

//axios는 CalcelToken을 통해 요청을 도중에 취소할 수 있다. 

const CancelToken = axios.CancelToken;
const source = CancelToken.source();

axios.get('/user/12345', {
  cancelToken: source.token
}).catch(function (thrown) {
  if (axios.isCancel(thrown)) {
    console.log('Request canceled', thrown.message);
  } else {
    // 에러 핸들링
  }
});

axios.post('/user/12345', {
  name: 'new name'
}, {
  cancelToken: source.token
})

// 요청 취소하기 (메시지 파라미터는 옵션입니다)
source.cancel('Operation canceled by the user.');
```
