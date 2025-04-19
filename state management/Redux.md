# Pendahuluan

- merupakan advance tools untuk sharing props di beberapa komponen
- membutuhkan reducer function, seperti useReducer
- tidak spesifik ke library react
- tetapi react memiliki react-redux yang memudahkan penggunaan redux ke react

1. npm install redux react-redux

    ```javascript
    // store/index.js
    import { createStore } from 'redux';

    const counterReducer = (state = { counter: 0 }, action) => {
      if (action.type === 'increment') {
        return {
          counter: state.counter + 1,
        };
      }

      if (action.type === 'decrement') {
        return {
          counter: state.counter - 1,
        };
      }

      return state;
    };

    const store = createStore(counterReducer);
    export default store;
    ```

2. wrap komponen app dengan komponen provider

    ```javascript
    // index.js
    import React from 'react';
    import ReactDOM from 'react-dom/client';

    import './index.css';
    import App from './App';
    import store from './store/index.js'
    import { Provider } from 'react-redux';

    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(<Provider store={store}> <App /> </Provider>);
    ```

3. pada komponen yang ingin menggunakan state tersebut

    ```javascript
    import { useSelector, useDispatch } from 'react-redux';

    import classes from './Counter.module.css';

    const Counter = () => {
      const dispatch = useDispatch();
      const counter = useSelector(state=> state.counter);

      const incrementHandler = () => {
        dispatch({type: 'increment'})
      };
      const decrementHandler = () => {
        dispatch({type: 'decrement'})
      };
      const toggleCounterHandler = () => {};

      return (
        <main className={classes.counter}>
          <h1>Redux Counter</h1>
          <div className={classes.value}>{counter}</div>
          <button onClick={incrementHandler}>Increment</button>
          <button onClick={decrementHandler}>Decrement</button>
          <button onClick={toggleCounterHandler}>Toggle Counter</button>
        </main>
      );
    };

    export default Counter;
    ```
