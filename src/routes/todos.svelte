<script context="module">
	export async function load({ page, fetch, session, context }) {
		console.log('Loading ToDos');
		const url = `https://jsonplaceholder.typicode.com/todos`;
		const res = await fetch(url);

		if (res.ok) {
			return {
				props: {
					todos: await res.json()
				}
			};
		}

		return {
			status: res.status,
			error: new Error(`Could not load ${url}`)
		};
	}
</script>

<script lang="ts">
	export let todos: any[];
</script>

<svelte:head>
	<title>b-nova ToDos</title>
</svelte:head>
<h1>To Dos</h1>

<ul>
	{#each todos as todo}
		<li>
			<a href="/todos/{todo.id}" sveltekit:prefetch>
				{todo.id}: {todo.title}
			</a>
		</li>
	{/each}
</ul>
