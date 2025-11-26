<script lang="ts">
	import Chip from '$lib/components/Chip.svelte';
	import Nav from '$lib/components/Nav.svelte';

	let isIntersecting = false;

	function handleIntersection(entries) {
		entries.forEach((entry) => {
			if (entry.isIntersecting) {
				isIntersecting = true;
			}
		});
	}
</script>

<svelte:head>
	<title>Kepler Systems</title>
	<meta property="og:type" content="website" />
	<meta property="og:title" content="Kepler Systems" />
	<meta
		property="og:description"
		content="Building the future of AI through collaborative research, shared datasets, and open-source models."
	/>
	<meta property="og:url" content="https://kepler.systems" />
	<meta property="og:image" content="https://kepler.systems/logo.png" />
	<script
		defer
		src="https://analytics.auna.li/script.js"
		data-website-id="c2811ea4-cc1f-4b5b-ad40-8cd7b4ed02a3"
	></script>

	<link rel="icon" type="image/png" href="/favicon-96x96.png" sizes="96x96" />
	<link rel="icon" type="image/svg+xml" href="/favicon.svg" />
	<link rel="shortcut icon" href="/favicon.ico" />
	<link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png" />
	<link rel="manifest" href="/site.webmanifest" />
</svelte:head>

<main>
	<div class="background-grid"></div>

	<Nav />

	<section class="hero-section wrapper">
		<div class="orbital-system">
			<div class="orbit orbit-1"></div>
			<div class="orbit orbit-2"></div>
			<div class="orbit orbit-3"></div>
		</div>
		<h1>kepler.systems</h1>
		<p class="hero-text">We build AI and share what works</p>
		<div class="hero-chips">
			<Chip name="Neural Networks" />
			<Chip name="Deep Learning" />
			<Chip name="AI Systems" />
		</div>
	</section>

	<section id="products" class="wrapper products-section">
		<div class="section-header">
			<span class="section-label">Open Research</span>
			<h2>Datasets & Models</h2>
			<p class="subtitle">Latest: Multilingual Rural India Journalism Datasets</p>
		</div>

		<div class="products-grid">
			<div class="product-card featured">
				<div class="product-content">
					<div class="product-icon">🌾</div>
					<h3>PAARI Datasets</h3>
					<p>
						Multilingual journalism datasets from the People's Archive of Rural India covering rural life and culture.
					</p>
					<ul class="feature-list">
						<li>8 Indian languages: Hindi, Urdu, Punjabi, Tamil, Telugu, Marathi, Gujarati, English</li>
						<li>7,650 professional journalism articles</li>
						<li>19.9M tokens with language-specific text normalization</li>
						<li>Parquet format, ready for text generation and classification</li>
					</ul>
					<div class="tags">
						<Chip name="Dataset" />
						<Chip name="Multilingual" />
						<Chip name="Open Access" />
					</div>
					<a href="/blog/introducing-paari-datasets" class="hf-link">
						Read more →
					</a>
				</div>
				<div class="product-stats">
					<div class="stat">
						<span class="value">8</span>
						<span class="label">Languages</span>
					</div>
					<div class="stat">
						<span class="value">7.6K</span>
						<span class="label">Articles</span>
					</div>
					<div class="stat">
						<span class="value">19.9M</span>
						<span class="label">Tokens</span>
					</div>
				</div>
			</div>

			<div class="product-card featured">
				<div class="product-content">
					<div class="product-icon">🤖</div>
					<h3>Poetry Llama</h3>
					<p>
						Large language model fine-tuned for Urdu poetry understanding and generation
					</p>
					<ul class="feature-list">
						<li>70 billion parameters</li>
						<li>Trained on diverse Urdu poetry</li>
						<li>Llama license</li>
					</ul>
					<div class="tags">
						<Chip name="LLM" />
						<Chip name="Open Source" />
						<Chip name="Urdu" />
					</div>
					<a
						href="https://huggingface.co/keplersystems/poetry-llama-3.3-70B"
						class="hf-link"
						target="_blank"
					>
						View on Hugging Face 🤗
					</a>
				</div>
				<div class="product-stats">
					<div class="stat">
						<span class="value">70B</span>
						<span class="label">Parameters</span>
					</div>
					<div class="stat">
						<span class="value">7M</span>
						<span class="label">Tokens</span>
					</div>
				</div>
			</div>

			<div class="product-card">
				<div class="product-content">
				<div class="product-icon">📚</div>
				<h3>UrduShers-10k</h3>
				<p>Comprehensive collection of classical Urdu poetry couplets</p>
					<ul class="feature-list">
						<li>10,000 shers</li>
						<li>Multiple poets and eras</li>
						<li>Quality validated</li>
						<li>CC BY-SA 4.0 license</li>
					</ul>
					<div class="tags">
						<Chip name="Dataset" />
						<Chip name="Poetry" />
					</div>
					<a
						href="https://huggingface.co/datasets/keplersystems/UrduShers-10k"
						class="hf-link"
						target="_blank"
					>
						View on Hugging Face 🤗
					</a>
				</div>
			</div>

			<div class="product-card">
				<div class="product-content">
					<div class="product-icon">📖</div>
					<h3>UrduGhazals-25k</h3>
					<p>Comprehensive dataset of Urdu ghazals with metadata</p>
					<ul class="feature-list">
						<li>25,000 complete ghazals</li>
						<li>Multiple poets and eras</li>
						<li>CC BY-SA 4.0 license</li>
					</ul>
					<div class="tags">
						<Chip name="Dataset" />
						<Chip name="Literature" />
					</div>
					<a
						href="https://huggingface.co/datasets/keplersystems/UrduGhazals-25k"
						class="hf-link"
						target="_blank"
					>
						View on Hugging Face 🤗
					</a>
				</div>
			</div>
		</div>
	</section>

	<section class="wrapper coming-soon-section">
		<div class="section-header">
			<span class="section-label">Coming Soon</span>
			<h2>Future Developments</h2>
			<p class="subtitle">Stay tuned for upcoming releases and updates</p>
		</div>

		<div class="coming-soon-card">
			<div class="card-content">
				<span class="icon">🔬</span>
				<h3>Research & Technology</h3>
				<p>
					We're working on exciting new developments in AI research and technology. Follow us on
					social media to stay updated.
				</p>
				<div class="tags">
					<Chip name="Research" />
					<Chip name="Technology" />
					<Chip name="Updates" />
				</div>
			</div>
		</div>
	</section>

	<footer id="contact" class="wrapper footer">
		<div class="footer-content">
			<div class="footer-section">
				<h4>Kepler Systems</h4>
				<p>Building AI research and open-source tools.</p>
			</div>
			<div class="footer-section">
				<h4>Contact</h4>
				<a href="mailto:contact@kepler.systems">contact@kepler.systems</a>
			</div>
			<div class="footer-section">
				<h4>Follow Us</h4>
				<div class="social-links">
					<a href="https://x.com/KeplerSystems" target="_blank">X / Twitter</a>
					<a href="https://huggingface.co/keplersystems" target="_blank">Hugging Face</a>
					<!-- <a href="#" target="_blank">GitHub</a> -->
				</div>
			</div>
		</div>
		<div class="footer-bottom">
			<a href="https://auna.li">Built with ❤️ in India 🇮🇳 by AunAli K.</a>
			<p>&copy; 2025 Kepler Systems. All rights reserved.</p>
		</div>
	</footer>
