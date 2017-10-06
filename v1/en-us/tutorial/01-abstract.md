## Abstract

### Preface

dva is a lite encapsulation of redux, although we don't need to fully understand redux to be able to use dva, we still need some knowledge of redux. Once we understand the basic knowledge of redux, dva is easy to use, also we can understand more underlining knowledge. Redux has a mature community and documentation, you can access [http://redux.js.org] to get more content. it will introduce the frameworks in the ecosystem and design pattern, it worth a look.


### Start

In __Geting started__ section, we have already some knowledge of dva, now we will finish a complete example project, during this project, we will finish following items step by step.

1. [Code Structure Design](./02-code_structure_design.md)
1. [Design Model](./03_design_model.md)
1. [Component Design Methods](./04-component_design_methods.md)
<!-- 1. [添加样式](./05-组件设计实践.md)
1. [添加 Reducers](./06-添加Reducers.md)
1. [添加 Effects](./07-添加Effects.md)
1. [定义 Service](./08-定义Services.md)
1. [mock 数据](./09-mock数据.md)
1. [添加样式](./10-添加样式.md)
1. [设计布局](./11-设计布局.md) -->

Firstly, we will clarify the structure of project, get familiar with the concept of each part; then we will talk about how to separate the model, and the design pattern of model; then we will introduce how to properly design your component according to the project, and how to deal with styles in the component; after we designed the component, we will present the content of data, including Synchronous asynchronous methods, and how to deal with asynchronous method. In the end, we will cover how to mock data and design of the layout.


This is a screenshot of the project that we will make.

![user-dashboard](https://cloud.githubusercontent.com/assets/1179603/17655205/dfde2f4e-62dd-11e6-9c91-657ee4c17b91.png)

Source code: [user-dashboard](https://github.com/dvajs/dva/tree/master/examples/user-dashboard)
The source code is runnable, however, we recommend to building it with us step by step.

Next [Code Structure Design](./02-code_structure_design.md)。
