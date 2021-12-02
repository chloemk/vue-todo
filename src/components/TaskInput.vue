<template>
	<div class="new-task-wrapper">
		<input
			v-model="newInput"
			@keyup.enter="addTodo"
			class="new-task-input"
			type="text"
			placeholder="Type here to create"
		/>
		<button
			@click="addTodo"
			v-bind:disabled="newInput.length === 0"
			class="new-task-button"
		>
			+ Add
		</button>
	</div>
</template>

<script>
export default {
	data: function () {
		return {
			newInput: '',
		};
	},
	methods: {
		addTodo: function () {
			this.$emit('addTodos', this.newInput);
			this.newInput = '';
		},
	},
};
</script>

<style>
.new-task-wrapper {
	display: flex;
}

.new-task-input {
	padding: 16px;
	color: #959595;
	border: none;
	flex: 1;
	font-weight: bold;
	border-top-left-radius: 7px;
	border-bottom-left-radius: 7px;
	box-shadow: 2px 4px 5px 1px rgba(0, 0, 0, 0.23);
	letter-spacing: 0.8px;
}

.new-task-input:focus {
	outline: none;
}

.new-task-button {
	padding: 18px 24px;
	background-color: #74bdcb;
	color: #fff;
	font-weight: bold;
	border-top-right-radius: 7px;
	border-bottom-right-radius: 7px;
	border: none;
}
</style>
