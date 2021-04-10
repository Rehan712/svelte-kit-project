<script>
	import { slide } from 'svelte/transition';
	import { goto } from '$app/navigation';
	let navExpand = false;
</script>

<header>
	<div
		class="bg-header"
		on:click={() => {
			goto('/');
		}}
	>
		<img src="/images/velophil-logo.png" alt="" class="w-4/5" />
	</div>
	<div
		on:click={() => {
			navExpand = !navExpand;
		}}
		class="flex justify-center items-center text-xl gap-2 font-bold bg-yellow text-white p-2"
	>
		{#if navExpand}
			<i class="fas fa-times" />
		{:else}
			<i class="fas fa-bars" />
			<h2 class="">Menu</h2>
		{/if}
	</div>
	{#if navExpand}
		<nav
			class="flex flex-col bg-yellow text-white justify-center items-center p-2 font-sans gap-6"
			transition:slide
		>
			<div
				on:click={() => {
					goto('/fahrraeder');
				}}
			>
				Räder
			</div>
			<div>Zubehör</div>
			<div>Service</div>
			<div>Ergonomie</div>
			<div>Aktivitäten</div>
			<div>galerie</div>
			<div>Über uns</div>
			<div>Kontakt</div>
			<div>Newsletter</div>
			<div>
				<input type="text" placeholder="Suche" class="p-2 placeholder-gray-600 rounded" />
			</div>
			<div
				on:click={() => {
					navExpand = !navExpand;
				}}
			>
				<i class="fas fa-times" />
			</div>
		</nav>
	{/if}
</header>
