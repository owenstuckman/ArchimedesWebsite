<script lang="ts">
	import Hero from '$lib/components/Hero.svelte';

	const faqs = [
		{
			question: 'Who can apply to Archimedes?',
			answer:
				'Archimedes is exclusively for Virginia Tech freshmen. All first-year students, regardless of major or experience level, are welcome to apply.'
		},
		{
			question: 'Do I need prior engineering experience?',
			answer:
				'No! We welcome students from all backgrounds and experience levels. Our teams are designed to teach you everything you need to know.'
		},
		{
			question: 'How much time commitment is required?',
			answer:
				'Most teams meet 2-3 times per week, with additional workshop time as needed. The total commitment is typically 8-10 hours per week.'
		},
		{
			question: 'Is there a membership fee?',
			answer:
				'No, there is no membership fee. All materials, tools, and travel expenses (where applicable) are covered by Archimedes.'
		},
		{
			question: 'Can I join multiple teams?',
			answer:
				'Due to the time commitment required for each team, members can only participate in one design team per year.'
		},
		{
			question: 'When do applications open?',
			answer:
				'Applications typically open in early September for the following academic year. Join our mailing list to be notified when applications open.'
		},
		{
			question: 'What happens after I apply?',
			answer:
				'After submitting your application, you may be invited for an interview. Final decisions are typically made within two weeks of the application deadline.'
		},
		{
			question: 'Do I get academic credit?',
			answer:
				"While Archimedes itself doesn't offer academic credit, some teams' work can count towards certain course requirements. Check with your academic advisor."
		}
	];

	let openItems: Record<number, boolean> = {};

	function toggleItem(index: number) {
		openItems[index] = !openItems[index];
	}
</script>

<svelte:head>
	<title>FAQ - Archimedes</title>
	<meta
		name="description"
		content="Frequently asked questions about Archimedes at Virginia Tech."
	/>
</svelte:head>

<Hero
	title="Frequently Asked Questions"
	subtitle="Everything you need to know about joining Archimedes"
	dark={true}
/>

<section class="section">
	<div class="container">
		<div class="faq-content">
			{#each faqs as faq, index}
				<div class="faq-item" class:open={openItems[index]}>
					<button class="faq-question" on:click={() => toggleItem(index)}>
						<span>{faq.question}</span>
						<span class="icon">{openItems[index] ? '−' : '+'}</span>
					</button>
					{#if openItems[index]}
						<div class="faq-answer">
							<p>{faq.answer}</p>
						</div>
					{/if}
				</div>
			{/each}

			<div class="more-questions">
				<h3>Still have questions?</h3>
				<p>
					Feel free to reach out to us at <a href="mailto:archimedesvt@gmail.com"
						>archimedesvt@gmail.com</a
					>
					or visit our <a href="/contact">contact page</a>.
				</p>
			</div>
		</div>
	</div>
</section>

<style>
	.faq-content {
		max-width: 800px;
		margin: 0 auto;
	}

	/* Card */
	.faq-item {
		background: var(--white);
		border-radius: var(--radius-md);
		margin-bottom: 1rem;
		box-shadow: var(--shadow-sm);
		border: 1px solid rgba(0, 0, 0, 0.06);
		overflow: hidden;
		transition:
			transform var(--tr),
			box-shadow var(--tr),
			border-color var(--tr);
	}
	.faq-item.open {
		transform: translateY(-2px);
		box-shadow: var(--shadow-md);
		border-color: rgba(255, 200, 0, 0.35); /* yellow accent glow */
	}

	/* Trigger */
	.faq-question {
		width: 100%;
		padding: 1.25rem 1.5rem;
		background: var(--white);
		color: var(--steel);
		border: 0;
		text-align: left;
		font-size: 1.1rem;
		font-weight: 700;
		letter-spacing: 0.01em;
		cursor: pointer;
		display: flex;
		justify-content: space-between;
		align-items: center;
		transition:
			background var(--tr),
			color var(--tr);
	}
	.faq-question:hover {
		background: var(--halogen-haze);
	}
	.faq-question:focus-visible {
		outline: none;
		box-shadow: 0 0 0 4px rgba(255, 208, 0, 0.25);
	}

	/* Plus / caret icon */
	.icon {
		font-size: 1.4rem;
		color: var(--archimedes-yellow-bright);
		transition:
			transform var(--tr),
			color var(--tr);
	}
	.faq-item.open .icon {
		transform: rotate(45deg); /* if using + as icon */
		color: var(--archimedes-yellow);
	}

	/* Answer */
	.faq-answer {
		padding: 0 1.5rem 1.25rem;
		animation: slideDown 0.25s ease;
	}
	.faq-answer p {
		line-height: 1.65;
		color: var(--steel);
	}

	/* “More questions” CTA block */
	.more-questions {
		margin-top: 3rem;
		text-align: center;
		padding: 2rem;
		background: var(--halogen-haze);
		border-radius: var(--radius-md);
		border: 1px solid rgba(0, 0, 0, 0.06);
		color: var(--black); /* make all text black */
	}

	.more-questions h3 {
		color: var(--black);
		margin-bottom: 1rem;
		font-weight: 800;
		letter-spacing: 0.02em;
	}

	.more-questions p {
		color: var(--black);
	}

	.more-questions a {
		color: var(--black);
		text-decoration: none;
		font-weight: 700;
		transition:
			color var(--tr),
			text-decoration-color var(--tr);
	}

	.more-questions a:hover {
		color: var(--steel); /* subtle dark hover shift */
		text-decoration: underline;
	}

	@keyframes slideDown {
		from {
			opacity: 0;
			transform: translateY(-8px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}

	/* Motion-safe */
	@media (prefers-reduced-motion: reduce) {
		.faq-item,
		.faq-question,
		.icon,
		.faq-answer {
			transition: none !important;
		}
		.faq-answer {
			animation: none !important;
		}
	}
</style>
