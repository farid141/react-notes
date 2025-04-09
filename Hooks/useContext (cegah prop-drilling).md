untuk mencegah prop-drilling dari parent ke grand-child
- bisa digunakan untuk mem-passing state dari useReducer atau useState

Berikut contoh penulisan **React Context** yang baik menggunakan **Reducer** dan **TypeScript**. Ini adalah pattern yang scalable dan maintainable untuk state global, cocok buat aplikasi menengah hingga besar.

---

## 📦 Struktur Direktori (Opsional, tapi Rapi)
```
src/
  context/
    CounterContext.tsx
  components/
    CounterDisplay.tsx
    CounterButtons.tsx
  App.tsx
```

---

## 1. `CounterContext.tsx`

```tsx
import React, { createContext, useContext, useReducer, ReactNode } from 'react';

// 1. Define state type
type CounterState = {
  count: number;
};

// 2. Define action types
type CounterAction = 
  | { type: 'INCREMENT' }
  | { type: 'DECREMENT' }
  | { type: 'RESET' };

// 3. Initial state
const initialState: CounterState = {
  count: 0,
};

// 4. Reducer function
function counterReducer(state: CounterState, action: CounterAction): CounterState {
  switch (action.type) {
    case 'INCREMENT':
      return { count: state.count + 1 };
    case 'DECREMENT':
      return { count: state.count - 1 };
    case 'RESET':
      return { count: 0 };
    default:
      return state;
  }
}

// 5. Context types
type CounterContextType = {
  state: CounterState;
  dispatch: React.Dispatch<CounterAction>;
};

// 6. Create Context
const CounterContext = createContext<CounterContextType | undefined>(undefined);

// 7. Provider component
export const CounterProvider = ({ children }: { children: ReactNode }) => {
  const [state, dispatch] = useReducer(counterReducer, initialState);

  return (
    <CounterContext.Provider value={{ state, dispatch }}>
      {children}
    </CounterContext.Provider>
  );
};

// 8. Custom hook for consuming context
export const useCounter = () => {
  const context = useContext(CounterContext);
  if (!context) {
    throw new Error('useCounter must be used within a CounterProvider');
  }
  return context;
};
```

---

## 2. `CounterDisplay.tsx`

```tsx
import React from 'react';
import { useCounter } from '../context/CounterContext';

const CounterDisplay = () => {
  const { state } = useCounter();

  return <h2>Current Count: {state.count}</h2>;
};

export default CounterDisplay;
```

---

## 3. `CounterButtons.tsx`

```tsx
import React from 'react';
import { useCounter } from '../context/CounterContext';

const CounterButtons = () => {
  const { dispatch } = useCounter();

  return (
    <div>
      <button onClick={() => dispatch({ type: 'INCREMENT' })}>+</button>
      <button onClick={() => dispatch({ type: 'DECREMENT' })}>-</button>
      <button onClick={() => dispatch({ type: 'RESET' })}>Reset</button>
    </div>
  );
};

export default CounterButtons;
```

---

## 4. `App.tsx`

```tsx
import React from 'react';
import { CounterProvider } from './context/CounterContext';
import CounterDisplay from './components/CounterDisplay';
import CounterButtons from './components/CounterButtons';

function App() {
  return (
    <CounterProvider>
      <div style={{ textAlign: 'center', marginTop: '50px' }}>
        <h1>React Context + Reducer + TypeScript</h1>
        <CounterDisplay />
        <CounterButtons />
      </div>
    </CounterProvider>
  );
}

export default App;
```

---