<script>
	import { slide } from 'svelte/transition';

	export let items = [];
	export let placeholder = '';
	export let selected;
	let extended = false;
</script>

<div
	on:click={() => {
		extended = !extended;
	}}
	class="flex flex-col bg-white text-gray-700 rounded p-2 relative"
>
	<div class="flex justify-between items-center">
		{#if !selected}
			{placeholder}
		{:else}
			{selected}
		{/if}
		<i class="fas fa-sort-down" />
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
				>
					{item}
				</div>
			{/each}
		</div>
	{/if}
</div>
