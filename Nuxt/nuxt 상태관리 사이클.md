# Nuxt.js store 상태관리 사이클

![스크린샷 2020-07-21 오전 11.34.31](/Users/baghan-eum/Library/Application%20Support/typora-user-images/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-07-21%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2011.34.31.png)

## 요약설명

```markdown
1. state
	- 모델 생성 및 모델 값 초기화
	- vue components로 rendering
2. vue components
	- 특정 이벤트를 실행하여 actions로 dispatch
3. actions
	- dispatch된 actions은 backend의 api를 axios로 응답
		- 응답은 post, get, put, delete
  - axios로 받아온 결과값은 view업데이트를 위한 mutations로 commit
4. mutations
	- commit된 mutations는 state를 변경하여 view를 업데이트
```



## 세부설명

-   vuex는 이용한 vue.js의 상태관리 라이브러리로 모든 컴포넌트에 대한 중앙 집중식 저장소 역할을 하며, 의도적인 방법으로 상태를 변경 및 관리할 수 있다.
-   `state`, `mutations`, `action`, `getters` 4가지 형태로 관리가 되며, 관리 포인트는 **store패턴**을 사용하고 통상 **store**라고 명명한다. 또한 간접적으로 서로 영향이 있으며, 단방향 데이터 흐름으로 볼 수 있다.

### State

-   State는 data로 볼 수 있다. view와 직접적으로 연결되어 있으나, 직접적인 변경은 불가능하고 mutation을 통해서만 변경이 가능하다. mutation을 통해 state가 변경이 일어나면 반응적으로 view가 업데이트 된다.



### Mutations

-   Mutation은 state를 변경하는 유일한 방법이다. 함수로 구현되며 첫 번째 인자는 `state`를 받을 수 있으며, 두 번째 인자는 `payload`를 받을 수 있다. 여기서 payload는 여러 필드를 포함할 수 있는 객체형태도 가능하다. 이 mutation은 일반적으로는 직접 호출을 할 수 없으며(Helper를 쓰지 않는 경우), commit함수를 통해서만 호출 할 수 있다.
-   대부분 mutations에서는 API를 통해 전달받은 데이터를 가공하여 state를 설정하는 데 많이 사용된다.



### Actions

-   Action은 mutation과는 달리 비동기 작업이 가능하다. 또한 mutation에 대한 `commit`이 가능하며 action에서도 mutation을 통해 state를 변경할 수 있다. action에서는 첫 번째 인자 인자를 `context` 인자로 받을 수 있으며, 이 context는 `state`, `commit`, `dispatch`, `rootstate`와 같은 속성들을 포함한다. 두 번째 인자는 mutation과 동일하게 payload로 받을 수 있다.
-   commit을 통해 mutation을 호출했다면 Action은 `dispatch`를 통해서 호출할 수 있다. context의 속성을 보면 dispatch가 있는 것으로 보아 action에서는 서로 다른 action을 호출할 수 있다는 것을 볼 수 있다.
-   action은 Axios를 통한 API호출과 그 결과에 대해서 return하거나 mutation으로 commit 하여 state를 변경하는 용도로 사용된다.



### Getters

-   Getters는 Computed에서 사용할 수 있다. 종속성에 따라 결과가 캐시되고 일부 종속성이 변경된 경우에만 다시 재계산 된다.
-   즉, 특정 state에 대해 연산을 하고 그 결과를 view에 바인딩할 수 있으며, state의 변경 여부에 따라 getter는 재계산이 되고 view 역시 업데이트를 일으킨다. 이때 state는 원본 데이터로서 변경이 일어나지 않는다.
-   *실무에서도 state의 연산 처리가 필요한 내용에 대해 getter를 사용하지만 getters의 경우 대용량 처리 시에 퍼포먼스와 연관이 되어있으므로 조심해야 한다. 대용량 처리에 관련해서는
    [[Vue.JS\] 대용량 데이터의 처리 방법과 성능 최적화 방법 (Vue.js Performance)](https://kdydesign.github.io/2019/04/10/vuejs-performance/) 를 참고하자.*

