<script setup>
import { useUserStore } from './stores/users'
import { ref } from 'vue'

const user_store = useUserStore()

const user_input = ref({
	name: '',
	email: ''
})

const sort = ref(false)

const CreateUser = () => {
	if (!user_input.value.name.trim() || !user_input.value.email.trim()) {
		return alert("Please enter a name and email")
	}
	user_store.create(user_input.value)

	user_input.value = {
		name: '',
		email: ''
	}
}
</script>

<template>
	<main>
		<h1>Team Manager</h1>

		<form @submit.prevent="CreateUser">
			<input 
				type="text"
				placeholder="e.g. Naruto Uzumaki"
				v-model="user_input.name"  />
			<input 
				type="email" 
				placeholder="e.g. hokage@ninja.com"
				v-model="user_input.email" />
			<input 
				type="submit" 
				value="Create user" />
		</form>

		<label><span>Sort</span><input type="checkbox" v-model="sort" /></label>
		<div class="users" v-if="!sort">
			<div v-for="user in user_store.users" class="user">
				<div>ID: {{ user.id }}</div>
				<h3>{{ user.name }}</h3>
				<p>{{ user.email }}</p>
			</div>
		</div>

		<div class="users" v-else>
			<div v-for="user in user_store.usersByName" class="user">
				<div>ID: {{ user.id }}</div>
				<h3>{{ user.name }}</h3>
				<p>{{ user.email }}</p>
			</div>
		</div>
	</main>
</template>

<style>
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
	font-family: sans-serif;
}

body {
	background-color: #EEE;
}

main {
	padding: 1.5rem;
}

h1 {
	color: #AAA;
	font-weight: 900;
	line-height: 1;
	text-transform: uppercase;
	margin-bottom: 1.5rem;
}

form {
	display: block;
	padding: 1.5rem;
	background-color: #fff;
	border-radius: 0.5rem;
	box-shadow: 0 3px 6px rgba(0,0,0,0.1);
	margin-bottom: 2rem;
}

input:not([type="checkbox"]) {
	appearance: none;
	border: none;
	outline: none;
	background: none;
}

input:not([type="submit"]):not([type="checkbox"]) {
	display: block;
	width: 100%;
	border: 1px solid #EEE;
	padding: 1rem;
	border-radius: 0.5rem;
	margin-bottom: 1rem;
	font-size: 1rem;
	transition: 0.4s;
}

input:not([type="submit"]):focus {
	border-color: #AAA;
}

input[type="submit"] {
	display: block;
	padding: 0.5rem 1rem;
	background-color: crimson;
	border-radius: 0.5rem;
	cursor: pointer;
	margin-left: auto;

	color: #FFF;
	font-size: 1rem;
	font-weight: 900;
	text-transform: uppercase;

	transition: 0.4s;
}

input[type="submit"]:hover {
	transform: scale(1.05);
	background-color: red;
}

label {
	display: flex;
	align-items: center;
	margin-bottom: 0.5rem;
}

label input {
	margin-left: 0.5rem;
}

.user {
	display: block;
	padding: 1rem;
	background-color: #FFF;
	margin-bottom: 1rem;
	border-radius: 0.5rem;
	transition: 0.2s;
}

.user div {
	color: #AAA;
	font-size: 0.875rem;
	margin-bottom: 0.5rem;
}

.user h3 {
	font-size: 1.5rem;
	margin-bottom: 0.5rem;
	transition: 0.2s;
}

.user:hover {
	box-shadow: 0 3px 6px rgba(0,0,0,0.1);
	transform: scale(1.05);
}

.user:hover h3 {
	color: crimson;
}

.user:last-of-type {
	margin-bottom: 0;
}
</style>