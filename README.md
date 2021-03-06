bind redux action to group, avoid action generate function name conflict, and compatibility [redux `bindActionCreators`](https://github.com/reactjs/redux/blob/master/src/bindActionCreators.js)


[![Build Status](https://travis-ci.org/eyasliu/redux-bind-action-groups.svg?branch=master)](https://travis-ci.org/eyasliu/redux-bind-action-groups)


# install 

```shell
npm i -S redux-bind-action-groups
```

# example

my two action creator files

```js
// post.js
export function getList(){
    return {
        type: 'POST_GETLIST'
    }
}


// photo.js
export function getList(){
    return {
        type: 'PHOTO_GETLIST'
    }
}
```

bind action creator with redux bindActionCreators

```js
import * as postActions from './post';
import * as photoActions from './photo';
import {bindActionCreators} from 'redux';

function mapDispatchToProps(dispatch){
    return bindActionCreators({
        ...postActions,
        ...photoActions
    }, dispatch)
}

// in React Component
this.props.getList();  // which getList will exec in post and photo
```

## useage

```js
import bindActionGroups from 'redux-bind-action-groups';

function mapDispatchToProps(dispatch){
    return bindActionGroups({
        post: postActions,
        photo: photoActions,
        foo: () => ({type: 'DO_SOMETHING'})
    }, dispatch)
}

// in React Component, work fine
this.props.post.getList();
this.props.photo.getList();
this.props.foo()
```
