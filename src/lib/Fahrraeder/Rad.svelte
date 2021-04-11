<script>
	import { goto } from '$app/navigation';

	export let item;
</script>

<div
	on:click={() => {
		goto(item.link);
	}}
>
	<div>
		<img src="https://dummyimage.com/400x300/222/999.png?text=Test" alt="" class="w-full" />
		<!-- <img src={item.file} alt="" /> -->
	</div>
	<h3 class="text-red font-bold text-lg">{@html item.title}</h3>
	<p>
		{@html item.text}
	</p>
</div>
