## Component Design Practice

### Preparation

We recommend to follow the complete code here [user-dashboard](https://github.com/dvajs/dva/tree/master/examples/user-dashboard/src)

We can also use [dva-cli](https://github.com/dvajs/dva-cli) to generate a template, you can enter this in your terminal.

```bash
$ mkdir myApp && cd myApp
$ dva init
```

Now we have our template, we can then add our implementation step by step, this will also show you how to design our component.

### Configure router
We need to set the path to Users Router Container firstly, and create `Users.jsx` under `/routes/`

```jsx
// .src/router.js
import React, { PropTypes } from 'react';
import { Router, Route } from 'dva/router';
import Users from './routes/Users';

export default function({ history }) {
  return (
    <Router history={history}>
      <Route path="/users" component={Users} />
    </Router>
  );
};
```

```jsx
// .src/routes/Users.jsx
import React, { PropTypes } from 'react';

function Users() {
  return (
    <div>User Router Component</div>
  );
}

Users.propTypes = {
};

export default Users;
```

You can add other routers, for more info, please have a look on [react-router](https://github.com/reactjs/react-router).

### Design of Users Container Component
The basic work are all done, next we need to start to design Users Container Component, In this project, Users Container is a Route Components (this is also recommended by dva), so we add `Users.jsx` under `/routes/`

We adopt the `from top to bottom` design method, modify `./src/routes/Users.jsx` as this:

```jsx
// ./src/routes/Users.jsx
import React, { Component, PropTypes } from 'react';

// Presentational Component of Users
// Not implemented yet
import UserList from '../components/Users/UserList';
import UserSearch from '../components/Users/UserSearch';
import UserModal from '../components/Users/UserModal';

// load the styles
// we can create an empty one firstly
import styles from './Users.less';

function Users() {

  const userSearchProps = {};
  const userListProps = {};
  const userModalProps = {};

  return (
    <div className={styles.normal}>
  {/* user search */}
      <UserSearch {...userSearchProps} />
    {/* user info display */}
      <UserList {...userListProps} />
    {/* add user & modify user modal */}
      <UserModal {...userModalProps} />
    </div>
  );
}

export default Users;
```
We haven't implemented `UserSearch`，`UserList`，`UserModal` yet, but we can create them temporarily, so we can show the basic structure, `Users Router Container` is consist of those 3 `Presentational Components`

```jsx
// ./src/components/Users/UserSearch.jsx
import React, { PropTypes } from 'react';
export default ()=><div>user search</div>;
```
```jsx
// ./src/components/Users/UserList.jsx
import React, { PropTypes } from 'react';
export default ()=><div>user list</div>;
```
```jsx
// ./src/components/Users/UserModal.jsx
import React, { PropTypes } from 'react';
export default ()=><div>user modal</div>;
```
If your local environment is ok, you can access [http://127.0.0.1:8989/#/users](http://127.0.0.1:8989/#/users) from your browser:


![image](https://zos.alipayobjects.com/rmsportal/QuGskhtqUjOnxZN.png)

Note that we have 3 styles to define a component

```
// 1. traditional style
const App = React.createClass({});

// 2. es6 style
class App extends React.Component({});

// 3. stateless style（recommended by us）
const App = (props) => ({});
```

The first style is not recommended, the second style is adopted when your component uses the lifecycle methods of react, the third style is recommended style, for more detail, please visit:[Stateless Functions](https://facebook.github.io/react/docs/reusable-components.html#stateless-functions)。

We will improve the components of Users Container next, here we will start from `UserList`

### Userlist component
We ignore firstly the `<UserSearch />`and`<UserModal />`，and implement `<UserList />`，this is a user info display, we only need to import our user data to this component. So we modify `./src/components/Users/UserList.jsx`：

```jsx
// ./src/components/Users/UserList.jsx
import React, { Component, PropTypes } from 'react';

// import ant design
import { Table, message, Popconfirm } from 'antd';

// stateless style
const UserList = ({
    total,
    current,
    loading,
    dataSource,
}) => {
  const columns = [{
    title: 'name',
    dataIndex: 'name',
    key: 'name',
    render: (text) => <a href="#">{text}</a>,
  }, {
    title: 'age',
    dataIndex: 'age',
    key: 'age',
  }, {
    title: 'address',
    dataIndex: 'address',
    key: 'address',
  }, {
    title: 'operation',
    key: 'operation',
    render: (text, record) => (
      <p>
        <a onClick={()=>{}}>edit</a>
        &nbsp;
        <Popconfirm title="Are you sure to delete？" onConfirm={()=>{}}>
          <a>Delete</a>
        </Popconfirm>
      </p>
    ),
  }];

	// design pagination object
  const pagination = {
    total,
    current,
    pageSize: 10,
    onChange: ()=>{},
  };

  return (
    <div>
      <Table
        columns={columns}
        dataSource={dataSource}
        loading={loading}
        rowKey={record => record.id}
        pagination={pagination}
      />
    </div>
  );
}

export default UserList;
```

For the sake of convenience, we recommend a good UI framework [antd](http://ant.design). `antd` offres a table component, it allows us to show the data conveniently, please refer the documentation of Ant Design.
Note that, as we are using antd, we need to add `./src/index.jsx` to our code.

```jsx
import 'antd/dist/antd.css';
```

This is the result of using ant design:

![image](https://zos.alipayobjects.com/rmsportal/YFYDtvgAClhMQRu.png)

We can find that, when we design `UserList` we need the pagination info `total, current` and `loading` to be transfered into our component, so now our `UserList` will be like:

```jsx
<UserList
	current={current}
	total={total}
	dataSource={list}
	loading={loading}
/>
```

Back to `Users Router Container` , we mock some static data, pass in the UserList to show the user list info

### add static data to UserList
```jsx
// ./src/routes/Users.jsx
import React, { Component, PropTypes } from 'react';

// Presentational Component of Users
// Not implemented yet
import UserList from '../components/Users/UserList';
import UserSearch from '../components/Users/UserSearch';
import UserModal from '../components/Users/UserModal';

// load the styles
// we can create an empty one firstly
import styles from './Users.less';

function Users() {

  const userSearchProps={};
  const userListProps={
    total: 3,
    current: 1,
    loading: false,
    dataSource: [
      {
        name: '张三',
        age: 23,
        address: '成都',
      },
      {
        name: '李四',
        age: 24,
        address: '杭州',
      },
      {
        name: '王五',
        age: 25,
        address: '上海',
      },
    ],
  };
  const userModalProps={};

    return (
      <div className={styles.normal}>
    {/* user search */}
        <UserSearch {...userSearchProps} />
      {/* user info display */}
        <UserList {...userListProps} />
      {/* add user & modify user modal */}
        <UserModal {...userModalProps} />
      </div>
    );
}

Users.propTypes = {
  users: PropTypes.object,
};

export default Users;
```

After we passed in the static data, the component looks like this:

![image|400](https://zos.alipayobjects.com/rmsportal/HIDhLSNEgyNnVQD.png)

### Summary
although our implementation is quite simply, it has already contains the direction of component design, we can see  `UserList` is a pure `Presentation Component`, the data we need and the state is passed via `Users Router Component`, we are using static data now, next we will show how to create a __reducer__ to abstract our data model.

下一步，进入[Add Reducers](./06-添加Reducers.md)。
