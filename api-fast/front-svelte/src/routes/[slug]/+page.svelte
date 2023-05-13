<script>
	import { onMount } from 'svelte';
	export let data;
	let answer;
	let title = data.title;
	async function getTodo(Title) {
		const response = await fetch(`http://127.0.0.1:8000/api/todo/${Title}`);
		const data = await response.json();
		return data;
	}

	console.log(answer, 'oh yeah this is my answer');
	onMount(async () => {
		answer = await getTodo(title);
		console.log(answer, 'this is my answer');
	});
</script>

<h1>This is your todo</h1>
<h1>{title}</h1>
{#if answer}
	<div>{answer.description}</div>
{/if}

<a href="/">Home</a>
