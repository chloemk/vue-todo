<template>
	<main class="main-wrapper">
		<h1 class="page-title">TODO-LIST</h1>
		<p class="subtitle">Let's get things done!</p>
		<div class="new-task-wrapper">
			<input
				class="new-task-input"
				type="text"
				placeholder="Type here to create"
			/>
			<button class="new-task-button">+ Add</button>
		</div>
	</main>
</template>

<script setup></script>

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

.new-task-button {
	padding: 18px 24px;
	background-color: #e8b4b8;
	color: #fff;
	font-weight: bold;
	border-top-right-radius: 7px;
	border-bottom-right-radius: 7px;
	border: none;
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
}
</style>
