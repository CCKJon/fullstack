<script>
	import { goto } from '$app/navigation';
	import { onMount } from 'svelte';
	export let data;
	let answer;
	let title = data.title;
	let description = '';
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
				window.location = '/';
			})
			.catch((error) => {
				// Handle error
			});
	}

	function updateTodo() {
		fetch(`http://127.0.0.1:8000/api/todo/${title}?desc=${description}`, {
			method: 'PUT',
			headers: {
				'Content-Type': 'application/json'
			},
			body: JSON.stringify({
				title: title,
				desc: description
			})
		})
			.then((response) => {
				// Handle response

				window.location = '/';
			})
			.catch((error) => {
				// Handle error
			});
	}

	onMount(async () => {
		answer = await getTodo();
		console.log(answer, 'this is my answer');
	});
</script>

<h1 class="text-gray-900 grid place-items-center text-3xl font-extrabold p-3 mb-5">
	This is your todo
</h1>
<h1 class="grid place-items-center text-2xl font-extrabold">{title}</h1>

<div class="mb-16">
	{#if answer}
		<div class="grid place-items-center">{answer.description}</div>
	{/if}
</div>
<div class="grid place-items-center text-rose-default text-xl font-bold">
	This is where you can update your To-do
</div>
<form class="mb-3 grid place-items-center text-rose-lighter" on:submit|preventDefault={updateTodo}>
	New description:
	<input type="text" bind:value={description} />

	<button
		class="mt-3 mb-20 text-center grid place-items-center w-44 mx-auto rounded-md text-rose-default border-rose-default border-2 hover:bg-slate-600 font-bold"
		type="submit">Update To-do</button
	>
</form>

<div class="border-rose-lighter border-4 mx-auto w-96 h-44 text-center mb-9 rounded-lg">
	<div class="grid place-items-center mt-7 mb-5 font-extrabold text-xl">
		Are you sure you want to delete this To-Do?
	</div>
	<button
		class="mb-16 text-center grid place-items-center w-44 mx-auto rounded-md text-rose-default border-rose-default border-2 hover:bg-slate-600 font-bold"
		on:click={deleteTodo}>Delete To-Do</button
	>
</div>
<a
	class="grid place-items-center text-center, w-20 mx-auto rounded-md text-rose-default border-rose-default border-2 hover:bg-slate-600 border-b-4"
	href="/">Home</a
>
