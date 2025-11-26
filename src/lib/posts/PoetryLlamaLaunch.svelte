<script lang="ts">
	import Nav from '$lib/components/Nav.svelte';
</script>

<svelte:head>
	<title>Poetry Llama: AI Meets Urdu Poetry - Kepler Systems</title>
	<meta
		name="description"
		content="Exploring how we fine-tuned Llama 3.3 70B on classical Urdu poetry to create a specialized language model."
	/>
	<meta property="og:title" content="Poetry Llama: AI Meets Urdu Poetry" />
	<meta
		property="og:description"
		content="Exploring how we fine-tuned Llama 3.3 70B on classical Urdu poetry to create a specialized language model."
	/>
	<meta property="og:type" content="article" />
</svelte:head>

<main>
	<div class="background-grid"></div>

	<Nav />

	<div class="wrapper">
		<div class="post-header">
			<h1 class="post-title">Poetry Llama: AI Meets Urdu Poetry</h1>
			<p class="post-meta">February 9, 2025</p>
			<p class="post-excerpt">
				Exploring how we fine-tuned Llama 3.3 70B on classical Urdu poetry to create a specialized
				language model.
			</p>
		</div>

		<article class="post-content">
			<p>
				We've released <strong>Poetry Llama</strong>, a 70 billion parameter language model
				fine-tuned on classical Urdu poetry. This represents months of work in bringing together
				modern AI with one of the richest poetic traditions.
			</p>

			<h2>Why Urdu Poetry?</h2>
			<p>
				Urdu poetry, with its rich traditions of ghazals, nazms, and shers, represents centuries of
				literary excellence. Poets like Ghalib, Mir, Faiz, and Iqbal have created works that
				continue to resonate deeply with millions.
			</p>

			<p>However, existing language models struggle with:</p>

			<ul>
				<li>The nuanced metaphors and imagery</li>
				<li>Classical poetic structures and meters</li>
				<li>Proper understanding of cultural context</li>
				<li>The elegant Nastaliq script</li>
			</ul>

			<h2>The Model</h2>
			<p>Poetry Llama is built on Llama 3.3 70B and fine-tuned on:</p>

			<ul>
				<li><strong>10,000 classical shers</strong> (couplets)</li>
				<li><strong>25,000 complete ghazals</strong></li>
				<li>Multiple eras and poetic styles</li>
				<li>Verified and validated content</li>
			</ul>

			<h2>Capabilities</h2>
			<p>The model can:</p>

			<ul>
				<li>Generate poetry in classical styles</li>
				<li>Complete incomplete verses</li>
				<li>Explain poetic metaphors and meanings</li>
				<li>Maintain proper meter and rhythm</li>
				<li>Work with both Roman and Nastaliq scripts</li>
			</ul>

			<h2>Technical Details</h2>
			<ul>
				<li><strong>Base Model</strong>: Llama 3.3 70B</li>
				<li><strong>Training Tokens</strong>: ~7M</li>
				<li><strong>Fine-tuning Approach</strong>: LoRA with custom tokenization</li>
				<li><strong>License</strong>: Llama license</li>
				<li><strong>Hardware</strong>: Trained on L40S GPUs</li>
			</ul>

			<h2>Try It Out</h2>
			<p>
				The model is available on <a
					href="https://huggingface.co/keplersystems/poetry-llama-3.3-70B"
					target="_blank"
					rel="noopener noreferrer">Hugging Face</a
				>. We're also working on a web demo for easy access.
			</p>

			<h2>Future Work</h2>
			<p>We're exploring:</p>

			<ul>
				<li>Expanding to other Urdu literary forms</li>
				<li>Multi-lingual poetry models</li>
				<li>Educational applications</li>
			</ul>
		</article>

		<div class="post-navigation">
			<a href="/blog" class="back-to-blog">← Back to Blog</a>
		</div>
	</div>
	<div class="bottom-margin"></div>
</main>

