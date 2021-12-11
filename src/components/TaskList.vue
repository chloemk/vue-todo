<template>
	<li class="task-list-item">
		<input type="checkbox" />
		<p class="task-list-text">
			{{ todoProps }}
		</p>
		<div class="task-list-cta">
			<button @click="editItem" class="task-list-btn">Edit</button>
			<button @click="removeTodo" class="task-list-btn">Delete</button>
		</div>
	</li>
</template>

<script>
export default {
	props: {
		todoProps: String,
		index: Number,
	},
	methods: {
		editItem: function () {},
		removeTodo: function () {
			this.$emit('removeTodo', this.index);
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

.done {
	text-decoration: line-through;
}
</style>
