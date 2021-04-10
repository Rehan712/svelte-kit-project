<script>
	let navExpand = false;
</script>

<header>
	<div class="background">
		<img src="/images/velophil-logo.png" alt="" class="headerimg" />
	</div>
	<nav>
		<div
			on:click={() => {
				navExpand = !navExpand;
			}}
		>
			{#if navExpand}
				<i class="fas fa-times" />
			{:else}
				<i class="fas fa-bars" />
				<h2>Menu</h2>
			{/if}
		</div>
		{#if navExpand}{/if}
	</nav>
</header>

<style lang="scss">
	header {
		.background {
			background-color: #f1ede3;
			position: relative;
			img {
				width: 80%;
			}
		}
		nav {
			display: flex;
			justify-content: center;
			align-items: center;
			background: #fbb900;
			color: white;
			gap: 0.5rem;
			padding: 0.5rem;
			div {
				display: flex;
				justify-content: center;
				align-items: center;
				gap: 0.5rem;
				i {
					font-size: 1.5rem;
				}
				h2 {
					margin: 0;
					padding: 0;
					font-size: 1.2rem;
				}
			}
		}
	}
</style>
