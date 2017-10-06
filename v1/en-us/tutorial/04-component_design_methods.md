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
857987965432313
// No subscription to the data
export default MyComponent;
```

#### Comparison
Categorized the components brings 2 benefits：

1. Centralize the data manipulation；
2. Let the component to be low coupling and highly cohesive

For the instance, if every component subscript the data model, then the component is high coupled with model, also the code is too spread, it will bring problems for the maintenance.

Except for the subscription difference, the design of those two kinds of components are also different.

`Presentational Component` is pure independent component, you can check  [ant.design React UI introduce](http://ant.design/docs/react/introduce)
Every component has no coupling with the business logic, it will only accomplish its own task. Data need to be passed via `props`, also we need to expose our interfaces.

`Container Component` is more like a state manager, it acts as a container, subscript component's data and also organize component's interaction logic and display.

More info of Dan Abramov's thought:
- https://github.com/reactjs/redux/issues/756#issuecomment-141683834
- https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0#.231v4pdgr

Next we will introduce the development of component of our project.

Next [Component Design Practice](./05-组件设计实践.md)。
