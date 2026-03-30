<script>
	import Hero from '$lib/components/Hero.svelte';

	function handleSubmit() {
		window.open('https://forms.gle/hn8M2EEhQZfhetTR9');
	}
</script>

<svelte:head>
	<title>Apply - Archimedes</title>
	<meta
		name="description"
		content="Apply to join Archimedes at Virginia Tech and start your engineering journey."
	/>
</svelte:head>

<Hero
	title="Apply to Archimedes"
	subtitle="We're glad you're interested."
	image="/images/hero-apply.png"
/>

<section class="section">
	<div class="container">
		<div class="apply-content">
			<div class="info-box">
				<h2>Applications are now closed for 25-26!</h2>
				<p>
					Please fill out our interest form for updates and instructions on applying to Archimedes.
					You will automatically be unsubscribed from our mailing list once the recruiting season
					has ended.
				</p>
			</div>
			<center>
				<button class="btn btn--primary interest-btn" on:click={handleSubmit}>
					Click to fill out the interest form!
				</button>
			</center>
			<!-- 
            {#if !submitted}
                <form class="interest-form" on:submit={handleSubmit}>
                    <input 
                        type="email" 
                        bind:value={email}
                        placeholder="Enter your email"
                        required
                    />
                    <button type="submit" class="btn">Submit</button>
                </form>
            {:else}
                <div class="success-message">
                    <h3>Thank you!</h3>
                    <p>We've added you to our interest list. You'll receive updates about the next application period.</p>
                </div>
            {/if}
        -->
		</div>
	</div>
</section>

<style>
	.interest-btn {
		font-size: 1.1rem;
		margin-top: 1rem;
	}

	.apply-content {
		max-width: 600px;
		margin: 0 auto;
	}

	.info-box {
		background: rgba(255, 255, 255, 0.05);
		border: 1px solid rgba(255, 255, 255, 0.1);
		padding: 2rem;
		border-radius: var(--radius-md);
		text-align: center;
		margin-bottom: 3rem;
	}

	.info-box h2 {
		color: var(--archimedes-yellow);
		margin-bottom: 1rem;
	}
</style>