<style>
	:global(:root) {
		--primary: #00ffd5;
		--primary-dark: #00b4a3;
		--primary-light: #7fffef;
		--accent: #ff00ee;
		--accent-dark: #b400a7;
		--bg-dark: #001a1a;
		--bg-darker: #000d0d;
		--text: #e0fffa;
		--text-secondary: #7fffef;
		--white: #aca1cb;
		--white-two: #7f7796;
		--purple: #835fe8;
		--purple-two: #494d86;
		--font-one: 'Chakra Petch', sans-serif;
		--font-two: 'Space Mono', monospace;
	}

	:global(*) {
		box-sizing: inherit;
		margin: 0;
		padding: 0;
		font-family: var(--font-one);
		scroll-behavior: smooth;
		-webkit-tap-highlight-color: rgba(0, 0, 0, 0);
	}

	:global(html) {
		box-sizing: border-box;
	}

	:global(body) {
		margin: 0;
		padding: 0;
		line-height: 1.4;
		background-color: var(--bg-color);
		overflow-x: hidden;
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
		background-image: linear-gradient(rgba(0, 255, 213, 0.05) 1px, transparent 1px),
			linear-gradient(90deg, rgba(0, 255, 213, 0.05) 1px, transparent 1px);
		background-size: 30px 30px;
		z-index: 1;
		pointer-events: none;
	}

	.wrapper {
		margin-inline: auto;
		width: min(90%, 60rem);
		position: relative;
		z-index: 2;
	}

	.post-header {
		margin-bottom: 4rem;
		text-align: center;

		.post-title {
			font-size: 5rem;
			color: var(--primary);
			font-weight: 600;
			letter-spacing: -0.055em;
			margin: 1rem 0;
			text-shadow: 0px 0px 71px rgba(131, 95, 232, 0.3);

			@media (max-width: 768px) {
				font-size: 3rem;
			}
		}

		.post-meta {
			color: var(--text);
			margin: 1rem 0;
			font-family: var(--font-two);
			font-weight: 300;
			letter-spacing: -0.04em;
		}

		.post-excerpt {
			color: var(--text-secondary);
			font-size: 1.2rem;
			margin: 1.5rem 0;
			font-style: italic;
			font-family: var(--font-two);
			letter-spacing: -0.04em;
		}
	}

	.post-content {
		h2 {
			font-size: 2.5rem;
			color: var(--text);
			font-weight: 600;
			margin: 4rem 0 1.5rem 0;
			position: relative;

			&:not(:first-child) {
				margin-top: 4rem;
			}
		}

		p {
			color: var(--text);
			font-family: var(--font-two);
			font-size: 0.95rem;
			font-weight: 300;
			line-height: 1.6;
			letter-spacing: -0.04em;
			margin: 1.5rem 0;

			strong {
				color: var(--primary);
				font-weight: bold;
			}
		}

		ul {
			margin: 1.5rem 0;
			padding-left: 2rem;

			li {
				color: var(--text);
				font-family: var(--font-two);
				font-size: 0.95rem;
				font-weight: 300;
				line-height: 1.6;
				letter-spacing: -0.04em;
				margin: 0.8rem 0;

				strong {
					color: var(--primary);
					font-weight: bold;
				}
			}
		}

		a {
			color: var(--primary);
			text-decoration: none;
			transition: color 0.3s ease;

			&:hover {
				color: var(--primary-light);
			}
		}
	}

	.post-navigation {
		margin-top: 4rem;
		text-align: center;
		padding-top: 2rem;
		border-top: 1px solid var(--primary-dark);

		.back-to-blog {
			color: var(--accent);
			text-decoration: none;
			font-family: var(--font-two);
			font-size: 1.1rem;
			transition: all 0.3s ease;
			display: inline-block;

			&:hover {
				color: var(--accent-dark);
				transform: translateX(-5px);
			}
		}
	}

	.bottom-margin {
		height: 4rem;
	}

	@media (max-width: 768px) {
		.post-header {
			h1 {
				font-size: 2.5rem;
			}
		}

		.post-content {
			h2 {
				font-size: 2rem;
			}
		}
	}
</style>
