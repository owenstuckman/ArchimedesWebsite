<script lang="ts">
	import Hero from '$lib/components/Hero.svelte';

	function handleSubmit(event: SubmitEvent) {
		event.preventDefault();

		const form = event.target as HTMLFormElement;
		const formData = new FormData(form);
		formData.append('service_id', 'service_uflz7t4');
		formData.append('template_id', 'template_tipmow6');
		formData.append('user_id', 'Jb0db_Gi8slMQgNYj');

		fetch('https://api.emailjs.com/api/v1.0/email/send-form', {
			method: 'POST',
			body: formData
		})
			.then((response) => {
				if (response.ok) {
					alert('Your mail is sent!');
					form.reset();
				} else {
					return response.text().then((text) => {
						throw new Error(text);
					});
				}
			})
			.catch((error: Error) => {
				alert('Oops... ' + error.message);
			});
	}
</script>

<svelte:head>
	<title>Sponsor - Archimedes</title>
	<meta
		name="description"
		content="Support the next generation of engineers by sponsoring Archimedes at Virginia Tech."
	/>
</svelte:head>

<Hero
	title="Sponsor Archimedes"
	subtitle="Our Sponsor Package"
	image="/images/hero-sponsor.jpg"
/>

<section class="section">
	<div class="container">
		<div class="sponsor-content">
			<div class="intro-text">
				<p>
					All proceeds go directly to supporting and growing our many talented members and
					incredible projects. Please see our sponsor package for a full breakdown and more
					information about sponsoring Archimedes.
				</p>
				<a href="/sponsor.pdf" download class="btn btn--primary"> Download Sponsor Package </a>
			</div>

			<div class="sponsors-section">
				<h2>Meet Our Sponsors</h2>
				<p>
					These sponsors make it possible for freshmen engineers to gain hands-on experience, grow
					technical skills, and explore engineering from day one at Virginia Tech. We are grateful
					for their support, which enables us to provide opportunities and resources for the next
					generation of innovators.
				</p>

				<div class="sponsors-grid">
					<!-- Placeholder for sponsor logos -->
					<img src="/altec.webp" alt="altec" class="w-100" />
					<img src="/mis.webp" alt="mis" class="sponsor-picture" />
					<img src="/sec.webp" alt="sec" class="sponsor-picture" />
				</div>
			</div>

			<div class="contact-section">
				<h2>Still Have a Question?</h2>
				<p class="email-link">
					<a href="mailto:archimedesvt@gmail.com">archimedesvt@gmail.com</a>
				</p>

				<form class="sponsor-form" on:submit={handleSubmit}>
					<h3>Fill out this form and we'll get back to you as soon as possible.</h3>
					<input type="text" name="name" placeholder="Your Name" required />
					<input type="text" name="company" placeholder="Company" required />
					<input type="email" name="email" placeholder="Email" required />
					<textarea name="message" placeholder="Message" rows="5" required></textarea>
					<button type="submit" class="btn btn--primary">Submit</button>
				</form>

				<p class="note">
					If you would like to contact our treasurer or president directly, please see the contact
					information near the end of our sponsor package.
				</p>
				<p class="note">
					For general inquiries, visit our <a href="/contact">contact</a> page.
				</p>
			</div>
		</div>
	</div>
</section>

<style>
	.sponsor-picture {
		width: 200px;
	}

	.sponsor-content {
		max-width: 900px;
		margin: 0 auto;
	}

	.intro-text {
		text-align: center;
		margin-bottom: 4rem;
	}

	.intro-text p {
		font-size: 1.1rem;
		margin-bottom: 2rem;
		line-height: 1.8;
	}

	.sponsors-section {
		margin-bottom: 4rem;
	}

	.sponsors-section h2 {
		color: var(--archimedes-yellow);
		text-align: center;
		margin-bottom: 1.5rem;
	}

	.sponsors-section p {
		text-align: center;
		max-width: 700px;
		margin: 0 auto 3rem;
		line-height: 1.8;
	}

	.sponsors-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
		gap: 2rem;
	}

	.contact-section {
		background: rgba(255, 255, 255, 0.05);
		border: 1px solid rgba(255, 255, 255, 0.1);
		padding: 3rem;
		border-radius: var(--radius-md);
	}

	.contact-section h2 {
		color: var(--archimedes-yellow);
		text-align: center;
		margin-bottom: 1rem;
	}

	.email-link {
		text-align: center;
		margin-bottom: 2rem;
	}

	.email-link a {
		color: var(--text-on-dark);
		font-size: 1.2rem;
		text-decoration: none;
	}

	.email-link a:hover {
		color: var(--archimedes-yellow);
	}

	.sponsor-form {
		max-width: 500px;
		margin: 0 auto;
	}

	.sponsor-form h3 {
		text-align: center;
		margin-bottom: 1.5rem;
		font-size: 1rem;
		color: var(--text-on-dark);
	}

	.sponsor-form input,
	.sponsor-form textarea {
		width: 100%;
		padding: 12px;
		margin-bottom: 1rem;
		border: 1px solid #ddd;
		border-radius: 4px;
		font-size: 1rem;
	}

	.sponsor-form button {
		width: 100%;
	}

	.note {
		text-align: center;
		margin-top: 1rem;
		color: rgba(255, 255, 255, 0.6);
	}

	.note a {
		color: var(--archimedes-yellow);
		text-decoration: none;
	}
</style>
