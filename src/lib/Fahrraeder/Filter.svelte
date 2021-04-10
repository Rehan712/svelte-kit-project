<script>
	import Dropdown from '$lib/Dropdown.svelte';
	import { page } from '$app/stores';
	import { onMount } from 'svelte';

	export let items = [];
	let antriebe = [],
		fahrradtypen = [],
		marken = [];
	let filterParams = {};
	let { host, path, query, params } = $page;

	onMount(() => {
		items.forEach((item) => {
			Object.keys(item.taxonomies).forEach((key) => {
				if (item.taxonomies[key] == 'antrieb') {
					console.log(antriebe, key);
					if (!antriebe.includes(key)) {
						antriebe.push(key);
					}
				}
				if (item.taxonomies[key] == 'marke') {
					if (!marken.includes(key)) {
						marken.push(key);
					}
				}
				if (item.taxonomies[key] == 'fahrradtyp') {
					if (!fahrradtypen.includes(key)) {
						fahrradtypen.push(key);
					}
				}
			});
		});
	});
	function filter() {
		console.log(items);
		let excludedFilter;
		items
			.filter(
				(bicycle) =>
					!filterParams.marke ||
					bicycle.taxonomies_slugged[filterParams.marke] === 'marke' ||
					excludedFilter === 'marke'
			)
			.filter(
				(bicycle) =>
					!filterParams.type ||
					bicycle.taxonomies_slugged[filterParams.type] === 'fahrradtyp' ||
					excludedFilter === 'fahrradtyp'
			)
			.filter(
				(bicycle) =>
					!filterParams.antrieb ||
					bicycle.taxonomies_slugged[filterParams.antrieb] === 'antrieb' ||
					excludedFilter === 'antrieb'
			)
			.filter((bicycle) => !angebot || bicycle.taxonomies['Angebote anzeigen'] === 'angebot');
	}
</script>

<section
	class="bg-yellow text-white relative p-4 grid grid-cols-1 md:grid-cols-3 lg:grid-cols-4 gap-4"
>
	<div>
		Marke
		<Dropdown items={marken} placeholder={'Marke'} bind:selected={filterParams.marke} />
	</div>
	<div>
		Fahrradtyp
		<Dropdown items={fahrradtypen} placeholder={'Fahrradtyp'} bind:selected={filterParams.type} />
	</div>
	<div>
		Antrieb
		<Dropdown items={antriebe} placeholder={'Antrieb'} bind:selected={filterParams.antrieb} />
	</div>
	<button class="bg-red p-4 rounded-full w-full md:col-span-3 lg:col-span-1" on:click={filter}>
		Anzeigen
	</button>
</section>

<section class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-4 p-2">
	<slot {items} />
</section>
