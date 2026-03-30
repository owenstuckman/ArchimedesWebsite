<script lang="ts">
	import { page } from '$app/stores';
	import { onMount, onDestroy } from 'svelte';
	import { browser } from '$app/environment';

	let mobileMenuOpen = false;

	function setBodyOverflow(val: string) {
		if (!browser) return; // guard for SSR
		document.body.style.overflow = val;
	}

	const toggleMobileMenu = () => {
		mobileMenuOpen = !mobileMenuOpen;
	};

	// Keep body overflow in sync with menu state (client only)
	$: if (browser) {
		setBodyOverflow(mobileMenuOpen ? 'hidden' : '');
	}

	// Close menu (and restore overflow) whenever route changes
	$: if ($page.url) {
		mobileMenuOpen = false;
	}

	onMount(() => {
		// nothing extra needed; reactive statement above handles it
	});

	onDestroy(() => {
		setBodyOverflow('');
	});
</script>

<header class="nav">
	<nav class="nav__inner container">
		<!-- Brand -->
		<a href="/" class="brand">
			<div class="image-section">
				<img src="/logoheader.png" alt="logoheader" class="hero-image" />
			</div>
		</a>

		<!-- Mobile toggle -->
		<button
			class="hamburger"
			on:click={toggleMobileMenu}
			aria-label="Toggle navigation"
			aria-expanded={mobileMenuOpen}
		>
			<span class:open={mobileMenuOpen}></span>
			<span class:open={mobileMenuOpen}></span>
			<span class:open={mobileMenuOpen}></span>
		</button>

		<!-- Overlay (must NOT be self-closing in Svelte) -->
		<div
			class="menu-overlay"
			class:open={mobileMenuOpen}
			on:click={toggleMobileMenu}
			on:keydown={(e) => e.key === 'Escape' && toggleMobileMenu()}
			role="button"
			tabindex="-1"
			aria-label="Close menu"
		></div>

		<!-- Desktop / Mobile menu -->
		<ul class="menu" class:open={mobileMenuOpen}>
			<li><a href="/" class:current={$page.url.pathname === '/'}>Home</a></li>
			<li><a href="/about" class:current={$page.url.pathname === '/about'}>About</a></li>
			<li>
				<a href="/design-teams" class:current={$page.url.pathname === '/design-teams'}
					>Design Teams</a
				>
			</li>
			<li><a href="/apply" class:current={$page.url.pathname === '/apply'}>Apply</a></li>
			<li><a href="/faq" class:current={$page.url.pathname === '/faq'}>FAQ</a></li>
			<li><a href="/sponsor" class:current={$page.url.pathname === '/sponsor'}>Sponsor</a></li>
			<li><a href="/contact" class:current={$page.url.pathname === '/contact'}>Contact</a></li>
		</ul>
	</nav>
</header>

<style>
	.image-section {
		height: 68px;
		display: flex;
		align-items: center;
	}

	.image-section img {
		height: 52px;
		width: auto;
		object-fit: contain;
		border-radius: var(--radius-md);
	}

	.nav {
		background: rgba(25, 43, 46, 0.95);
		backdrop-filter: blur(6px);
		border-bottom: 1px solid rgba(255, 255, 255, 0.06);
		position: sticky;
		top: 0;
		z-index: 60;
	}

	.nav__inner {
		height: 68px;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}

	.brand {
		display: flex;
		align-items: center;
		text-decoration: none;
		color: var(--text-on-dark);
	}

	.menu {
		list-style: none;
		display: flex;
		gap: 1.75rem;
		align-items: center;
	}

	.menu a {
		color: var(--text-on-dark);
		text-decoration: none;
		font-weight: 600;
		padding: 10px 0;
		transition:
			color var(--tr),
			opacity var(--tr);
	}

	.menu a:hover {
		color: var(--luminal-yellow);
	}

	.menu a.current {
		color: var(--archimedes-yellow);
	}

	.menu a.current::after {
		transform: scaleX(1);
	}

	.hamburger {
		display: none;
		flex-direction: column;
		justify-content: center;
		gap: 5px;
		width: 36px;
		height: 36px;
		background: transparent;
		border: 1px solid rgba(255, 255, 255, 0.12);
		border-radius: var(--radius-sm);
		cursor: pointer;
		padding: 6px;
		transition:
			border-color var(--tr),
			background var(--tr);
	}

	.hamburger:hover {
		border-color: var(--archimedes-yellow);
		background: rgba(255, 200, 0, 0.06);
	}

	.hamburger span {
		display: block;
		width: 100%;
		height: 2px;
		background: var(--archimedes-yellow);
		transition:
			transform var(--tr),
			opacity var(--tr);
	}

	.hamburger span.open:nth-child(1) {
		transform: translateY(7px) rotate(45deg);
	}

	.hamburger span.open:nth-child(2) {
		opacity: 0;
	}

	.hamburger span.open:nth-child(3) {
		transform: translateY(-7px) rotate(-45deg);
	}

	/* overlay */
	.menu-overlay {
		display: none;
		position: fixed;
		inset: 68px 0 0 0;
		background: rgba(10, 18, 20, 0.98);
		z-index: 30;
		transition: opacity var(--tr);
		opacity: 0;
		pointer-events: none;
	}

	.menu-overlay.open {
		display: block;
		opacity: 1;
		pointer-events: auto;
	}

	@media (max-width: 900px) {
		.hamburger {
			display: flex;
		}

		.image-section {
			display: none;
		}

		.menu {
			position: fixed;
			inset: 68px 0 auto 0;
			background: transparent;
			box-shadow: var(--shadow-lg);
			flex-direction: column;
			align-items: flex-start;
			padding: 20px 24px 28px;
			gap: 0.25rem;
			transform: translateX(-100%);
			transition:
				transform var(--tr) ease,
				opacity var(--tr);
			z-index: 40;
			pointer-events: none;
		}

		.menu.open {
			transform: translateX(0);
			pointer-events: auto;
			background: #102224; /* solid panel background when open */
		}

		.menu li {
			width: 100%;
		}

		.menu a {
			width: 100%;
			padding: 12px 4px;
			border-bottom: 1px solid rgba(255, 255, 255, 0.06);
		}
	}
</style>
