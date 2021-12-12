<template>
	<li class="task-list-item">
		<input type="checkbox" @change="isChecked" :checked="todoProps.checked" />
		<p class="task-list-text" :class="toggleClass">
			<!-- :class="todoProps.checked ? 'completed' : ''" -->
			<!-- :style="todoProps.checked ? 'text-decoration:line-through' : ''" -->
			{{ todoProps.item }}
		</p>
		<div class="task-list-cta">
			<button @click="editTodo" class="task-list-btn">Edit</button>
			<button @click="removeTodo" class="task-list-btn">Delete</button>
		</div>
	</li>
</template>

<script>
export default {
	props: {
		todoProps: Object,
		index: Number,
	},
	// 클래스의 조건 처리
	computed: {
		toggleClass() {
			return this.todoProps.checked ? 'completed' : null;
		},
	},
	methods: {
		editTodo: function () {
			this.$emit('edit-Todo', this.index);
		},
		removeTodo: function () {
			this.$emit('remove-todo', this.index);
		},
		isChecked: function (e) {
			this.$emit('complete-toggle', e.target.checked, this.index);
		},
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

.completed {
	text-decoration: line-through;
	text-decoration-thickness: 2px;
	opacity: 0.7;
	text-decoration-color: #6b6b6b;
}
</style>
