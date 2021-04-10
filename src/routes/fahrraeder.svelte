<script>
	import { onMount } from 'svelte';
	import Filter from '$lib/Fahrraeder/Filter.svelte';
	import Rad from '$lib/Fahrraeder/Rad.svelte';
	let data = [];

	onMount(() => {
		const endpoint =
			'https://velophil.test/react-service.php?service=cycles&access_token=VMoxiRv9pyrb6MvwMMYAfNbRiU63QcCnREf4R8FVhAazP3RLDt4AGt79PFsJKhhM';
		fetch(endpoint)
			.then((r) => r.json())
			.then((r) => {
				data = r[0].data;
				console.log(r);
			});
	});
</script>

<section class="flex flex-col justify-center items-center h-64">
	<h2 class="text-red font-bold text-xl">Fahrräder</h2>
	<p class="flex justify-center items-center text-center w-4/5">
		Hier eine Auswahl der interessantesten Räder, die bei uns zur Probefahrt bereitstehen. Das ist
		aber noch längst nicht alles – besuchen Sie uns im Laden
	</p>
</section>

<Filter>
	{#each data as item}
		<Rad />
	{:else}
		no Data
	{/each}
</Filter>
