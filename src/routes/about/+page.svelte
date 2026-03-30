<script>
	import Hero from '$lib/components/Hero.svelte';

	const officers = [
		{ role: 'President', name: 'Nidhi Gangadharan', image: '' },
		{ role: 'VP', name: 'Indu Sanil', image: '' },
		{ role: 'Secretary', name: 'Sophie Atkisson', image: '' },
		{ role: 'External Treasurer', name: 'Kevin Xu', image: '' },
		{ role: 'Internal Treasurer', name: 'Helen Brown', image: '' },
		{ role: 'Recruitment/Publicity', name: 'Bella Guereca', image: '' },
		{ role: 'Webmaster', name: 'Owen Stuckman', image: '' }
	];
</script>

<svelte:head>
	<title>About - Archimedes</title>
	<meta
		name="description"
		content="Learn about Archimedes at Virginia Tech and our mission to empower STEM freshmen."
	/>
</svelte:head>

<Hero title="About Archimedes" subtitle="Who we are" image="/images/hero-about.png" />

<section class="section">
	<div class="container">
		<div class="about-content">
			<div class="about-section">
				<h2>Who we are</h2>
				<p>
					Archimedes is an umbrella organization that encompasses four design teams, each
					participating in different national-level collegiate STEM competitions. The teams and their
					respective competitions are managed and operated by upperclassmen leads and guided by
					Virginia Tech professors and subject matter experts.
				</p>
			</div>

			<div class="about-section">
				<h2>Our mission</h2>
				<p>
					Archimedes was founded in 2015 on the principle that STEM freshmen are passionate,
					goal-driven problem solvers who are more than capable of conquering a design challenge. We
					strive to give freshmen a more in-depth experience than they might find in an
					upperclassmen-dominated team. Archimedes provides first-year STEM students with the tools,
					funding, and mentors to excel in their design competitions.
				</p>
			</div>
			<div class="about-section">
				<h2>Meet the officers</h2>
				<div class="officers-grid">
					{#each officers as officer}
						<div class="officer-card">
							<div class="officer-avatar">
								{#if officer.image}
									<img src={officer.image} alt={officer.name} />
								{:else}
									<span class="officer-initials">
										{officer.name
											.split(' ')
											.map((n) => n[0])
											.join('')}
									</span>
								{/if}
							</div>
							<div class="officer-info">
								<p class="officer-name">{officer.name}</p>
								<p class="officer-role">{officer.role}</p>
							</div>
						</div>
					{/each}
				</div>
			</div>
		</div>
	</div>
</section>

<style>
	.about-content {
		max-width: 900px;
		margin: 0 auto;
	}

	.about-section {
		margin-bottom: 4rem;
	}

	.about-section h2 {
		color: var(--archimedes-yellow);
		margin-bottom: 1.5rem;
		text-align: center;
	}

	.about-section > p {
		font-size: 1.1rem;
		line-height: 1.8;
		text-align: center;
	}

	/* Officers */
	.officers-grid {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
		gap: 1.5rem;
		margin-top: 2rem;
	}

	.officer-card {
		background: rgba(255, 255, 255, 0.04);
		border: 1px solid rgba(255, 255, 255, 0.08);
		border-radius: var(--radius-lg);
		padding: 2rem 1.5rem;
		text-align: center;
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 1rem;
		transition:
			transform var(--tr),
			border-color var(--tr),
			background var(--tr);
	}

	.officer-card:hover {
		transform: translateY(-4px);
		border-color: rgba(255, 184, 0, 0.35);
		background: rgba(255, 255, 255, 0.07);
	}

	.officer-avatar {
		width: 88px;
		height: 88px;
		border-radius: 50%;
		background: linear-gradient(135deg, var(--archimedes-yellow), var(--incandescent-gold));
		display: flex;
		align-items: center;
		justify-content: center;
		overflow: hidden;
		flex-shrink: 0;
	}

	.officer-avatar img {
		width: 100%;
		height: 100%;
		object-fit: cover;
	}

	.officer-initials {
		font-size: 1.4rem;
		font-weight: 800;
		color: var(--steel);
		letter-spacing: 0.5px;
	}

	.officer-info {
		display: flex;
		flex-direction: column;
		gap: 0.25rem;
	}

	.officer-name {
		font-weight: 700;
		font-size: 1.1rem;
		color: var(--text-on-dark);
		margin: 0;
	}

	.officer-role {
		font-size: 0.8rem;
		font-weight: 600;
		text-transform: uppercase;
		letter-spacing: 1.2px;
		color: var(--archimedes-yellow);
		margin: 0;
	}

	@media (max-width: 768px) {
		.officers-grid {
			grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
			gap: 1rem;
		}

		.officer-card {
			padding: 1.5rem 1rem;
		}

		.officer-avatar {
			width: 72px;
			height: 72px;
		}

		.officer-initials {
			font-size: 1.15rem;
		}
	}
</style>
