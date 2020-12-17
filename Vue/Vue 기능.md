# Vue 기능

----------------------------------------------------------------------------------------------------------------

## 1. Debouce

- lodash가 있으면 편하다.
- 입력 시 값은 입력될때마다 변경되기 때문에 데이터변경이 빈번한 페이지라면 사용하기에 좋은 기능.
- 기본적으로 동작되지만 특정한 상황에서 동작되지 않는다.

```vue
PW: <input type="text" v-model="password" v-on:input="passwordCheck">
PW 확인: <input type="text" v-model="passwordConfirm" v-on:input="passwordCheck">
{{ message }}
<script>
// lodash를 필수로 설치해야만 가능함.
// npm: npm install --save lodash, yarn: yarn add lodash
import _ from 'lodash';
  
export default {
  data: () => ({
    password: '',
    passwordConfirm: '',
    message: '',
  }),
  created() {
    this.passwordCheck = _.debounce(() => {
      if (this.password.search(this.passwordConfirm) > -1) this.message = '';
      else this.message = '비밀번호가 일치 ㄴㄴ';
    });
  },
  methods: {
    passwordCheck: () => {},
  },
};
</script>
```

----------------------------------------------------------------------------------------------------------------

## 2. allCheck

- 체크박스의 전체 체크를 위한 기능.
- 체크된 변수값들을 이후 사용하는 것이 가능

```vue
<input type="checkbox" v-model="allCheck">
<div v-for="(item, i) in items" :key="i">
  <input type="checkbox" :id="item.value" :value="item.value" v-model="checked">
  <label :for="item.value">{{ item.text }}</label>
</div>

<script>
export default {
  data: () => ({
    items: [
      { text: '에이', value: 'a' },
      { text: '비', value: 'b' },
      { text: '씨', value: 'c' },
    ],
    checked: [],
  }),
  computed: {
    allCheck: {
      get() {
        return this.items ? this.items.length === this.checked.length : false;
      },
      set(value) {
        const checked = [];
        if (value) {
          this.items.forEach((item) => {
            checked.push(item.value);
          });
        }
        this.checked = checked;
      },
    },
  },
};
</script>
```

----------------------------------------------------------------------------------------------------------------

## 3.  Pagination

- 다량의 배열객체 데이터를 테이블화 시켜 페이지네이션을 수행하는 기능

```vue
<table>
  <tbody>
  	<tr v-for="(item, i) in itemList" :key="i">
      <td>{{ (pageNum * pageSize) + i + 1 }}</td>
    	<td>{{ item.text }}</td>
      <td>{{ item.value }}</td>
    </tr>
  </tbody>
</table>
<div>
  <button :disabled="pageNum === 0" v-on:click="prevPage">이전</button>
  <button
          v-for="page in pageCount"
          :key="page"
          :id="`page_${page}`"
          :disabled="pageNum + 1 === page"
          v-on:click="pagination"
	>
    {{ page }}
  </button>
  <button :disabled="pageNum >= pageCount - 1" v-on:click="nextPage">다음</button>
</div>

<script>
export default {
  data: () => ({
    items: [
      { text: '1', value: '1' },
      					...
      { text: '20', value: '20' },
    ],
    pageNum: 0,
    pageSize: 10,
  }),
  computed: {
    pageCount() {
      const page = Math.floor(this.items.length / this.pageSize) + 1;
      return page;
    },
    itemList() {
      const start = this.pageNum * this.pageSize;
      const end = start + this.pageSize;
      return this.items.slice(start, end);
    },
  },
  methods: {
    nextPage() {
      this.pageNum += 1;
    },
    prevPage() {
      this.pageNum -= 1;
    },
    pagination(e) {
      const id = e.target.id;
      const page = parseInt(id.split('_')[1], 10);
      this.pageNum = page - 1;
    },
  },
};
</script>
```

----------------------------------------------------------------------------------------------------------------

## 4.  Sorting of Array

- 오름차순 정렬은 sort()
- 내림차순 정렬의 경우 sort().reverse() 를 사용
- 문자열과 숫자를 섞어써도 정렬이 된다.
- 가장 널리 사용되는 방법이며 퍼포먼스도 좋다.

```javascript
var a = ['b', 'a', 'c', 'z'];
console.log(a.sort()); // 오름차순 정렬 Ascending
// result => ["a", "b", "c", "z"]
console.log(a.sort().reverse()) // 내림차순 정렬 Descending
// result => ["z", "c", "b", "a"]

var a = [2, 1, 4, 3];
console.log(a.sort()); // 오름차순 정렬 Ascending
// result => [1, 2, 3, 4]
console.log(a.sort().reverse()) // 내림차순 정렬 Descending
// result => [4, 3, 2, 1]

var a = ['1', '2', 3, 4, 'apple', 'b', 'd'];
console.log(a.sort()); // 오름차순 정렬 Ascending
// result => ["1", "2", 3, 4, "apple", "b", "d"]
console.log(a.sort().reverse()) // 내림차순 정렬 Descending
// result => ["d", "b", "apple", 4, 3, "2", "1"]
```

