<script>
	import { goto } from '$app/navigation';
	import { onMount } from 'svelte';
	export let data;
	let answer;
	let title = data.title;
	async function getTodo() {
		const response = await fetch(`http://127.0.0.1:8000/api/todo/${title}`);
		const data = await response.json();
		return data;
	}

	async function deleteTodo() {
		const response = await fetch(`http://127.0.0.1:8000/api/todo/${title}`, {
			method: 'DELETE',
			headers: {
				'Content-Type': 'application/json'
			}
		})
			.then((response) => {
				goto('/');
			})
			.catch((error) => {
				// Handle error
			});
	}

	async function updateTodo(description) {
		const response = await fetch(`http://127.0.0.1:8000/api/todo/${title}`);
	}

	onMount(async () => {
		answer = await getTodo();
		console.log(answer, 'this is my answer');
	});
</script>

<h1>This is your todo</h1>
<h1>{title}</h1>
{#if answer}
	<div>{answer.description}</div>
{/if}

<div>Would you like to delete this To-Do?</div>
<button on:click={deleteTodo}>Delete To-Do</button>

<a href="/">Home</a>
