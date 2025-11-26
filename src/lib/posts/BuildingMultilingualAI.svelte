<script lang="ts">
	import Nav from '$lib/components/Nav.svelte';
</script>

<svelte:head>
	<title>The Challenge of Building Multilingual AI - Kepler Systems</title>
	<meta
		name="description"
		content="Why Indian language AI matters and the unique challenges we face in creating inclusive language models."
	/>
	<meta property="og:title" content="The Challenge of Building Multilingual AI" />
	<meta
		property="og:description"
		content="Why Indian language AI matters and the unique challenges we face in creating inclusive language models."
	/>
	<meta property="og:type" content="article" />
</svelte:head>

<main>
	<div class="background-grid"></div>

	<Nav />

	<div class="wrapper">
		<div class="post-header">
			<h1 class="post-title">The Challenge of Building Multilingual AI</h1>
			<p class="post-meta">November 26, 2025</p>
			<p class="post-excerpt">
				Why Indian language AI matters and the unique challenges we face in creating inclusive
				language models.
			</p>
		</div>

		<article class="post-content">
			<p>
				Building AI that understands and works with Indian languages is harder than it looks. Here's
				what we've learned.
			</p>

			<h2>The English Bias</h2>
			<p>
				Most AI models are predominantly trained on English text. This creates several problems:
			</p>

			<ul>
				<li>
					<strong>Tokenization Issues</strong>: Models treat Indian language words inefficiently
				</li>
				<li><strong>Cultural Context</strong>: Missing cultural nuances and context</li>
				<li><strong>Data Scarcity</strong>: Limited quality training data</li>
				<li><strong>Script Complexity</strong>: Multiple writing systems and diacritical marks</li>
			</ul>

			<h2>Why It Matters</h2>
			<p>India has:</p>

			<ul>
				<li><strong>22 official languages</strong></li>
				<li><strong>19,500+ dialects</strong></li>
				<li><strong>1.4 billion people</strong>, many preferring their native language</li>
				<li>Rich literary and cultural traditions in each language</li>
			</ul>

			<p>Yet AI advancement has largely left these languages behind.</p>

			<h2>Our Approach</h2>

			<h3>1. Data Collection</h3>
			<p>We focus on:</p>

			<ul>
				<li>High-quality, verified content</li>
				<li>Diverse sources (literature, journalism, social media)</li>
				<li>Proper licensing and attribution</li>
				<li>Community involvement</li>
			</ul>

			<h3>2. Proper Preprocessing</h3>
			<ul>
				<li>Script-specific normalization</li>
				<li>Maintaining linguistic nuances</li>
				<li>Handling mixed-script text</li>
				<li>Preserving cultural context</li>
			</ul>

			<h3>3. Evaluation</h3>
			<p>Beyond perplexity scores:</p>

			<ul>
				<li>Cultural appropriateness</li>
				<li>Linguistic accuracy</li>
				<li>Real-world usability</li>
				<li>Community feedback</li>
			</ul>

			<h2>Challenges We Face</h2>

			<h3>Technical</h3>
			<ul>
				<li>Limited compute resources</li>
				<li>Lack of standard benchmarks</li>
				<li>Tokenization inefficiency</li>
				<li>Cross-script handling</li>
			</ul>

			<h3>Social</h3>
			<ul>
				<li>Data availability and licensing</li>
				<li>Community trust and involvement</li>
				<li>Balancing tradition with innovation</li>
				<li>Ensuring inclusive representation</li>
			</ul>

			<h2>Progress So Far</h2>
			<p>We've released:</p>

			<ul>
				<li><strong>8 PAARI language datasets</strong></li>
				<li><strong>Poetry Llama</strong> for Urdu</li>
				<li><strong>UrduShers</strong> and <strong>UrduGhazals</strong> datasets</li>
			</ul>

			<p>But this is just the beginning.</p>

			<h2>Looking Forward</h2>
			<p>Our goals:</p>

			<ol>
				<li>Expand to more Indian languages</li>
				<li>Build specialized domain models</li>
				<li>Create accessible tools</li>
				<li>Foster an open-source community</li>
				<li>Ensure ethical and inclusive AI</li>
			</ol>

			<h2>Join Us</h2>
			<p>Building truly multilingual AI requires:</p>

			<ul>
				<li>Linguists and cultural experts</li>
				<li>Machine learning researchers</li>
				<li>Data contributors</li>
				<li>Community feedback</li>
				<li>Computational resources</li>
			</ul>

			<p>
				Interested in contributing? Contact us at <a href="mailto:contact@kepler.systems"
					>contact@kepler.systems</a
				>
			</p>
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

		h3 {
			font-size: 1.8rem;
			color: var(--text-secondary);
			font-weight: 600;
			letter-spacing: -0.06em;
			margin: 2rem 0 1rem 0;
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

		ul,
		ol {
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

			h3 {
				font-size: 1.5rem;
			}
		}
	}
</style>
