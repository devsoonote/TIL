### 1. 언제 `take(1)`을 사용해야할까?
- `switchMap`은 그 다음의 스트림으로 중심을 옮겨주는 역할을 하는데, `switchMap`을 사용하여 `store`에 있는 데이터를 가지고 올때는 스트림을 옮기려는 목적이 아닌 그저 데이터를 가지고 오는 목적이기 때문에 `take(1)` 을 사용하여 스트림을 한 번만 가지고 오도록 한다.
- 그럼 언제 `take(1)`을 사용하는 걸까?
- `switchMap`을 `withLatestFrom`으로 변경하여도 잘 작동하면 `take(1)`을 사용한다.
- `withLatestForm`은 스트림의 주체가 바뀌지 않으며 한번만 울린다.

### 2. `markForCheck`와 `detechChange`
- `props`가 아닌 `state`만 변경되었을 때는 `detechChange`가 작동하지 않는다. (props: 읽기전용) ⇒ markForCheck
- `detechChange`
    - 완전히 `sync` 이므로, `detechChange` 뒤에 있는 코드는 업데이트되지 않는다.
    - 나를 기준으로 내가 변경되면 아래의 자식컴포넌트도 전부 바뀐다.
- `markForCheck`
    - 자기 스스로 `detechtion`을 발생시키지 않는다.
    - `ApplicationRef`가 `tick`이 된 상태면 업데이트를 시키기 때문에, 상위 컨텍스트의 컴포넌트가 ApplicationRef를 tick하지 않는다면, 절대로 업데이트가 되지 않는다.
- 만약에 `change detect onPush`전략을 사용하였을때, 부모가 변경했는데, 자식이 변경되지 않는다면, `tree`가 중간에 끊겼다는 소리이다.