- 이번엔 다른방식으로 정렬을 사용한다.
- sort에 사용되지 않았던 파라미터값을 넣어 사용한다.

```javascript
var a = ['b', 'a', 'c', 'z'];
console.log(a.sort((b, a) => -(a>b)||+(a<b))); // 오름차순 정렬 Ascending
// result => ["a", "b", "c", "z"]
console.log(a.sort((a, b) => -(a>b)||+(a<b))) // 내림차순 정렬 Descending
// result => ["z", "c", "b", "a"]

var a = [2, 1, 4, 3];
console.log(a.sort((b, a) => -(a>b)||+(a<b))); // 오름차순 정렬 Ascending
// result => [1, 2, 3, 4]
console.log(a.sort((a, b) => -(a>b)||+(a<b))) // 내림차순 정렬 Descending
// result => [4, 3, 2, 1]

var a = ['1', '2', 3, 4, 'apple', 'b', 'd'];
console.log(a.sort((b, a) => -(a>b)||+(a<b))); // 오름차순 정렬 Ascending
// result => ["1", "2", 3, 4, "apple", "b", "d"]
console.log(a.sort((a, b) => -(a>b)||+(a<b))) // 내림차순 정렬 Descending
// result => ["d", "b", "apple", 4, 3, "2", "1"]
```

- 만약 배열[객체]로 되어 있는 변수의 경우 객체 내의 값으로 객체를 정렬하고자 할 때, 앞서 보였던 방식으로는 해결되지 않는다.
- 파라미터를 이용한 정렬방식을 응용하여 정렬한다.

```javascript
var a = [{ a: 'd', b: 'e', c: 'f' }, { a: 'a', b: 'b', c: 'c' }, { a: 'g', b: 'h', c: 'i' }];
// 객체 내의 키값 a로 정렬하는 경우
a.sort((a, b) => (a.a > b.a) ? 1 : ((b.a > a.a) ? -1 : 0));
// result 는 오름차순 정렬이 된다.
a.sort((b, a) => (a.a > b.a) ? 1 : ((b.a > a.a) ? -1 : 0));
// result 는 내림차순 정렬이 된다.

// 그러나 lint를 사용하는 경우 이 방식은 권장하지 않을 뿐더러 동작도 막는다.
// 중첩 삼항 연산자를 권장하지 않기 때문이다.
Array.prototype.sort.call((a, b) => {
  if (a.a > b.a) return 1;
  if (b.a > a.a) return -1;
  if (a.a === b.a) return 0;
});
// 파라미터를 뒤바꾸면 내림차순으로 정렬이 된다.
```

----------------------------------------------------------------------------------------------------------------

## 5. Objects of Array Division

- 각각의 배열 또는 객체는 어떻게든 분류하여 새로운 변수로 재정의 할 수 있다.

- 그러나 N개의 배열이나 객체 또는 배열[객체], 다차원 배열은 길이가 정해져 있지 않기 때문에 분할하여 재정의하기가 다소 어렵다.

- 지금 제시하는 방법은 reduce, concat을 사용하여 재정의하는 방법으로,

  N개의 객체를 재정의하여 출력하는 방식이다.

- 쉽게말해,

  `var a = [['a','b','c','d'], ... , ['w','x','y','z']];`

  가 있다. 2차원 배열안에 몇개인지 모를 1차원 배열을

  `[['a', ... , 'w'], ... , ['d', ... , 'z']];`

  로 만들기 위해서 제시되는 방법이다.

```javascript
var a = [['a','b','c','d'], ... , ['w','x','y','z']];
var result = a.reduce(
  (values, currentValues) => values.reduce(
    (value, currentValue) => value.concat(
      currentValues.map(
        (index) => [].concat(currentValue, index)
      )
    ), []
  )
);
```

- 상당히 식이 복잡하다. 예로 `var a = [['a','b','c','d'], ['e','f','g','h']];` 의 1차원 배열이 만들어졌다는 가정 하에 결과값을 출력하자면,

```javascript
var a = [['a','b','c','d'], ['e','f','g','h']];
var result = a.reduce((values, currentValues) => values.reduce((value, currentValue) => value.concat(currentValues.map((index) => [].concat(currentValue, index))), []));
// 0: (2) ["a", "e"]
// 1: (2) ["a", "f"]
// 2: (2) ["a", "g"]
// 3: (2) ["a", "h"]
// 4: (2) ["b", "e"]
// 5: (2) ["b", "f"]
// 6: (2) ["b", "g"]
// 7: (2) ["b", "h"]
// 8: (2) ["c", "e"]
// 9: (2) ["c", "f"]
// 10: (2) ["c", "g"]
// 11: (2) ["c", "h"]
// 12: (2) ["d", "e"]
// 13: (2) ["d", "f"]
// 14: (2) ["d", "g"]
// 15: (2) ["d", "h"]
```

- 의 결과값이 출력된다. 4일간 삽질하고 머리싸맨 후 발견한 방법이며, 알고리즘을 적용하면 더 간단한 식이 나올지도 모른다.
- 그러나 머리아프므로 패스.

----------------------------------------------------------------------------------------------------------------

