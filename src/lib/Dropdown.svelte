<script>
	import { slide } from 'svelte/transition';

	export let items = [];
	export let placeholder = '';
	export let selected;
	export let preApplyFilter = () => {};
	export let type;
	let extended = false;
	let preFilterTemplate = {};
	function preApplyFilterApply(item) {
		preFilterTemplate[type] = item;
		return preApplyFilter(preFilterTemplate);
	}
</script>

<div
	on:click={() => {
		extended = !extended;
	}}
	class="flex flex-col bg-white text-gray-700 rounded p-2 relative"
>
	<div class="flex justify-between items-center">
		{#if !selected}
			{placeholder} <i class="fas fa-sort-down" />
		{:else}
			{selected.name}
			<i
				class="fas fa-times"
				on:click={() => {
					selected = undefined;
				}}
			/>
		{/if}
	</div>
	<hr />

	{#if extended}
		<div
			transition:slide
			class="mt-2 md:m-0 md:absolute top-full bg-white left-0 right-0 p-2 md:mt-1"
		>
			{#each items as item}
				<div
					on:click={() => {
						selected = item;
					}}
					class="flex gap-2"
				>
					{item.name} ({preApplyFilterApply(item)})
				</div>
			{/each}
		</div>
	{/if}
</div>
