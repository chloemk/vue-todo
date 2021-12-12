<template>
	<main class="main-wrapper">
		<h1 class="page-title">TODO-LIST</h1>
		<p class="subtitle">Let's get things done!</p>
		<TaskInput
			:newItem="newInput"
			@update-input="updateTodo"
			@add-todo="addTodo"
		></TaskInput>
		<nav>
			<ul class="tab-wrapper">
				<li class="tab-item is-active">
					<button class="tab-button">All</button>
				</li>
				<li class="tab-item">
					<button @click="sortTodo" class="tab-button">Sort</button>
				</li>
				<li class="tab-item">
					<button @click="clearTodo" class="tab-button">Clear</button>
				</li>
			</ul>
		</nav>
		<ul class="task-list">
			<TaskList
				v-for="(todo, idx) in todoItems"
				:key="idx"
				:index="idx"
				:todoProps="todo"
				@remove-todo="removeItem"
				@complete-toggle="checkboxToggle"
				@edit-Todo="editItem"
			></TaskList>
		</ul>
	</main>
</template>

<script>
import TaskInput from './components/TaskInput.vue';
import TaskList from './components/TaskList.vue';

// 키 만들기
const STORAGE_KEY = 'vue-todo-key';

// API
const storage = {
	save(val) {
		// 배열을 받아서 문자열로 바꾸고 로컬스토리지에 저장
		const parsed = JSON.stringify(val);
		localStorage.setItem(STORAGE_KEY, parsed);
	},
	fetch() {
		// 로컬스토리지에서 값을 가져왔을 때 null일 경우를 대비해 [] 초기화를 해준다.
		const todos = localStorage.getItem(STORAGE_KEY) || '[]';
		const parsedResult = JSON.parse(todos);
		return parsedResult;
	},
};

export default {
	data: function () {
		return {
			todoItems: [],
			newInput: '',
		};
	},
	components: {
		TaskInput,
		TaskList,
	},
	methods: {
		getTodos: function () {
			this.todoItems = storage.fetch();
		},
		// created: 인스턴스가 생성되자마자 실행된다.
		created: function () {
			console.log('생성됨!!!!');
			this.getTodos();
		},
		updateTodo: function (inputVal) {
			this.newInput = inputVal;
		},
		addTodo: function () {
			const value = this.newInput;
			this.todoItems.push({ checked: false, item: value });
			storage.save(this.todoItems);
			this.clearInput();
		},
		removeItem: function (idx) {
			this.todoItems.splice(idx, 1);
			// 투두를 삭제한 배열을 전부 로컬스토리지에 덮어씌우는 방식으로 저장
			storage.save(this.todoItems);
		},
		checkboxToggle: function (checked, idx) {
			// 업데이트된 checked도 투두 배열에 업데이트 해준다.
			this.todoItems[idx].checked = checked;
			storage.save(this.todoItems);
		},
		editItem: function () {},
		clearTodo: function () {
			if (this.todoItems.length !== 0) {
				localStorage.clear();
				this.todoItems = [];
			} else {
				return alert('할 일을 추가한 후 삭제해주세요.');
			}
		},
		clearInput: function () {
			this.newInput = '';
		},
		sortTodo: function () {
			if (this.todoItems.length !== 0) {
				this.todoItems.sort((a, b) => {
					return a[this.todoItems.item] > b[this.todoItems.item] ? 1 : -1;
				});
			} else {
				return alert('할 일을 추가해주세요.');
			}
		},
	},
};
</script>

<style>
html {
	background-color: #fbfbfb;
}

#app {
	font-family: 'Source Code Pro', Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	font-size: 16px;
}

.main-wrapper {
	max-width: 600px;
	margin: 0 auto;
}

.page-title {
	font-size: 44px;
	color: #2d2d2d;
	font-weight: 600;
	margin-bottom: 10px;
	margin-top: 150px;
	text-align: center;
}

.subtitle {
	font-size: 1rem;
	font-weight: bold;
	color: #6b6b6b;
	margin-top: 0;
	text-align: center;
	margin-bottom: 25px;
}

.tab-wrapper {
	display: flex;
	list-style: none;
	justify-content: center;
	padding: 0;
	margin: 40px 0;
}

.tab-item {
	margin: 0 15px;
}

.tab-button {
	border: 0;
	background-color: #fff;
	color: #6b6b6b;
	font-weight: bold;
	letter-spacing: 0.8px;
}

.tab-button:hover {
	cursor: pointer;
}

.tab-item.is-active {
	border-bottom: 3px solid #74bdcb;
	padding-bottom: 5px;
}

.task-list {
	padding: 0;
}
</style>
