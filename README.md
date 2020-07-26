![banner](/rxdeep-local-banner.png)

```bash
npm i rxdeep-local
```
Reactive states that persist on `localStorage` and are shared between different tabs/windows, based on [RxDeep](https://loreanvictor.github.io/rxdeep/)
and [RxJS](https://rxjs.dev). Store deep nested objects, persist select parts of a state-tree, modify/listen to changes on any node in the state-tree
in a [fast](https://loreanvictor.github.io/rxdeep/docs/performance) and [precise](https://loreanvictor.github.io/rxdeep/docs/precision) manner.

<br><br>

## Example Usage

▷ Create state object:
```ts
import { local } from 'rxdeep-local';
import { state } from 'rxdeep';

const s = local(state(42), 's');
s.subscribe();

s.value = 43; // --> updates local storage, informs other tabs/windows of the change.
```
▷ Nested complex values are also possible:

```ts
const s = local(state({ x: 2, y: [{ z: 4 }, {z : 5}, {z : 6}]}, 's');
```
▷ You can also just persist part of another state tree:

```ts
const s = state({ x: 2, y: [{ z: 4 }, {z : 5}, {z : 6}]});
const l = local(s.sub('x'), 's.x');
```
▷ As per any [RxDeep](https://loreanvictor.github.io/rxdeep/) state, you can listen to and/or modify parts of a deep nested state:

```ts
const s = local(state({ x: 2, y: [{ z: 4 }, {z : 5}, {z : 6}]}, 's');

s.sub('y').sub(2).sub('z').subscribe(console.log);     // --> logs 5
s.sub('x').value = 3;                                  // --> updates the state, 
                                                       // ... rewriting on localStorage 
                                                       // ... and notifying other tabs
```

<br>

👉 Read [RxDeep documentation](https://loreanvictor.github.io/rxdeep/) for more info.

