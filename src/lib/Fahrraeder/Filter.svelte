<script>
	import Dropdown from '$lib/Dropdown.svelte';

	let filterParams = {};

	export let items = [];

	function filter() {
		console.log(filterParams);
	}
</script>

<section class="bg-yellow text-white relative p-4">
	<div>
		Marke
		<Dropdown items={['test']} placeholder={'Marke'} bind:selected={filterParams.marke} />
	</div>
	<div>
		Fahrradtyp
		<Dropdown items={['test']} placeholder={'Fahrradtyp'} bind:selected={filterParams.type} />
	</div>
	<div>
		Antrieb
		<Dropdown items={['test']} placeholder={'Antrieb'} bind:selected={filterParams.antrieb} />
	</div>
	<button class="bg-red p-4 rounded-full w-full" on:click={filter}> Anzeigen </button>
</section>

<section>
	<slot {items} />
</section>
