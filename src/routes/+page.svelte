<script>
	import Hero from '$lib/components/Hero.svelte';
</script>

<svelte:head>
	<title>Archimedes at Virginia Tech</title>
	<meta
		name="description"
		content="We are a student organization that hosts four design teams exclusively for STEM freshmen at Virginia Tech."
	/>
</svelte:head>

<Hero
	title="Jump-start your STEM career early."
	subtitle="Get the best hands-on engineering experience right from the start, here at Virginia Tech. Open to freshmen only."
	image="/images/hero-home.jpg"
>
	<a href="/apply" class="btn btn--primary">Apply Now</a>
</Hero>

<section class="section">
	<div class="container">
		<div class="content-grid">
			<div class="content-block">
				<h2>Who are we?</h2>
				<p>
					We are a student organization that hosts four design teams exclusively for Virginia Tech
					freshmen. Guided by upperclassmen leads and subject-matter experts, freshmen have the
					unique opportunity to participate in STEM design challenges that feature hands-on work
					alongside NASA, Microsoft, ASME, and RESNA.
				</p>
			</div>

			<div class="content-block">
				<h2>No experience required.</h2>
				<p>
					No matter your intended major or experience level, Archimedes is here to accelerate and
					test your capabilities as an engineer or scientist.
				</p>
			</div>

			<div class="content-block">
				<h2>Why join?</h2>
				<p>
					Archimedes gives freshmen full creative freedom from the drawing board to the workshop.
					Members are provided with mentorship, funding, professional development opportunities, and
					more!
				</p>
			</div>
		</div>

		<div class="image-section">
			<img
				src="/images/home-team.jpg"
				alt="Archimedes team working"
				class="hero-image"
			/>
		</div>
	</div>
</section>

<style>
	.content-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
		gap: 3rem;
		margin-bottom: 4rem;
	}

	.content-block {
		text-align: center;
	}

	.content-block h2 {
		color: var(--archimedes-yellow);
		margin-bottom: 1rem;
	}

	.content-block p {
		font-size: 1.1rem;
		line-height: 1.8;
	}

	.image-section {
		margin-top: 4rem;
		width: 100%;
		display: flex;
		justify-content: center;
	}

	.image-section img {
		width: 100%;
		max-width: 1200px; /* keeps image neatly centered on large screens */
		height: auto;
		border-radius: var(--radius-lg);
		object-fit: cover;
		display: block;
		box-shadow: var(--shadow-md);
	}
</style>
