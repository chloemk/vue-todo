<template>
	<form @submit.prevent="submitTodo">
		<div class="new-task-wrapper">
			<input
				type="text"
				class="new-task-input"
				placeholder="Type here to create"
				:value="newItem"
				@input="inputHandler"
			/>
			<button type="submit" class="new-task-button">+ Add</button>
		</div>
	</form>
</template>

<script>
export default {
	// props validation
	props: {
		newItem: {
			type: String,
			required: true,
		},
	},
	methods: {
		inputHandler: function (e) {
			// this.$emit('addTodos', this.newInput);
			// this.newInput = '';
			//이벤트 이름에는 항상 kebab-case 사용
			this.$emit('update-input', e.target.value);
		},
		submitTodo: function () {
			console.log('클릭', this.newItem);
			if (this.newItem === '') {
				// ! 인풋이 빈값이라면 모달 띄우기
				alert('입력 후 버튼을 클릭해 주세요.');
				return;
			} else {
				this.$emit('add-todo');
			}
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
