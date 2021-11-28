<template>
	<main class="main-wrapper">
		<h1 class="page-title">TODO-LIST</h1>
		<p class="subtitle">Let's get things done!</p>
		<input type="text" />
		<button>+ Add</button>
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
}

.subtitle {
	font-size: 1rem;
	font-weight: bold;
	color: #6b6b6b;
	margin-top: 0;
}
</style>