</main>

<style lang="scss">
	:root {
		--primary: #00ffd5;
		--primary-dark: #00b4a3;
		--primary-light: #7fffef;
		--accent: #ff00ee;
		--accent-dark: #b400a7;
		--bg-dark: #001a1a;
		--bg-darker: #000d0d;
		--text: #e0fffa;
		--text-secondary: #7fffef;
	}

	main {
		background: linear-gradient(180deg, var(--bg-darker) 0%, var(--bg-dark) 100%);
		min-height: 100vh;
		position: relative;
		overflow: hidden;
	}

	.background-grid {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background-image:
			linear-gradient(rgba(0, 255, 213, 0.05) 1px, transparent 1px),
			linear-gradient(90deg, rgba(0, 255, 213, 0.05) 1px, transparent 1px);
		background-size: 30px 30px;
		z-index: 1;
		pointer-events: none;
	}

	.hero-section {
		text-align: center;
		padding: 8rem 0;
		position: relative;
		z-index: 2;

		h1 {
			font-size: 5rem;
			color: var(--primary);
			margin-bottom: 2rem;
			text-shadow: 0 0 30px rgba(0, 255, 213, 0.3);
		}

		.hero-text {
			color: var(--text-secondary);
			font-size: 1.4rem;
			max-width: 800px;
			margin: 0 auto 3rem;
			line-height: 1.6;
		}

		.hero-chips {
			display: flex;
			gap: 1rem;
			justify-content: center;
			margin-top: 2rem;
		}
	}

	.orbital-system {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		z-index: -1;

		.orbit {
			position: absolute;
			border: 1px dashed var(--primary-dark);
			border-radius: 50%;
			animation: rotate 20s linear infinite;

			&-1 {
				width: 300px;
				height: 300px;
			}

			&-2 {
				width: 500px;
				height: 500px;
				animation-direction: reverse;
			}

			&-3 {
				width: 700px;
				height: 700px;
			}
		}
	}

	.section-header {
		text-align: center;
		margin-bottom: 4rem;

		.section-label {
			color: var(--accent);
			text-transform: uppercase;
			letter-spacing: 0.2em;
			font-size: 0.9rem;
			display: block;
			margin-bottom: 1rem;
		}

		h2 {
			color: var(--primary);
			font-size: 3rem;
			margin-bottom: 1rem;
		}

		.subtitle {
			color: var(--text-secondary);
			font-size: 1.2rem;
		}
	}

	.products-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
		gap: 2rem;
		margin-top: 2rem;
	}

	.product-card {
		background: rgba(0, 255, 213, 0.05);
		border: 1px solid var(--primary-dark);
		border-radius: 12px;
		padding: 2rem;
		transition: all 0.3s ease;

		&.featured {
			grid-column: 1 / -1;
			display: grid;
			grid-template-columns: 2fr 1fr;
			gap: 2rem;
		}

		&:hover {
			transform: translateY(-5px);
			box-shadow: 0 10px 30px rgba(0, 255, 213, 0.1);
		}

		.product-icon {
			font-size: 2.5rem;
			margin-bottom: 1.5rem;
		}

		h3 {
			color: var(--primary);
			font-size: 1.8rem;
			margin-bottom: 1rem;
		}

		p {
			color: var(--text);
			margin-bottom: 1.5rem;
			line-height: 1.6;
		}

		.feature-list {
			list-style: none;
			margin: 1.5rem 0;
			padding: 0;

			li {
				color: var(--text-secondary);
				margin-bottom: 0.5rem;
				padding-left: 1.5rem;
				position: relative;

				&::before {
					content: '→';
					position: absolute;
					left: 0;
					color: var(--accent);
				}
			}
		}
	}

	.hf-link {
		display: inline-block;
		color: var(--accent);
		text-decoration: none;
		margin-top: 1rem;
		transition: all 0.3s ease;

		&:hover {
			color: var(--accent-dark);
			transform: translateX(5px);
		}
	}

	.product-stats {
		display: flex;
		flex-direction: column;
		justify-content: center;
		gap: 2rem;
		padding: 2rem;
		border-left: 1px dashed var(--primary-dark);

		.stat {
			text-align: center;

			.value {
				display: block;
				font-size: 2.5rem;
				color: var(--primary);
				font-weight: bold;
				margin-bottom: 0.5rem;
			}

			.label {
				color: var(--text-secondary);
				font-size: 0.9rem;
				text-transform: uppercase;
				letter-spacing: 0.1em;
			}
		}
	}

	.coming-soon-section {
		margin-top: 8rem;
	}

	.coming-soon-card {
		background: rgba(255, 0, 238, 0.05);
		border: 1px solid var(--accent-dark);
		border-radius: 12px;
		padding: 3rem;
		text-align: center;
		transition: all 0.3s ease;
		max-width: 800px;
		margin: 0 auto;

		&:hover {
			transform: translateY(-5px);
			background: rgba(255, 0, 238, 0.08);
		}

		.icon {
			font-size: 4rem;
			margin-bottom: 2rem;
			display: block;
		}

		h3 {
			color: var(--primary);
			font-size: 2rem;
			margin-bottom: 1.5rem;
		}

		p {
			color: var(--text);
			font-size: 1.2rem;
			line-height: 1.6;
			margin-bottom: 2rem;
		}

		.tags {
			display: flex;
			gap: 1rem;
			justify-content: center;
		}
	}

	.footer {
		margin-top: 8rem;
		padding: 4rem 0 2rem;
		border-top: 1px dashed var(--primary-dark);
	}

	.footer-content {
		display: grid;
		grid-template-columns: 2fr 1fr 1fr;
		gap: 4rem;
		margin-bottom: 4rem;

		@media (max-width: 768px) {
			grid-template-columns: 1fr;
			gap: 2rem;
		}
	}

	.footer-section {
		h4 {
			color: var(--primary);
			font-size: 1.2rem;
			margin-bottom: 1rem;
		}

		p,
		a {
			color: var(--text-secondary);
			text-decoration: none;
			transition: color 0.3s ease;

			&:hover {
				color: var(--primary);
			}
		}
	}

	.social-links {
		display: flex;
		gap: 1rem;
	}

	.footer-bottom {
		text-align: center;
		padding-top: 2rem;
		border-top: 1px dashed var(--primary-dark);
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 0.5rem;

		p, a {
			color: var(--text-secondary);
			font-size: 0.9rem;
			margin: 0;
			text-decoration: none;
		}

		a:hover {
			color: var(--primary);
		}
	}

	@keyframes rotate {
		from {
			transform: translate(-50%, -50%) rotate(0deg);
		}
		to {
			transform: translate(-50%, -50%) rotate(360deg);
		}
	}

	@media (max-width: 768px) {
		.hero-section h1 {
			font-size: 3rem;
		}

		.product-card.featured {
			grid-template-columns: 1fr;

			.product-stats {
				border-left: none;
				border-top: 1px dashed var(--primary-dark);
			}
		}
	}
</style>
