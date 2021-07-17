# Data-fetching library

부제: **data-fetching library가 만들어진 이유와 잘 사용하는 법**

1. 데이터의 일관성(Consistency)의 문제
2. 비동기 미들웨어 사용의 복잡함

## 기존 문제점

### 1. 데이터 일관성(Consistency)

Redux 등 상태관리 라이브러리를 사용할 때 Store를 백엔드 상태에 대한 데이터 캐시로 사용하는 경우가 대부분입니다. 데이터를 fetching 한 후 store에 저장하여 사용하는 것이죠. 하지만 이렇게 fetching 해온 데이터의 경우 시간이 지날 수록 BE의 데이터와 Consistency가 깨지기 때문에 데이터를 최신 상태로 유지하기 위해 주기적으로 호출함(polliing & refetching)으로써 FE, BE 두 곳에 존재하는 데이터 상태를 동기화하여 Data Consistency를 최대한 보장해주려고 노력합니다. 그리고 이는 추가적인 많은 코드 작성이 필요하다는 것을 의미합니다.

### 2. 비동기 미들웨어 사용의 복잡함

위에서 설명한 백엔드와의 동기화를 통한 데이터 일관성을 지키기 위해 redux-saga, redux-thunk, redux-observable등의 미들웨어들을 사용하게 됩니다. 하지만 이런 미들웨어를 사용할 경우 이미 boilerplate-heavy library에 복잡한 Layer를 또 추가하는 것이며. 뿐만 아니라 data 상태에 대한 action들을 모두 정의해야하는 필요성이 생기게 됩니다.

## Data Fetching Library의 역할

Data-Fetching Library를 사용하게 되면 Data Consistency의 문제점을 개발자의 몫에서 라이브러리의 역할로 바뀌게 됩니다.

일일히 정의해줘야할 data-fetching과 관련된 상태(Status, data, error, isFetching)를 한꺼번에 제어할 수 있으며, 주기적인 polling & refetching을 통해 BE의 상태와 동기화를 시키기 위해 노력하며, 자체 캐싱을 통해 네트워크 레이턴시 또한 줄여줍니다.

### Reference

- [https://dev.to/g_abud/why-i-quit-redux-1knl](https://dev.to/g_abud/why-i-quit-redux-1knl)
- [https://blog.bitsrc.io/how-to-start-using-react-query-4869e3d5680d](https://blog.bitsrc.io/how-to-start-using-react-query-4869e3d5680d)
- [https://react-query-v2.tanstack.com/](https://react-query-v2.tanstack.com/docs/guides/)
- [https://www.ridicorp.com/story/how-to-use-redux-in-ridi/](https://www.ridicorp.com/story/how-to-use-redux-in-ridi/)
- [https://ko.wikipedia.org/wiki/CAP_%EC%A0%95%EB%A6%AC](https://ko.wikipedia.org/wiki/CAP_%EC%A0%95%EB%A6%AC)
