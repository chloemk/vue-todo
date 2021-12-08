# 기능 구현

[x] 새로운 투두 입력 시 리스트에 추가

- 투두 데이터를 넣는 데이터 배열을 v-for 디텍티브로 반복문으로 돌려준다.

```html
<li
	v-for="(todo, idx) in todoItems"
	v-bind:key="todo"
	class="task-list-item"
></li>
```

---

[x] 새로운 투두 입력 시 엔터로 추가 기능

- Input 태그에 v-model과 함께 `@keyup.enter="addTodo"`를 추가해준다.

---

[x] 새로운 투두 입력 시 로컬스토리지에 저장

---

[x] 새로운 투두 입력 시 아무것도 입력되지 않았다면 추가하지 않음

- 버튼에 `v-bind:disabled="newInput.length === 0"` 추가

---

[x] 투두 삭제할 시 리스트에서 삭제
[x] 투두 삭제할 시 로컬스토리지에서 삭제
[x] 클리어 버튼 클릭 시 전체 투두 삭제

```html
<button @click="clearTodo" class="tab-button">Clear</button>
```

```js
methods: {
  clearTodo: function () {
    localStorage.clear();
  },
},
```
