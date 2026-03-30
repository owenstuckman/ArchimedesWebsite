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
	<title>Contact - Archimedes</title>
	<meta name="description" content="Get in touch with Archimedes at Virginia Tech." />
</svelte:head>

<Hero title="Get in Touch" dark={true} />

<section class="section">
	<div class="container">
		<div class="contact-content">
			<div class="contact-info">
				<h2>Contact Information</h2>
				<div class="contact-item">
					<h3>Email</h3>
					<a href="mailto:archimedesvt@gmail.com">archimedesvt@gmail.com</a>
				</div>

				<div class="info-links">
					<p>
						Before contacting, see our <a href="/faq">FAQ</a> to check if your question has already been
						answered.
					</p>
					<p>For sponsorship inquiries, please visit our <a href="/sponsor">sponsor page</a>.</p>
				</div>
			</div>

			<div class="contact-form">
				<h2>Send us a message</h2>
				<form on:submit={handleSubmit}>
					<input type="text" name="name" placeholder="Your Name" required />
					<input type="email" name="email" placeholder="Your Email" required />
					<textarea name="message" placeholder="Your Message" rows="6" required></textarea>
					<button type="submit" class="btn btn--primary">Send Message</button>
				</form>
			</div>
		</div>
	</div>
</section>

<style>
	.contact-content {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 4rem;
		max-width: 1000px;
		margin: 0 auto;
	}

	.contact-info h2,
	.contact-form h2 {
		color: var(--archimedes-yellow);
		margin-bottom: 2rem;
	}

	.contact-item {
		margin-bottom: 2rem;
	}

	.contact-item h3 {
		color: var(--incandescent-gold);
		font-size: 1.1rem;
		margin-bottom: 0.5rem;
	}

	.contact-item a {
		color: var(--text-on-dark);
		text-decoration: none;
		font-size: 1.1rem;
	}

	.contact-item a:hover {
		color: var(--archimedes-yellow);
	}

	.info-links {
		margin-top: 2rem;
		padding: 1.5rem;
		background: rgba(255, 255, 255, 0.05);
		border: 1px solid rgba(255, 255, 255, 0.1);
		border-radius: var(--radius-md);
	}

	.info-links p {
		margin-bottom: 0.5rem;
	}

	.info-links a {
		color: var(--archimedes-yellow);
		text-decoration: none;
		font-weight: 600;
	}

	.contact-form form {
		display: flex;
		flex-direction: column;
		gap: 1rem;
	}

	.contact-form input,
	.contact-form textarea {
		padding: 12px;
		border: 1px solid #ddd;
		border-radius: 4px;
		font-size: 1rem;
		font-family: inherit;
	}

	.contact-form button {
		align-self: flex-start;
	}

	@media (max-width: 768px) {
		.contact-content {
			grid-template-columns: 1fr;
			gap: 2rem;
		}
	}
</style>
