---
title: Redux-devTools简单的使用
date: 2019-07-04 09:06:11
categories: 
  - 技术
  - Redux
tags: [devTools]
---
#### Introducing
redux-devtools 是一个非常棒的工具，它可以让你实时的监控Redux的状态树的Store

#### Installation
```javascript
npm install --save-dev redux-devtools
npm install --save-dev redux-devtools-log-monitor
npm install --save-dev redux-devtools-dock-monitor
```
<!-- more -->
#### Usege
创建DevTools组件
在你的App项目中，通过“Monitor（监视显示）”用createDevTools创建一个DevTools组件。示例用了最常用，最简单的LogMonitor和DockMonitor

`redux/DevTools/DevTools.dev.js`
```javascript
    import React from 'react';
    import {createDevTools} from 'redux-devtools';
    import LogMonitor from 'redux-devtools-log-monitor';
    import DockMonitor from 'redux-devtools-dock-monitor';
    // 默认隐藏,键盘h控制显示隐藏，q切换位置
    const DevTools = createDevTools(<DockMonitor
      toggleVisibilityKey="h"
      changePositionKey="q"
      defaultIsVisible={false}
      defaultSize={0.2}
    >
      <LogMonitor />
    </DockMonitor>);

    export default DevTools;
```
`redux/DevTools/DevTools.prd.js`
```javascript
const DevTools = {};
DevTools.instrument = () => null;

export default DevTools;

```
`redux/DevTools/index.js`
```javascript
if (process.env.NODE_ENV !== 'production') {
  module.exports = require('./DevTools.dev');
} else {
  module.exports = require('./DevTools.prd');
}
```

#### 用DevTools.instrument()通过redux的compose来扩展store
用createDevTools()创建的DevTools组件有个特殊的静态方法instrument(),它返回一个store的增强器,在开发中你需要在compose中使用。注意：DevTools.instrument()要放在applyMiddleware后，因为你的applyMiddleware可以存在异步行为，为了确保所有的actions显示在store中，所以要放在后面

 
`redux/store.js`
```javascript
import {createStore, applyMiddleware, compose} from 'redux';
import reduxOrder from 'redux-order';
import reducers from './reduces';
import DevTools from './DevTools';

const enhancer = compose(
  applyMiddleware(reduxOrder()),
  DevTools.instrument()
);

const store = createStore(
  reducers,
  enhancer
);

export default store;
or ====================================

import {createStore,applyMiddleware,compose} from 'redux'
import rootReducer from './modules/reducers'

import thunk from './middleware/thunk'
import DevTools from '../containers/DevTools'

const enhancer = compose(
  //你要使用的中间件，放在前面
  applyMiddleware(thunk),
  //必须的！启用带有monitors（监视显示）的DevTools
  DevTools.instrument()
)

export default function createStoreWithMiddleware(initialState){
  //注意：仅仅只有redux>=3.1.0支持第三个参数
  const store = createStore(rootReducer,initialState,enhancer)
  return store
}
```

#### Render <DevTools /> in your App
```javascript
import React from 'react';
import {BrowserRouter, Route, Switch} from 'react-router-dom';
import {Provider} from 'react-redux';
import {hot} from 'react-hot-loader';
import Store from '../redux';
// 使用时要区分开发环境和生产环境
import DevTools from '../redux/DevTools';
import App from '../containers/app';
import Docs from '../containers/docs';

const Router = ({component: Component, children, ...rest}) => (
  <Route
    {...rest}
    render={props => (
      <Component {...props} ><Switch>{children}</Switch></Component>
    )}
  />
);

const Root = () => (
  <BrowserRouter>
    <Provider store={Store}>
      <div className="router-content">
        {__DEVELOPMENT__ && <DevTools />}
        <Switch>
          <Router path="/" component={App} >
            <Router exact path="/docs" component={Docs} />
          </Router>
        </Switch>
      </div>
    </Provider>
  </BrowserRouter>
);

export default hot(module)(Root);

```
 
参考文档：<a href="https://link.jianshu.com?t=https://github.com/gaearon/redux-devtools" target="_blank" rel="nofollow">redux-devTools</a>