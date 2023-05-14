<script>
	import { onMount } from 'svelte';
	export let data;
	console.log('this is my data', data);
	let Todos = data.items;
	onMount(() => {
		Todos = Todos;
	});
</script>

<header>NavBar</header>

<h1 class="grid place-items-center text-9xl">Tooooooooo-Dooooooooooooooo List</h1>
<div>Todo lists are very cool, trust me</div>

{#each Todos as todo}
	<div>
		<a href={`/${todo.title}`}>{todo.title}</a>
		<p>{todo.description}</p>
	</div>
{/each}

<div>
	<div class="text-white bg-black h-10 w-10">
		<p class="hello">End of List</p>
		<a id="Im_an_id" href="/new_todo">Create a new To-Do</a>
	</div>
</div>

<style>
	div {
		color: rgb(20, 126, 67);
	}
	.hello {
		color: rgb(44, 46, 179);
	}
	#Im_an_id {
		color: gold;
	}
</style>
