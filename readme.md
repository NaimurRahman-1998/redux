# initialize rtk
1. npm init --y
2. npm i @reduxjs/toolkit

## three redux basic
1. create actions
2. create reducers
3. create store and dispacth the store

```
const redux = require('redux')
const produce = require('immer').produce
const reduxLogger = require('redux-logger')
const logger = reduxLogger.createLogger()
const applyMiddleware = redux.applyMiddleware

// action
const STREET_UPDATED = 'STREET_UPDATED'
function updateStreet(street) {
    return {
        type: STREET_UPDATED,
        payload: street
    }
}

const initialState = {
    name: 'Jon',
    address: {
        city: 'Dhaka',
        country: 'BD',
        street: 'Dhanmondi'
    }
}

const reducer = (state = initialState, action) => {
    switch (action.type) {
        case STREET_UPDATED:
            // return {
            //     ...state,
            //     address: {
            //         ...state.address,
            //         street: action.payload
            //     }
            // }
            return produce(state, (draft) => {
                draft.address.street = action.payload
            })
        default:
            return state
    }
}

const store = redux.createStore(reducer , applyMiddleware(logger));
console.log('initial State', store.getState())

const unsubscribe = store.subscribe(() => {})

store.dispatch(updateStreet('Mohammadpur'))

unsubscribe()
```
