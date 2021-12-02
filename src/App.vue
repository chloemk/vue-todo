<template>
	<main class="main-wrapper">
		<h1 class="page-title">TODO-LIST</h1>
		<p class="subtitle">Let's get things done!</p>
		<task-input v-on:addTodos="addTodo"></task-input>
		<nav>
			<ul class="tab-wrapper">
				<li class="tab-item is-active">
					<button class="tab-button">All</button>
				</li>
				<li class="tab-item">
					<button @click="clearTodo" class="tab-button">Clear</button>
				</li>
			</ul>
		</nav>
		<task-list
			v-bind:newtodos="todoItems"
			v-on:removeTodo="removeItem"
		></task-list>
	</main>
</template>

<script>
import TaskInput from './components/TaskInput.vue';
import TaskList from './components/TaskList.vue';

export default {
	data: function () {
		return {
			todoItems: [],
		};
	},
	components: {
		'task-input': TaskInput,
		'task-list': TaskList,
	},
	methods: {
		//created는 lifecycle 중 instance가 생성되자마자 호출되는 lifecycle hook이다.
		created: function () {
			if (localStorage.length > 0) {
				for (let i = 0; i < localStorage.length; i++) {
					if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
						this.todoItems.push(localStorage.key(i));
					}
				}
			}
		},
		addTodo: function (inputItem) {
			console.log('인풋 값', inputItem);
			localStorage.setItem(inputItem, inputItem);
			this.todoItems.push(inputItem);
		},
		removeItem: function (todo, idx) {
			localStorage.removeItem(todo);
			this.todoItems.splice(idx, 1);
		},
		clearTodo: function () {
			localStorage.clear();
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
</style>
