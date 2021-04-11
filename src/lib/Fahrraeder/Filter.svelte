<script>
	import Dropdown from '$lib/Dropdown.svelte';
	import { onMount } from 'svelte';
	import { page } from '$app/stores';
	import { goto } from '$app/navigation';

	export let items = [];

	let antriebe = [],
		fahrradtypen = [],
		marken = [];
	let filterParams = {};
	let itemsout = items;

	onMount(() => {
		items.forEach((item) => {
			Object.keys(item.taxonomies).forEach((key) => {
				if (item.taxonomies[key] == 'antrieb') {
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
		let tempAntriebe = [];
		loop1: for (let i = 0; i < antriebe.length; i++) {
			const elementi = antriebe[i];

			loop2: for (let j = 0; j < items.length; j++) {
				const elementj = items[j];

				if (elementj.taxonomies_grouped.antrieb[elementi]) {
					tempAntriebe.push({
						name: elementi,
						slugg: elementj.taxonomies_grouped.antrieb[elementi]
					});
					continue loop1;
				}
			}
		}
		antriebe = tempAntriebe;

		let tempType = [];
		loop1: for (let i = 0; i < fahrradtypen.length; i++) {
			const elementi = fahrradtypen[i];

			loop2: for (let j = 0; j < items.length; j++) {
				const elementj = items[j];

				if (elementj.taxonomies_grouped.fahrradtyp[elementi]) {
					tempType.push({
						name: elementi,
						slugg: elementj.taxonomies_grouped.fahrradtyp[elementi]
					});
					continue loop1;
				}
			}
		}
		fahrradtypen = tempType;

		let tempMarke = [];
		loop1: for (let i = 0; i < marken.length; i++) {
			const elementi = marken[i];

			loop2: for (let j = 0; j < items.length; j++) {
				const elementj = items[j];

				if (elementj.taxonomies_grouped.marke[elementi]) {
					tempMarke.push({
						name: elementi,
						slugg: elementj.taxonomies_grouped.marke[elementi]
					});
					continue loop1;
				}
			}
		}
		marken = tempMarke;

		$page.params.searchParams.split('/').forEach((e) => {
			if (
				marken.find((i) => {
					return i.slugg === e;
				})
			) {
				filterParams.marke = marken.find((i) => {
					return i.slugg === e;
				});
			}
			if (
				fahrradtypen.find((i) => {
					return i.slugg === e;
				})
			) {
				filterParams.type = fahrradtypen.find((i) => {
					return i.slugg === e;
				});
			}
			if (
				antriebe.find((i) => {
					return i.slugg === e;
				})
			) {
				filterParams.antrieb = antriebe.find((i) => {
					return i.slugg === e;
				});
			}
			console.log(
				antriebe.find((i) => {
					return i.slugg === e;
				}),
				antriebe,
				e,
				filterParams
			);
		});

		console.log($page.params.searchParams.split('/'));
		applyFilter(items);
	});

	function applyFilter(items, searchParams) {
		if (!filterParams) return;
		itemsout = items
			.filter(
				(bicycle) =>
					!filterParams.marke || bicycle.taxonomies_slugged[filterParams.marke.slugg] === 'marke'
			)
			.filter(
				(bicycle) =>
					!filterParams.type || bicycle.taxonomies_slugged[filterParams.type.slugg] === 'fahrradtyp'
			)
			.filter(
				(bicycle) =>
					!filterParams.antrieb ||
					bicycle.taxonomies_slugged[filterParams.antrieb.slugg] === 'antrieb'
			);
	}

	function getNewURL() {
		return `/fahrraeder/${filterParams.marke ? filterParams.marke.slugg + '/' : ''}${
			filterParams.type ? filterParams.type.slugg + '/' : ''
		}${filterParams.antrieb ? filterParams.antrieb.slugg + '/' : ''}`;
	}
</script>

<section
	className='bg-yellow text-white relative p-4 grid grid-cols-1 md:grid-cols-3 lg:grid-cols-4 gap-4'
>
	<div>
		Marke
		<Dropdown bind:items={marken} placeholder={'Marke'} bind:selected={filterParams.marke} />
	</div>
	<div>
		Fahrradtyp
		<Dropdown
			bind:items={fahrradtypen}
			placeholder={'Fahrradtyp'}
			bind:selected={filterParams.type}
		/>
	</div>
	<div>
		Antrieb
		<Dropdown bind:items={antriebe} placeholder={'Antrieb'} bind:selected={filterParams.antrieb} />
	</div>
	<button
		className='bg-red p-4 rounded-full w-full md:col-span-3 lg:col-span-1'
		on:click={() => {
			applyFilter(items, filterParams);
			goto(getNewURL());
		}}
	>
		Anzeigen
	</button>
</section>

<section className='grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-4 p-2'>
	<slot items={itemsout} />
</section>
