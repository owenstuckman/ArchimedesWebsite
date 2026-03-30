<script>
	export let title = '';
	export let subtitle = '';
	export let image = '';
	export let dark = false;
</script>

<section class="hero" class:dark>
	{#if image}
		<img src={image} alt="Hero background" class="hero-bg" />
	{/if}
	<div class="hero-content">
		<h1>{title}</h1>
		{#if subtitle}
			<p class="subtitle">{subtitle}</p>
		{/if}
		<slot />
	</div>
</section>

<style>
	.hero {
		position: relative;
		min-height: 60vh;
		display: flex;
		align-items: center;
		justify-content: center;
		background: transparent;
		color: white;
		text-align: center;
		overflow: hidden;
	}

	.hero.dark {
		background: var(--steel);
	}

	.hero-bg {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		object-fit: cover;
		opacity: 0.3;
	}

	.hero-content {
		position: relative;
		z-index: 1;
		padding: 2rem;
		max-width: 800px;
	}

	.subtitle {
		font-size: 1.3rem;
		margin-top: 1rem;
		opacity: 0.9;
	}
</style>
