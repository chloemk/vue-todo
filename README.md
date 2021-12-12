# Vue Todo-List

Using Vue 2 + Vite

---

## 기능 구현

- [x] 투두 조회하기
  - [x] 구조 변경
    > v-for를 TaskInput 컴포넌트에서 직접 돌려줬는데 이럴 때 전체 투도 데이터를 props로 내려 줘야 하기 때문에 불필요한 props 내리기라고 판단되어 상위 컴포넌트 (전체 데이터가 있는 컴포넌트)에서 TaskInput 컴포넌트를 import 한 후 v-for를 적용하여 배열의 각 요소를 투두리스트로 만들어 주었다.
  - [x] 투두 리스트 오름차순 내림차순 정렬 기능 추가

---

- [x] 투두 추가하기
  - [x] 새로운 투두 입력 시 리스트에 추가
  - [x] 새로운 투두 입력 시 아무것도 입력되지 않았다면 추가하지 않음
  - [x] 새로운 투두 입력 시 로컬스토리지에 저장
  - [x] 인풋이 빈값이라면 알림 띄우기
  - [x] 투두 추가할 때마다 새로고침 해야 하는 문제점 해결 (컴포넌트 간의 통신 문제)
    > 부모 컴포넌트 데이터를 등록한 후 하위 컴포넌트에 props를 내려주고 하위에서 이벤트를 emit 하여 올려줬어야 하지만, 반대로 코드를 작성하여 투두를 추가할 때마다 새로고침을 해야 투두가 업데이트되는 현상이 나타나 해결했다.
  - [x] 양방향 바인딩이 한국어에서 한 박자 늦게 반응하는 현상 해결 (v-on:input으로 해결)
    > 양방향 통신을 위해 v-model을 사용했지만, 한국어, 중국어, 일본어를 인풋에 입력하면 양방향 바인딩이 한 박자 늦게 반응하여 마지막 글자가 떨어져 나가는 현상을 발견하여 데이터에 input 태그로 받을 값을 선언한 뒤 v-bind를 이용하여 해당 변수를 value 값으로 연결해 e.target·value로 받아오는 방식으로 변경했다.

```js
// 1. value에 사용할 변수를 데이터에 선언한 뒤 v-on:input에 이벤트 명을 작성하여 메서드로 연결하는 방법
<input type='text' v-bind:value='newInput' v-on:input='inputHandler' />

export default() {
  data: function() {
    return {
      newInput: ''
    }
  },
  methods: {
    inputHandler: function(e) {
      this.newInput = e.target.value
    }
  }
}

// 2. value에 사용할 변수를 데이터에 선언한 후 v-on:input에 직접 데이터를 연결하는 내용을 선언해주는 방법
<input type='text' :value='newInput' @input='newInput=$event.target.value' />

 export default() {
   data: function() {
     return {
       newInput: ''
     }
   }
 }
```

---

- [x] 투두 삭제하기
  - [x] 클리어 버튼 클릭 시 전체 투두 삭제
  - [x] 투두 삭제할 시 전체 리스트에서 삭제
  - [x] 투두 삭제할 시 로컬스토리지에서 삭제
  - [x] 구조 변경
    > 상위 컴포넌트에서 삭제할 인덱스를 하위 컴포넌트에 props로 내려주는 방식으로 변경했다. TaskInput에서 각 투두들에 있는 삭제 버튼이 클릭 되면(이벤트가 발생하면) event emit을 통해 이벤트를 상위 컴포넌트에 올려준다. 상위 컴포넌트에서는 올라온 이벤트를 잡고 삭제하는 작업을 진행해주는 식으로 구조를 변경했다.

---

- [x] 투두 완료 표시 기능
  > v-bind:class를 이용하여 클래스를 바인딩할 수 있고, :style을 이용하여 스타일을 바인딩할 수도 있다.

```js
// :class 바인딩 - 인라인 스타일 조작
<p :class="todoProps.checked ? 'completed' : ''" ></p>

<style>
.completed {
  text-decoration: line-through;
}
</style>
```

```js
// :style 바인딩 - 인라인 스타일 조작
<p :style="[todoProps.checked ? {'text-decoration:line-through'} : {''}]" ></p>
```

> :class로 바인딩 하다보면 복잡해질 수 있기 때문에 computed 속성을 대신 사용할 수 있다.

```js
// computed 속성을 이용하여 인라인 스타일 조작
<p class="task-list-text" :class="toggleClass"></p>

computed: {
  toggleClass() {
    return this.todoProps.checked ? 'completed' : null;
  },
},
```

### computed 속성

#### computed 속성은 언제 사용하는가?

1. 템플릿 표현식을 간결하고 직관적으로 보이게 할 때
2. 조건에 따라 HTML 클래스를 추가하거나 변경할 때
3. Vuex 스토어의 state 값을 접근할 때
4. Vue i18n과 같은 다국어 라이브러리를 사용할 때

#### 언제 사용하지 않는가?

1. HTTP 요청과 같은 많은 리소스가 할애될 때 -> watch나 methods에 넣어 사용

#### computed 속성의 특징

- `computed` 속성은 종속 대상에 따라 캐싱되며, 의존하는 값이 변할 때만 실행된다. (반면 `methods`는 렌더링 될 때만 함수가 실행된다.)
- `가독성 향상`
- computed 속성은 인자를 받지 않는다.

---

- [ ] 투두 수정하기
- [ ] 투두 드래그앤드롭

---

### 마주한 에러

`Invalid prop: type check failed for prop "TodoProps". Expected String with value "[object Object]", got Object`
string value로 prop을 전달해줬어야했지만 object로 전달해서 일어난 오류였다. props로 내려주는 value를 string에서 object 타입의 value로 변경하여 내려줘서 해결하였다.

---

## 아쉬웠던 점

타입스크립트를 vue + vite로 생성한 해당 프로젝트에 적용해보고 싶어서 tsconfig.json, shims-vue.d.ts 등 설정해보았지만 연속되는 설정 에러 때문에 기존 투두가 가지고 있던 문제들에 더 집중하여 업데이트를 했다.

vue + vite 프로젝트에 typescript 적용했을 때 참고했었던 자료들

> [How to add typescript to Vue 3 and Vite project](https://techinplanet.com/how-to-add-typescript-to-vue-3-and-vite-project/ 'How to add typescript to Vue 3 and Vite project')

> [Vite Docs](https://vitejs.dev/guide/features.html#typescript 'Vite Docs')

> [The missing migration guide: from Vue CLI to Vite](https://moiva.io/blog/the-missing-migration-guide-from-vue-cli-to-vite/ 'The missing migration guide: from Vue CLI to Vite')

더 공부해야 할 부분

- rollup
- webpack
