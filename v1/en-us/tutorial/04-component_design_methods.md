## Component Design Methods

Let's have a look how to design a react component of dva.

### Component Design
A react application is building upon many independent component. We need to make sure that every component is focus on its own business when we separate the component.

Generally, there are two types of component design.

1. Container Component
2. Presentational Component

#### Container Component
Container Component means a component that `watches the data behavior`, that is to say its duty is to `bind related model data`. Accoring to the role of this component, it contains some other sub-component. For example in project, Layouts, router components and other regular containers component.

Usually we write it as follows：

```javascript
import React, { Component, PropTypes } from 'react';

// the connect function of dva connects the data model and component together
import { connect } from 'dva';

// Component
const MyComponent = (props)=>{};
MyComponent.propTypes = {};

// Watching property, building the map relation between component and data model
function mapStateToProps(state) {
  return {...state.data};
}

// connect model
export default connect(mapStateToProps)(MyComponent);
```

#### Presentational Component
Presentational Component shows its nature, present the components. AKA: Dumb Component. it won't subscript the data from model, but use props to pass needed data from parent to it.

Usually we write it as follows：

```javascript
import React, { Component, PropTypes } from 'react';

// Component
// the needed data of Container Component is passed via props.
const MyComponent = (props)=>{}
MyComponent.propTypes = {};

// No subscription to the data
export default MyComponent;
```

#### 对比
对组件分类，主要有两个好处：

1. 让项目的数据处理更加集中；
2. 让组件高内聚低耦合，更加聚焦；

试想如果每个组件都去订阅数据 model，那么一方面组件本身跟 model 耦合太多，另一方面代码过于零散，到处都在操作数据，会带来后期维护的烦恼。

除了写法上订阅数据的区别以外，在设计思路上两个组件也有很大不同。
`Presentational Component`是独立的纯粹的，这方面很好的例子，大家可以参考 [ant.design UI组件的React实现](http://ant.design/docs/react/introduce) ，每个组件跟业务数据并没有耦合关系，只是完成自己独立的任务，需要的数据通过 `props` 传递进来，需要操作的行为通过接口暴露出去。
而 `Container Component` 更像是状态管理器，它表现为一个容器，订阅子组件需要的数据，组织子组件的交互逻辑和展示。

更多的相关内容，可以看看Redux作者（facebook的程序员）Dan Abramov 的看法：
- https://github.com/reactjs/redux/issues/756#issuecomment-141683834
- https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0#.231v4pdgr

接下来我们会进入本例中组件的设计开发，从实践一步一步看看如何贯穿起来。

下一步，进入[组件设计实践](./05-组件设计实践.md)。
