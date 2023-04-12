# 🧡 TSyringe

## [Tsyringe](https://github.com/microsoft/tsyringe)

마이크로소프트에서 만든 의존성 주입(Dependency Injection) 라이브러리.\
`TSyringe`을 사용하면, 객체 간의 의존성을 관리하고, 객체 생성과 소멸을 자동으로 처리할 수 있다.

External Store를 관리하는데 활용 할 수 있으며, React 컴포넌트 입장에서는 “전역”처럼 여겨진다. “Prop Drilling” 문제를 우아하게 해결할 수 있는 방법 중 하나(React로 한정하면 Context도 쓸 수 있다).



### 의존성 설치

```bash
npm i tsyringe reflect-metadata
```

* tsyringe와  tsyringe 부적으로 사용하는 reflect-metadata를 설치.
  * reflectAPI라는,것이 존재하는데,  폴리필을 지원안하는 곳에서 지원하게 해주려고 사용.

```typescript
// src/stores/Store.ts
import { singleton } from "tsyringe";

// @singleton() 
export default class Store {
  count = 0;
}
```

싱글톤 CounterStore 객체를 사용하여, container에 resolve후 꺼내서 사용할수 있다.

> 싱글톤 패턴(Singleton Pattern)\
> 어떤 클래스를 최초 한 번만 생성하고, 이후에는 생성된 객체를 계속해서 반환하는 패턴\
> 이를 통해, 하나의 객체만을 생성하여 공유함으로써 리소스를 효율적으로 사용할 수 있다.

그리고 프로그램의 시작점에 import "reflect-metadata를 적어준다. \
(index.html -> src/main.tsx)&#x20;

데코레이터를 사용하기 위해 tsconfing.json에서 데코레이터 주석을 푸는것도 잊지 말자.

```typescript
// src/stores/Store.ts
import { singleton } from "tsyringe";

@singleton()
export default class Store {
  count = 0;
}

```

싱글톤으로 객체를 생성했다. 자동으로 컨테이너가 객체를 생성하고 제거하는 제어의 역전.

`Count Control`

```tsx
// App.tsx
import CounterControl from "./components/CountControl";
import Counter from "./components/Counter";

export default function App() {
  return (
    <div>
      <p>Hello, world!</p>
      <Counter />
      <CounterControl />
    </div>
  );
}
```

```tsx
// CountControl.tsx
import { container } from "tsyringe";
import useForceUpdate from "../hooks/useForceUpdate";
import Store from "../stores/Store";

// UI
export default function CounterControl() {
  const store = container.resolve(Store);

  const forceUpdate = useForceUpdate();
  const handleClick = () => {
    store.count += 1;
    forceUpdate();
  };
  return (
    <div>
      <p>{store.count}</p>
      <button type="button" onClick={handleClick}>
        Increase
      </button>
    </div>
  );
}
```

```tsx
// Counter.tsx
import { container } from "tsyringe";
import useForceUpdate from "../hooks/useForceUpdate";
import Store from "../stores/Store";

// UI
export default function Counter() {
  const store = container.resolve(Store);

  const forceUpdate = useForceUpdate();
  const handleClick = () => {
    forceUpdate();
  };
  return (
    <div>
      <p>{store.count}</p>
      <button type="button" onClick={handleClick}>
        Refresh
      </button>
    </div>
  );
}
```

increase버튼 클릭시, conterControl의 숫자 증가, refresh시 상태가 공유된다.\


```tsx
// stores/Store.ts
import { singleton } from "tsyringe";

@singleton()
export default class Store {
  count = 0;

  forceUpdate: () => void;

  update() {
    this.forceUpdate();
  }
}

// Counter.tsx
import { container } from "tsyringe";
import useForceUpdate from "../hooks/useForceUpdate";
import Store from "../stores/Store";

export default function Counter() {
  const store = container.resolve(Store);

  const forceUpdate = useForceUpdate();
  store.forceUpdate = forceUpdate; //forceUpdate등록

  return (
    <div>
      <p>{store.count}</p>
    </div>
  );
}

// CountControl.tsx
import { container } from "tsyringe";
import Store from "../stores/Store";

// UI
export default function CounterControl() {
  const store = container.resolve(Store);

  const handleClick = () => {
    store.count += 1;
    store.update(); // 보면 내가 forceUpdate하는게 아님
  };
  return (
    <div>
      <button type="button" onClick={handleClick}>
        Increase
      </button>
    </div>
  );
}
```

다음과 같이 업데이트가 잘 되도록 하자.

허나 이럴경우에는(카운트 컴포넌트를 두번 누를경우) 두번째가 덮어 씌여지기 때문에 문제가 발생한다.

