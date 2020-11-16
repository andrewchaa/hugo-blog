---
title: "Calling an API with redux saga"
date: 2020-11-15T19:45:09Z
draft: false
---
# Calling an API with redux saga

redux-saga is a library that aims to make application side effects \(i.e. asynchronous things like data fetching and impure things like accessing the browser cache\) easier to manage, more efficient to execute, easy to test, and better at handling failures. redux-saga uses ES6 generator function.

Install the packages

```bash
$ npm install --save redux-saga
$ redux-starter-kit
```

When the user clicks on confirmation on a dialog, the api call will be fired

```javascript
{ this.state.dialog && <Dialog
    hideDialog={this.hideDialog}
    confirmText={'Verify email'}
    confirmAction={() => verifyEmailStart(installer.username)}
    title={'Confirmation'}
    body={'Are you sure you want to verify the email?'}
    /> }

const mapDispatchToProps = {
  verifyEmailStart: verifyEmailStart,
}
export default connect(mapStateToProps, mapDispatchToProps)(InstallerPage)
```

verifyEmailStart is an action in the redux reducer

```javascript
import { createSlice } from 'redux-starter-kit';

const installer = createSlice({
  slice: 'installer',
  initialState: {
    loading: false,
    installer: {}
  },
  reducers: {
    verifyEmailStart: (state) => { state.loading = true },
    verifyEmailComplete: (state) => {
      state.installer.emailVerified = true
      state.loading = false
    }
  }
})

export const { actions, reducer } = installer
export const {
  verifyEmailStart,
  verifyEmailComplete
 } = actions
export default installer
```

Saga intercept the action call and execute a function.

```javascript
import { call, put, takeLatest } from 'redux-saga/effects'
import Amplify, { API } from 'aws-amplify'

import aws_exports from '../../aws-exports'
import {
  verifyEmailStart,
  verifyEmailComplete
  } from '../reducers/installer'

Amplify.configure(aws_exports)

const apiNames = {
  installersV2: "installers/v2"
}

function* verifyEmail(action) {
  try {
    yield call(() => API.put(apiNames.installersV2,
      `/installers/${action.payload}`,
      { body: {'verifyemail': true }}
      )
    )
    yield put(verifyEmailComplete())
  } catch (error) {
    throw error
  }
}

function* installerSaga() {
  yield takeLatest(verifyEmailStart().type, verifyEmail)
}

export default installerSaga;
```

