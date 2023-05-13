<!-- <script context="module">
    export async function load(params, fetch) {
        const Posts = await GetAllPosts()
        async function GetAllPosts(params) {
            let url = 'http://localhost:8000'
            const res = await fetch(url)
            return await res.json()
        }
        return {
            props:{
                Posts:Posts
            }
        }
    }
</script>


<script>
    export let Posts;
</script>

<svelte:head>
    <title>Posts list</title>

</svelte:head>

<section id="posts">
    {#each Posts as post }
        <p>
            <a href="{post.id}">{post.title}</a>
        </p>
    {/each}
</section> -->