```tsx
// App.tsx
import CounterControl from "./components/CountControl";
import Counter from "./components/Counter";

export default function App() {
  return (
    <div>
      <p>Hello, world!</p>
      <Counter />
      <Counter />
      <CounterControl />
    </div>
  );
}

// stores/Store.ts
import { singleton } from "tsyringe";

type ForceUpdate = () => void;
@singleton()
export default class Store {
  count = 0;

  forceUpdates = new Set<ForceUpdate>();

  update() {
    this.forceUpdates.forEach((forceUpdate) => {
      forceUpdate();
    });
  }
}

// Counter.tsx
import { useEffect } from "react";
import { container } from "tsyringe";
import useForceUpdate from "../hooks/useForceUpdate";
import Store from "../stores/Store";

export default function Counter() {
  const store = container.resolve(Store);

  const forceUpdate = useForceUpdate();
  // store.forceUpdates.add(forceUpdate);

  useEffect(() => {
    store.forceUpdates.add(forceUpdate);

    return () => {
      store.forceUpdates.delete(forceUpdate);
    };
  }, [store, forceUpdate]);
  return (
    <div>
      <p>{store.count}</p>
    </div>
  );
}

// CountControl.tsx
import { container } from "tsyringe";

import Store from "../stores/Store";

export default function CounterControl() {
  const store = container.resolve(Store);

  const handleClick = () => {
    store.count += 1;
    store.update();
  };
  return (
    <div>
      <button type="button" onClick={handleClick}>
        Increase
      </button>
    </div>
  );
}

// hooks/useForceUpdate.ts
import { useState, useCallback } from "react";

export default function useForceUpdate() {
  const [, setState] = useState({});
  return useCallback(() => setState({}), []);
}
```

위와같이 수정해도, 리렌더링시,  store.forceUpdates.add(forceUpdate) 가 계속 실행된다.\
물론 UseCallBack을 통해 막아주었다.

&#x20;`useEffect(()=> { store.forceUpdates.add(forceUpdate);}, [])`

&#x20;결국 useEffect로 리렌더링될땐 추가 안하게 하고,\
&#x20;useForceUpdate에서 반환되는 함수에 useCallback으로 감싸서 같은 함수가 나오게해준다.

또한 컴포넌트가 화면에 그려졌다가 다시 사라질때도 클린업함수를 통해 해당 함수에 대한 처리 역시 필요하다.

여태까지 만든 방법은 스토어 내부에 무언가를 만들고 있지 않는 형식이기 때문에\
캡슐화 하는 모습으로 접근하자.

```tsx
// Counter.tsx
import { useEffect } from "react";
import { container } from "tsyringe";
import useForceUpdate from "../hooks/useForceUpdate";
import Store from "../stores/Store";

// UI
export default function Counter() {
  const store = container.resolve(Store);

  const forceUpdate = useForceUpdate();
  // store.forceUpdates.add(forceUpdate);

  useEffect(() => {
    store.addListener(forceUpdate);

    return () => {
      store.removeListener(forceUpdate);
    };
  }, [store, forceUpdate]);
  return (
    <div>
      <p>{store.count}</p>
    </div>
  );
}
```

```tsx
// stores/CounterStore.ts
import { singleton } from "tsyringe";

type Listener = () => void;

@singleton()
export default class CounterStore {
  count = 0;

  listeners = new Set<Listener>();

  publish() {
    this.listeners.forEach((forceUpdate) => {
      forceUpdate();
    });
  }

  addListener(listener: Listener) {
    this.listeners.add(listener);
  }

  removeListener(listener: Listener) {
    this.listeners.delete(listener);
  }
}

// src/Counter.tsx
import useForceUpdate from "../hooks/useForceUpdate";

import CounterStore from "../stores/CounterStore";

export default function Counter() {
  const store = container.resolve(CounterStore);

  const forceUpdate = useForceUpdate();

  useEffect(() => {
    store.addListener(forceUpdate);

    return () => store.removeListener(forceUpdate);
  }, [store, forceUpdate]);

  return (
    <div>
      <p>Count: {store.count}</p>
    </div>
  );
}

// src/CounterControl.tsx
import { container } from "tsyringe";

import CountStore from "../stores/CounterStore";

// UI
export default function CounterControl() {
  const store = container.resolve(CountStore);

  const handleClickIncrease = () => {
    store.count += 1;
    store.publish();
  };

  const handleClickDecrease = () => {
    store.count -= 1;
    store.publish();
  };
  // 아래 store.count는 갱신안됨 여기선 forceUpdate해주는게 없으니.
  // 나중에 forceUpdate가 들어간 스토어를 커스텀훅으로빼줄거
  return (
    <div>
      <p>{store.count}</p>
      <button type="button" onClick={handleClickIncrease}>
        Increase
      </button>
      <button type="button" onClick={handleClickDecrease}>
        Decrease
      </button>
    </div>
  );
}
```

lisner(Subscriber) / Publisher

구독과 발행, 업데이트 될 시, 화면을 다시 그려준다.



