# 💚 Usestore-ts

## Action을 메서드로 처리하기

지난번에 BaseStore와 비슷하게 Object store와 counter Store를 만들어보자

### 실습 코드

CounterStore.ts

```javascript
import { singleton } from "tsyringe";

import { Action, Store } from "usestore-ts";

@singleton()
@Store()

// Increase, decrease 같은 애들만 집중할 수가 있다.
export default class CounterStore {
  count = 0;

  // 객체를 넣을 때 주의할 점
  state = {
    x: 1,
  };

  // 자동완성, 문서화의 장점이 있다.
  /**
   *  카운트를 증가시킨다.
   */
  @Action()
  increase(step = 1) {
    this.count += step;
    // 주의할 점은 일차적으로 바뀐것만 인식이 되기 때문에 ...this.state로 받아와햐한다.
    this.state = { ...this.state, x: this.state.x + 1 };
  }

  /**
   * 카운트를 감소시킨다.
   */
  @Action()
  decrease(step = 1) {
    this.count -= step;
  }
}
```

useCounterStore.ts

```javascript
import { container } from "tsyringe";

import { useStore } from "usestore-ts";

import CounterStore from "../stores/CounterStore";

export default function useCounterStore() {
  const store = container.resolve(CounterStore);

  return useStore(store);
}
```

Counter.tsx

```javascript
import useCounterStore from "../hooks/useCounterStore";

export default function Counter() {
  const [{ count }] = useCounterStore();

  return (
    <div>
      <p>Count: {count}</p>
    </div>
  );
}
```

CounterStore.tsx

```javascript
import useCounterStore from "../hooks/useCounterStore";

export default function CounterControl() {
  const [, store] = useCounterStore();

  return (
    <div>
      <button
        type="button"
        onClick={() => {
          store.increase();
        }}
      >
        Increase
      </button>
      <button
        type="button"
        onClick={() => {
          store.increase(10);
        }}
      >
        Increase 10
      </button>
      <button
        type="button"
        onClick={() => {
          store.decrease();
        }}
      >
        Decrease
      </button>
      <button
        type="button"
        onClick={() => {
          store.decrease(10);
        }}
      >
        Decrease 10
      </button>
    </div>
  );
}
```

이렇게 간단하게 쓸 수 있지만 마법처럼 막 쓰면 안되고 내부 동작 원리를 이해하자.



