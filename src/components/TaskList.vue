<template>
	<ul class="task-list">
		<li
			v-for="(todo, idx) in todoItems"
			v-bind:key="todo"
			class="task-list-item"
		>
			<input type="checkbox" />
			<p v-bind:class="{ done: todo.done }" class="task-list-text">
				{{ todo }}
			</p>
			<div class="task-list-cta">
				<button @click="editItem" class="task-list-btn">Edit</button>
				<button @click="removeItem(todo, idx)" class="task-list-btn">
					Delete
				</button>
			</div>
		</li>
	</ul>
</template>

<script>
export default {
	data: function () {
		return {
			todoItems: [],
		};
	},
	methods: {
		editItem: function () {},
		removeItem: function (todo, idx) {
			localStorage.removeItem(todo);
			this.todoItems.splice(idx, 1);
		},
	},
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
};
</script>

<style>
.task-list-item {
	border: 1px solid #f6f6f6;
	border-radius: 8px;
	box-shadow: 2px 4px 5px 1px rgba(0, 0, 0, 0.23);
	list-style: none;
	display: flex;
	align-items: center;
	padding: 0 16px;
	margin-bottom: 20px;
}

.task-list-cta {
	display: flex;
	column-gap: 16px;
}

.task-list-text {
	margin-left: 12px;
	font-weight: bold;
	flex: 1;
	color: #6b6b6b;
}

.task-list {
	padding: 0;
}

.task-list-btn {
	border: none;
	background-color: #fff;
	font-family: 'Source Code Pro', Helvetica, Arial, sans-serif;
	font-weight: bold;
}
.task-list-btn:hover {
	opacity: 0.5;
	cursor: pointer;
}

.done {
	text-decoration: line-through;
}
</style>
