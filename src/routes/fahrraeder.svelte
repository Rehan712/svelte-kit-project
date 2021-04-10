<script>
	import { onMount } from 'svelte';

	let data = [];

	onMount(() => {
		const endpoint =
			'https://velophil.test/react-service.php?service=cycles&access_token=VMoxiRv9pyrb6MvwMMYAfNbRiU63QcCnREf4R8FVhAazP3RLDt4AGt79PFsJKhhM';
		fetch(endpoint)
			.then((r) => r.json())
			.then((r) => {
				data = r[0].data;
			});
	});
</script>

{#each data as item}
	{JSON.stringify(item)}
{:else}
	no Data
{/each}
