# Vue Todo-List

Using Vue 2 + Vite

---

## 기능 구현

- [x] 투두 조회하기
  - [x] 구조 변경
    > v-for를 TaskInput 컴포넌트에서 직접 돌려줬는데 이럴 때 전체 투도 데이터를 props로 내려 줘야 하기 때문에 불필요한 props 내리기라고 판단되어 상위 컴포넌트 (전체 데이터가 있는 컴포넌트)에서 TaskInput 컴포넌트를 import 한 후 v-for를 적용하여 배열의 각 요소를 투두리스트로 만들어 주었다.

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

- [x] 투두 수정하기

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
