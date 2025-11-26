<script lang="ts">
	import Chip from '$lib/components/Chip.svelte';
	import Nav from '$lib/components/Nav.svelte';

	const posts = [
		{
			title: 'Introducing Curated PAARI Datasets: 8 Indian Languages for AI Research',
			date: 'November 26, 2025',
			category: 'Datasets',
			excerpt:
				"Curated journalism datasets from the People's Archive of Rural India across 8 Indian languages, ready for AI research and language modeling.",
			slug: 'introducing-paari-datasets'
		},
		{
			title: 'The Challenge of Building Multilingual AI',
			date: 'November 26, 2025',
			category: 'Research',
			excerpt:
				'Why Indian language AI matters and the unique challenges we face in creating inclusive language models.',
			slug: 'building-multilingual-ai'
		},
		{
			title: 'Poetry Llama: AI Meets Urdu Poetry',
			date: 'February 9, 2025',
			category: 'Models',
			excerpt:
				'Exploring how we fine-tuned Llama 3.3 70B on classical Urdu poetry to create a specialized language model.',
			slug: 'poetry-llama-launch'
		}
	];
</script>

<svelte:head>
	<title>Blog - Kepler Systems</title>
	<meta
		name="description"
		content="Latest updates and insights from Kepler Systems on multilingual AI, datasets, and language models."
	/>
	<meta property="og:title" content="Blog - Kepler Systems" />
	<meta
		property="og:description"
		content="Latest updates and insights from Kepler Systems on multilingual AI, datasets, and language models."
	/>
	<script
		defer
		src="https://analytics.auna.li/script.js"
		data-website-id="c2811ea4-cc1f-4b5b-ad40-8cd7b4ed02a3"
	></script>
</svelte:head>

<main>
	<div class="background-grid"></div>

	<Nav />

	<div class="wrapper">
		<div class="blog-header">
			<h1>Blog</h1>
			<p>Latest updates on multilingual AI and language technology.</p>
		</div>

		<div class="blog-grid">
			{#each posts as post (post.slug)}
				<a href="/blog/{post.slug}" class="post-card">
					<div class="post-content">
						<div class="post-meta">
							<Chip name={post.category} />
							<span class="post-date">{post.date}</span>
						</div>
						<h3>{post.title}</h3>
						<p class="post-excerpt">{post.excerpt}</p>
					</div>
				</a>
			{/each}
		</div>
	</div>
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

	.blog-header {
		text-align: center;
		margin-bottom: 4rem;

		h1 {
			font-size: 5rem;
			color: var(--primary);
			font-weight: 600;
			letter-spacing: -0.055em;
			margin-bottom: 1rem;
			text-shadow: 0px 0px 71px rgba(131, 95, 232, 0.3);

			@media (max-width: 768px) {
				font-size: 3rem;
			}
		}

		p {
			color: var(--text);
			font-family: var(--font-two);
			font-size: 1.1rem;
			font-weight: 300;
			letter-spacing: -0.04em;
			max-width: 600px;
			margin: 0 auto;
		}
	}

	.blog-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
		gap: 2rem;
		margin-top: 3rem;
	}

	.post-card {
		text-decoration: none;
		color: inherit;
		display: block;
		background: rgba(0, 255, 213, 0.05);
		border: 1px solid var(--primary-dark);
		border-radius: 12px;
		padding: 2rem;
		transition: all 0.3s ease;
		position: relative;
		overflow: hidden;

		&::after {
			content: '\2192';
			position: absolute;
			bottom: 2rem;
			right: 2rem;
			font-size: 1.5rem;
			color: var(--accent);
			opacity: 0;
			transform: translateX(-10px);
			transition: all 0.3s ease;
		}

		&:hover {
			transform: translateY(-5px);
			box-shadow: 0 10px 30px rgba(0, 255, 213, 0.1);
			background: rgba(0, 255, 213, 0.08);

			&::after {
				opacity: 1;
				transform: translateX(0);
			}
		}
	}

	.post-content {
		position: relative;
		z-index: 1;
	}

	.post-meta {
		display: flex;
		align-items: center;
		justify-content: space-between;
		margin-bottom: 1rem;
	}

	.post-date {
		color: var(--text-secondary);
		font-family: var(--font-two);
		font-size: 0.95rem;
		font-weight: 400;
		letter-spacing: -0.04em;
	}

	h3 {
		font-size: 1.8rem;
		color: var(--text);
		font-weight: 600;
		letter-spacing: -0.06em;
		margin-bottom: 1rem;
		line-height: 1.3;
	}

	.post-excerpt {
		color: var(--text-secondary);
		font-family: var(--font-two);
		font-size: 0.95rem;
		font-weight: 300;
		line-height: 1.6;
		letter-spacing: -0.04em;
	}

	@media (max-width: 768px) {
		.blog-header {
			h1 {
				font-size: 3rem;
			}

			p {
				font-size: 1rem;
			}
		}

		.blog-grid {
			grid-template-columns: 1fr;
			gap: 1.5rem;
		}

		.post-card {
			padding: 1.5rem;
		}

		h3 {
			font-size: 1.5rem;
		}

		.post-meta {
			flex-direction: column;
			align-items: flex-start;
			gap: 0.5rem;
		}
	}
</style>
