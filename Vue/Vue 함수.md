# Vue

-----------------------------------------------------------------------------------------------------------------------------

### 1. $emit

자식 컴포넌트

```vue
<a @click="함수"></a>
<script>
export default {
  methods: {
    함수명() {
      this.$emit('보낼함수', 보내는 값(없어도됨));
    },
  },
};
</script>
```

부모 컴포넌트

```vue
<child-component @받는함수="실행할 함수"></child-component>
<script>
export default {
  methods: {
    실행할 함수명(받는값(없어도됨)) {
  		...
		},
  },
};
</script>
```

받는함수이름과 보낼함수이름이 같아야하며, 실행할 함수는 부모컴포넌트에서 정의해줘야 에러가 없다.

-----------------------------------------------------------------------------------------------------------------------------

## 2. watch

```vue
<input type="text" v-model="item">
{{ item }}
<script>
export default {
  data: () => ({
    item: '',
  }),
  watch: {
    item: { // item은 감시할 data 파라미터
      console.log('변경될때마다 이 코드를 실행');
    },
  },
};
</script>
```

중첩된 즉, 객체를 감지하려면,

```vue
<input type="text" v-model="item.foo">
{{ item }}
<script>
export default {
  data: () => ({
    item: {
      foo: '',
    },
  }),
  watch: {
    item: { // item은 감시할 data 파라미터
      deep: true, // 객체 감시의 허용여부 프로퍼티
      // 무조건 handler를 정의하고 써줘야함.
      // handler는 이름을 handler라고밖에 정의할 수 없다.
      // handler의 파라미터는 변경된 객체와 변경전 객체를 파라미터로 쓸 수 있다.
      handler(val, oldVal) {
        console.log('item객체의 내부 변수값이 변경될때마다 이 코드를 실행');
      },
    },
  },
};
</script>
```

-----------------------------------------------------------------------------------------------------------------------------

## 3. $refs

$refs는 vue 파일의 요소에 ref 속성을 부여하여 돔에 접근할 수 있다.

```vue
<input ref="item" type="type" v-on:input="items">

<script>
export default {
  methods: {
    items() {
      // this.$refs.'이름'.'가져올 속성값의 속성명';
      const values = this.$refs.item.value;
      console.log(values);
    },
  },
};
</script>
```

