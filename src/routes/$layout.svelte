<script>
	import '../app.scss';
	import Header from '$lib/Header/index.svelte';
</script>

<Header />

<slot />

<style global>
	@tailwind base;
	@tailwind components;
	@tailwind utilities;
</style>
