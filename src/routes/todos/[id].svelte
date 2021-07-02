<!-- src/routes/todos/[id].svelte -->
<script context="module">
	export async function load({ page, fetch, session, context }) {
		const id = page.params.id;
		console.log('Loading To Do ' + id);

		const url = `https://jsonplaceholder.typicode.com/todos/${id}`;
		const res = await fetch(url);

		if (res.ok) {
			return {
				props: {
					todo: await res.json()
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
	export let todo;
</script>

<svelte:head>
	<title>b-nova To Do {todo.title}</title>
</svelte:head>
title: {todo.title}
