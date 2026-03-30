<footer class="footer">
	<div class="container">
		<div class="footer__grid">
			<div class="footer__col">
				<h4>Archimedes</h4>
				<p>Empowering STEM freshmen at Virginia Tech through hands-on engineering experiences.</p>
			</div>

			<div class="footer__col">
				<h4>Quick Links</h4>
				<ul>
					<li><a href="/about">About</a></li>
					<li><a href="/design-teams">Design Teams</a></li>
					<li><a href="/apply">Apply</a></li>
					<li><a href="/faq">FAQ</a></li>
				</ul>
			</div>

			<div class="footer__col">
				<h4>Contact</h4>
				<p>archimedesvt@gmail.com</p>
				<p>Virginia Tech<br />Blacksburg, VA 24061</p>
			</div>

      <div class="footer__col">
        <h4>Follow Us</h4>
        <div class="social">
          <a href="https://www.instagram.com/archimedes.vt/?hl=en" aria-label="Instagram">Instagram</a>
          <a href="linkedin.com/company/archimedesvt/" aria-label="LinkedIn">LinkedIn</a>
        </div>
      </div>
    </div>

    <div class="footer__bottom">
      <p>2025 Archimedes at Virginia Tech</p>
    </div>
  </div>
</footer>

<style>
	.footer {
		background: #0f1d1f;
		color: rgba(255, 255, 255, 0.85);
		padding: 4rem 0 2rem;
		border-top: 1px solid rgba(255, 255, 255, 0.06);
		font-family: var(--font-secondary);
	}

	.footer__grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(230px, 1fr));
		gap: 2.5rem;
		margin-bottom: 2.5rem;
	}

	.footer__col h4 {
		color: var(--archimedes-yellow);
		margin-bottom: 1rem;
		font-weight: 800;
		letter-spacing: 0.05em;
	}

	.footer__col p {
		color: var(--text-on-dark);
		opacity: 0.9;
		line-height: 1.6;
		font-size: 0.95rem;
	}

	.footer__col ul {
		list-style: none;
		padding: 0;
	}

	.footer__col a {
		color: var(--halogen-haze);
		text-decoration: none;
		transition: color var(--tr);
		font-weight: 500;
	}
	.footer__col a:hover {
		color: var(--luminal-yellow);
	}

	.social {
		display: flex;
		flex-direction: column;
		gap: 0.6rem;
	}

	.footer__bottom {
		border-top: 1px solid rgba(255, 255, 255, 0.06);
		text-align: center;
		padding-top: 1.25rem;
		color: rgba(255, 255, 255, 0.6);
		font-size: 0.9rem;
	}

	@media (max-width: 768px) {
		.footer {
			padding: 3rem 0 1.5rem;
		}
		.footer__grid {
			gap: 1.8rem;
		}
	}
</style>
