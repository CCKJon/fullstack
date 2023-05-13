<script>
    export let data
    console.log("this is my data", data)
    const Todos = data.items
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
<footer>test app</footer>