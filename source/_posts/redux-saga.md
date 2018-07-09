---
title: redux-saga
date: 2018-04-03 22:12:46
categories: 
  - 技术
tags: redux-saga
---

### createSagaMiddleware(...sagas)`

创建一个 Redux 中间件，将 Sagas 与 Redux Store 建立
<!-- more -->
- `sagas: Array` - Generator 函数列表

  ```
  import createSagaMiddleware from 'redux-saga'
  import reducer from './path/to/reducer'
  import sagas from './path/to/sagas'

  export default function configureStore(initialState) {
    // 注意：redux@>=3.1.0 的版本才支持把 middleware 作为 createStore 方法的最后一个参数
    return createStore(
      reducer,
      initialState,
      applyMiddleware(/* other middleware, */createSagaMiddleware(...sagas))
    )
  }
  ```