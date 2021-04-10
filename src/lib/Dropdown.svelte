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
	class="flex flex-col bg-white text-gray-700 rounded p-2 m-2 "
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
		<div transition:slide class="mt-2">
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
