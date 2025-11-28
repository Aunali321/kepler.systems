<script lang="ts">
	import Nav from '$lib/components/Nav.svelte';
	import { onMount } from 'svelte';

	// Language mapping and colors
	const languageNames = {
		pa: 'Punjabi',
		gu: 'Gujarati',
		ur: 'Urdu',
		ta: 'Tamil',
		te: 'Telugu',
		hi: 'Hindi',
		mr: 'Marathi',
		en: 'English'
	};

	const languageColors = {
		pa: '#FF6B6B',
		gu: '#4ECDC4',
		ur: '#45B7D1',
		ta: '#96CEB4',
		te: '#FFEAA7',
		hi: '#DDA0DD',
		mr: '#98D8C8',
		en: '#F7DC6F'
	};

	// PARI Dataset information from Hugging Face
	const datasetInfo = {
		HI: {
			name: 'Hindi',
			code: 'hi',
			script: 'Devanagari',
			size: 'n<1K',
			url: 'https://huggingface.co/datasets/keplersystems/PAARI-Hindi'
		},
		UR: {
			name: 'Urdu',
			code: 'ur',
			script: 'Arabic',
			size: 'n<1K',
			url: 'https://huggingface.co/datasets/keplersystems/PAARI-Urdu'
		},
		PA: {
			name: 'Punjabi',
			code: 'pa',
			script: 'Gurmukhi',
			size: 'n<1K',
			url: 'https://huggingface.co/datasets/keplersystems/PAARI-Punjabi'
		},
		MR: {
			name: 'Marathi',
			code: 'mr',
			script: 'Devanagari',
			size: 'n<1K',
			url: 'https://huggingface.co/datasets/keplersystems/PAARI-Marathi'
		},
		TA: {
			name: 'Tamil',
			code: 'ta',
			script: 'Tamil',
			size: 'n<1K',
			url: 'https://huggingface.co/datasets/keplersystems/PAARI-Tamil'
		},
		TE: {
			name: 'Telugu',
			code: 'te',
			script: 'Telugu',
			size: 'n<1K',
			url: 'https://huggingface.co/datasets/keplersystems/PAARI-Telugu'
		},
		EN: {
			name: 'English',
			code: 'en',
			script: 'Latin',
			size: 'n<1K',
			url: 'https://huggingface.co/datasets/keplersystems/PAARI-English'
		},
		GU: {
			name: 'Gujarati',
			code: 'gu',
			script: 'Gujarati',
			size: 'n<1K',
			url: 'https://huggingface.co/datasets/keplersystems/PAARI-Gujarati'
		}
	};

	// Language stats for datasets (tokens from LLM training datasets)
	const languageStats = {
		PA: { tokens: 4277490, articles: 978, size: 7.4 },
		GU: { tokens: 2918993, articles: 976, size: 7.3 },
		UR: { tokens: 2365924, articles: 963, size: 6.0 },
		TA: { tokens: 2232056, articles: 975, size: 6.7 },
		TE: { tokens: 2211858, articles: 743, size: 5.9 },
		HI: { tokens: 2102270, articles: 976, size: 6.9 },
		MR: { tokens: 2097149, articles: 974, size: 6.9 },
		EN: { tokens: 1741555, articles: 965, size: 4.4 }
	};

	onMount(async () => {
		// Import Chart.js dynamically
		const Chart = (await import('chart.js/auto')).default;

		// Initialize charts
		function initCharts() {
			// Articles chart
			const articlesCtx = document.getElementById('articlesChart')?.getContext('2d');
			if (articlesCtx) {
				new Chart(articlesCtx, {
					type: 'bar',
					data: {
						labels: Object.keys(languageStats).map((lang) => languageNames[lang.toLowerCase()]),
						datasets: [
							{
								label: 'Articles Count',
								data: Object.values(languageStats).map((lang) => lang.articles),
								backgroundColor: Object.keys(languageStats).map(
									(lang) => languageColors[lang.toLowerCase()] + '80'
								),
								borderColor: Object.keys(languageStats).map(
									(lang) => languageColors[lang.toLowerCase()]
								),
								borderWidth: 2,
								borderRadius: 8
							}
						]
					},
					options: {
						responsive: true,
						maintainAspectRatio: false,
						plugins: {
							legend: {
								labels: { color: '#ffffff' }
							}
						},
						scales: {
							y: {
								beginAtZero: true,
								ticks: { color: '#ffffff' },
								grid: { color: 'rgba(255, 255, 255, 0.1)' }
							},
							x: {
								ticks: { color: '#ffffff' },
								grid: { color: 'rgba(255, 255, 255, 0.1)' }
							}
						}
					}
				});
			}

			// Token distribution pie chart
			const tokenCtx = document.getElementById('tokenChart')?.getContext('2d');
			if (tokenCtx) {
				new Chart(tokenCtx, {
					type: 'doughnut',
					data: {
						labels: Object.keys(languageStats).map((lang) => languageNames[lang.toLowerCase()]),
						datasets: [
							{
								data: Object.values(languageStats).map((lang) => lang.tokens),
								backgroundColor: Object.keys(languageStats).map(
									(lang) => languageColors[lang.toLowerCase()] + '80'
								),
								borderColor: Object.keys(languageStats).map(
									(lang) => languageColors[lang.toLowerCase()]
								),
								borderWidth: 2
							}
						]
					},
					options: {
						responsive: true,
						maintainAspectRatio: false,
						plugins: {
							legend: {
								position: 'right',
								labels: {
									color: '#ffffff',
									padding: 20
								}
							}
						}
					}
				});
			}
		}

		// Populate language cards
		function populateLanguageCards() {
			const grid = document.getElementById('languageGrid');
			if (!grid) return;

			Object.entries(languageStats).forEach(([lang, stats]) => {
				const info = datasetInfo[lang];
				const card = document.createElement('div');
				card.className = 'card fade-in';
				const cardColor = languageColors[lang.toLowerCase()];
				card.innerHTML = `
                    <div class="card-header">
                        <div class="card-icon">📚</div>
                        <div style="flex: 1;">
                            <div class="card-title">${languageNames[lang.toLowerCase()]}</div>
                            <div class="card-subtitle">${info.script} Script</div>
                        </div>
                        <div class="language-badge" style="background: ${cardColor}30; border: 1px solid ${cardColor}; color: ${cardColor};">
                            ${lang}
                        </div>
                    </div>
                    <div class="card-stats">
                        <div class="card-stat">
                            <span class="card-stat-number">${(stats.tokens / 1000000).toFixed(1)}M</span>
                            <span class="card-stat-label">Tokens</span>
                        </div>
                        <div class="card-stat">
                            <span class="card-stat-number">${stats.articles}</span>
                            <span class="card-stat-label">Articles</span>
                        </div>
                        <div class="card-stat">
                            <span class="card-stat-number">${stats.size} MB</span>
                            <span class="card-stat-label">Size</span>
                        </div>
                    </div>
                    <div style="text-align: center;">
                        <a href="${info.url}" target="_blank" class="hf-link">
                            View on Hugging Face 🤗
                        </a>
                    </div>
                `;
				grid.appendChild(card);
			});
		}

		// Initialize animations
		function initAnimations() {
			const observer = new IntersectionObserver((entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						entry.target.style.animationDelay = Math.random() * 0.5 + 's';
						entry.target.classList.add('fade-in');
					}
				});
			});

			document.querySelectorAll('.card, .stat-card').forEach((el) => {
				observer.observe(el);
			});
		}

		// Add copy buttons to code blocks
		function addCopyButtons() {
			const codeBlocks = document.querySelectorAll('pre');
			codeBlocks.forEach((block) => {
				const button = document.createElement('button');
				button.className = 'copy-button';
				button.innerHTML = '📋 Copy';
				button.addEventListener('click', async () => {
					const code = block.querySelector('code')?.textContent || '';
					try {
						await navigator.clipboard.writeText(code);
						button.innerHTML = '✓ Copied!';
						button.classList.add('copied');
						setTimeout(() => {
							button.innerHTML = '📋 Copy';
							button.classList.remove('copied');
						}, 2000);
					} catch (err) {
						button.innerHTML = '✗ Failed';
						setTimeout(() => {
							button.innerHTML = '📋 Copy';
						}, 2000);
					}
				});
				block.style.position = 'relative';
				block.appendChild(button);
			});
		}

		// Initialize everything
		initCharts();
		populateLanguageCards();
		initAnimations();
		addCopyButtons();
	});
</script>

<svelte:head>
	<title
		>Introducing Curated PARI Datasets: 8 Indian Languages for AI Research | Kepler Systems</title
	>
	<meta
		name="description"
		content="Curated multilingual journalism datasets from PARI covering Hindi, Urdu, Punjabi, Tamil, Telugu, Marathi, Gujarati & English. 7,650+ articles, 19.9M tokens for AI research and language modeling."
	/>
	<meta
		name="keywords"
		content="Indian languages dataset, multilingual AI, Hindi dataset, Urdu dataset, Punjabi dataset, Tamil dataset, Telugu dataset, Marathi dataset, Gujarati dataset, PARI, rural India, journalism dataset, language modeling, text generation, LLM training"
	/>
	<meta name="author" content="Kepler Systems" />
	<meta name="robots" content="index, follow" />
	<link rel="canonical" href="https://kepler.systems/blog/introducing-paari-datasets" />

	<!-- Open Graph / Facebook -->
	<meta property="og:type" content="article" />
	<meta property="og:url" content="https://kepler.systems/blog/introducing-paari-datasets" />
	<meta
		property="og:title"
		content="Introducing Curated PARI Datasets: 8 Indian Languages for AI Research"
	/>
	<meta
		property="og:description"
		content="Curated multilingual journalism datasets from PARI covering Hindi, Urdu, Punjabi, Tamil, Telugu, Marathi, Gujarati & English. 7,650+ articles for AI research."
	/>
	<meta property="og:site_name" content="Kepler Systems" />
	<meta property="article:published_time" content="2025-11-25T00:00:00Z" />
	<meta property="article:author" content="Kepler Systems" />
	<meta property="article:tag" content="datasets" />
	<meta property="article:tag" content="AI" />
	<meta property="article:tag" content="multilingual" />
	<meta property="article:tag" content="Indian languages" />

	<!-- Twitter -->
	<meta name="twitter:card" content="summary_large_image" />
	<meta name="twitter:url" content="https://kepler.systems/blog/introducing-paari-datasets" />
	<meta
		name="twitter:title"
		content="Introducing Curated PARI Datasets: 8 Indian Languages for AI Research"
	/>
	<meta
		name="twitter:description"
		content="Curated multilingual journalism datasets from PARI covering Hindi, Urdu, Punjabi, Tamil, Telugu, Marathi, Gujarati & English. 7,650+ articles for AI research."
	/>

	<!-- Structured Data -->
	<script type="application/ld+json">
		{JSON.stringify({
			"@context": "https://schema.org",
			"@type": "BlogPosting",
			"headline": "Introducing Curated PARI Datasets: 8 Indian Languages for AI Research",
			"description": "Curated multilingual journalism datasets from the People's Archive of Rural India across 8 Indian languages",
			"author": {
				"@type": "Organization",
				"name": "Kepler Systems"
			},
			"publisher": {
				"@type": "Organization",
				"name": "Kepler Systems",
				"url": "https://kepler.systems"
			},
			"datePublished": "2025-11-25",
			"dateModified": "2025-11-25",
			"keywords": "Indian languages, datasets, NLP, multilingual, Hindi, Urdu, Punjabi, Tamil, Telugu, Marathi, Gujarati, PARI",
			"articleSection": "Datasets",
			"url": "https://kepler.systems/blog/introducing-paari-datasets",
			"mainEntityOfPage": {
				"@type": "WebPage",
				"@id": "https://kepler.systems/blog/introducing-paari-datasets"
			},
			"about": [
				{
					"@type": "Dataset",
					"name": "PARI Multilingual Datasets",
					"description": "Journalism articles from People's Archive of Rural India in 8 Indian languages",
					"url": "https://huggingface.co/keplersystems",
					"keywords": ["Hindi", "Urdu", "Punjabi", "Tamil", "Telugu", "Marathi", "Gujarati", "English", "Indian languages", "rural India"],
					"license": "Free to use and consume",
					"distribution": {
						"@type": "DataDownload",
						"encodingFormat": "parquet",
						"contentUrl": "https://huggingface.co/keplersystems"
					},
					"measurementTechnique": "Text processing and normalization",
					"variableMeasured": ["article count", "token count", "language coverage"],
					"includedInDataCatalog": {
						"@type": "DataCatalog",
						"name": "Hugging Face Datasets"
					}
				}
			],
			"inLanguage": ["hi", "ur", "pa", "ta", "te", "mr", "gu", "en"]
		})}
	</script>

	<!-- FAQ Schema for SEO -->
	<script type="application/ld+json">
		{JSON.stringify({
			"@context": "https://schema.org",
			"@type": "FAQPage",
			"mainEntity": [
				{
					"@type": "Question",
					"name": "What languages are included in the PARI datasets?",
					"acceptedAnswer": {
						"@type": "Answer",
						"text": "The PARI datasets include 8 Indian languages: Hindi, Urdu, Punjabi, Tamil, Telugu, Marathi, Gujarati, and English. Together they contain 7,650 articles and 19.9M tokens."
					}
				},
				{
					"@type": "Question",
					"name": "How can I use the PARI datasets?",
					"acceptedAnswer": {
						"@type": "Answer",
						"text": "You can use the PARI datasets for text generation, language modeling, text classification, cross-lingual research, cultural analysis, and training multilingual AI models. All datasets are available on Hugging Face and can be loaded using the datasets library."
					}
				},
				{
					"@type": "Question",
					"name": "What is the source of the PARI datasets?",
					"acceptedAnswer": {
						"@type": "Answer",
						"text": "The datasets are sourced from the People's Archive of Rural India (PARI), a journalism platform documenting rural life, agriculture, social issues, and cultural stories across India."
					}
				},
				{
					"@type": "Question",
					"name": "Are the PARI datasets free to use?",
					"acceptedAnswer": {
						"@type": "Answer",
						"text": "Yes, the PARI datasets are freely available on Hugging Face for research and development purposes. Users should respect the original journalism attribution and cite PARI when using the datasets."
					}
				}
			]
		})}
	</script>

	<link
		href="https://fonts.googleapis.com/css2?family=Chakra+Petch:ital,wght@0,300;0,400;0,500;0,600;0,700;1,300;1,400;1,500;1,600;1,700&family=Space+Mono:ital,wght@0,400;0,700;1,400;1,700&display=swap"
		rel="stylesheet"
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
		<div class="post-header">
			<h1 class="post-title">
				Introducing Curated PARI Datasets: 8 Indian Languages for AI Research
			</h1>
			<p class="post-meta">November 26, 2025</p>
			<p class="post-excerpt">
				Curated journalism datasets from the People's Archive of Rural India across 8 Indian
				languages, ready for AI research and language modeling.
			</p>
		</div>

		<article class="post-content">
			<p>
				We've released multilingual journalism datasets from the People's Archive of Rural India
				(PARI).
			</p>

			<!-- Hero Stats -->
			<div class="hero-stats">
				<div class="stat-card fade-in">
					<span class="stat-number">8</span>
					<span class="stat-label">Languages</span>
				</div>
				<div class="stat-card fade-in">
					<span class="stat-number">7,650</span>
					<span class="stat-label">Total Articles</span>
				</div>
				<div class="stat-card fade-in">
					<span class="stat-number">19.9M</span>
					<span class="stat-label">Total Tokens</span>
				</div>
				<div class="stat-card fade-in">
					<span class="stat-number">51.5 MB</span>
					<span class="stat-label">Total Size</span>
				</div>
			</div>

			<h2>Why This Matters</h2>
			<p>
				Indian languages represent some of the world's most widely spoken yet technologically
				underrepresented languages. While Hindi alone has over 600 million speakers and languages
				like Telugu, Tamil, and Marathi each have 70+ million speakers, they lack the quality
				datasets needed for training modern AI systems.
			</p>

			<p>These PARI datasets help address this critical gap by providing:</p>
			<ul>
				<li>
					<strong>Authentic voices:</strong> Real journalism capturing rural India's stories, not synthetic
					or translated content
				</li>
				<li>
					<strong>Cultural context:</strong> Content grounded in the lived experiences of rural communities
				</li>
				<li>
					<strong>Linguistic diversity:</strong> Coverage across multiple scripts (Devanagari, Arabic,
					Gurmukhi, Tamil, Telugu, Gujarati)
				</li>
				<li>
					<strong>Quality over quantity:</strong> Professionally written, edited content from respected
					journalists
				</li>
			</ul>

			<h2>What is PARI?</h2>
			<p>
				The People's Archive of Rural India documents the lives, cultures, and stories of rural
				India through professional journalism. These stories, written in multiple Indian languages,
				capture rural life often overlooked in mainstream media.
			</p>

			<h2>Dataset Overview</h2>
			<p>We've compiled and processed journalism articles across <strong>8 languages</strong>:</p>

			<ul>
				<li><strong>Hindi (हिन्दी)</strong> - 2.1M tokens, 976 articles</li>
				<li><strong>Urdu (اردو)</strong> - 2.4M tokens, 963 articles</li>
				<li><strong>Punjabi (ਪੰਜਾਬੀ)</strong> - 4.3M tokens, 978 articles</li>
				<li><strong>Marathi (मराठी)</strong> - 2.1M tokens, 974 articles</li>
				<li><strong>Tamil (தமிழ்)</strong> - 2.2M tokens, 975 articles</li>
				<li><strong>Telugu (తెలుగు)</strong> - 2.2M tokens, 743 articles</li>
				<li><strong>English</strong> - 1.7M tokens, 965 articles</li>
				<li><strong>Gujarati (ગુજરાતી)</strong> - 2.9M tokens, 976 articles</li>
			</ul>

			<!-- Charts Section -->
			<section class="charts-section">
				<div class="chart-container">
					<h3 class="chart-title">Articles Distribution by Language</h3>
					<div class="chart-wrapper chart-wrapper-small">
						<canvas id="articlesChart"></canvas>
					</div>
				</div>

				<div class="chart-container">
					<h3 class="chart-title">Token Distribution</h3>
					<div class="chart-wrapper">
						<canvas id="tokenChart"></canvas>
					</div>
				</div>
			</section>

			<h2>Datasets by Language</h2>

			<div class="language-grid" id="languageGrid">
				<!-- Language cards will be populated by JavaScript -->
			</div>

			<h2>Sample Data</h2>
			<p>
				Explore the actual content from one of our datasets. Here's a preview of the Gujarati
				dataset showing article titles and content:
			</p>

			<div class="hf-embed-container">
				<iframe
					src="https://huggingface.co/datasets/keplersystems/PAARI-Gujarati/embed/viewer/default/train"
					frameborder="0"
					width="100%"
					height="560px"
					title="PAARI Gujarati Dataset Sample"
				></iframe>
			</div>

			<h2>Dataset Features</h2>
			<p>Each dataset includes:</p>

			<ul>
				<li><strong>Clean Text</strong>: HTML entity decoding and tag removal</li>
				<li>
					<strong>Script-Specific Normalization</strong>: Language-appropriate text processing
				</li>
				<li><strong>Parquet Format</strong>: Efficient storage and fast loading</li>
				<li><strong>Structured Data</strong>: Title and full article content</li>
			</ul>

			<h2>Use Cases</h2>
			<p>These datasets are designed for:</p>

			<ul>
				<li>Text generation and language modeling</li>
				<li>Cross-lingual research</li>
				<li>Cultural and linguistic analysis</li>
				<li>Training multilingual AI models</li>
			</ul>

			<h2>License & Usage</h2>
			<p>
				PARI Content is licensed under <a
					href="https://creativecommons.org/licenses/by-nc-nd/4.0/"
					target="_blank"
					rel="noopener noreferrer"
					>Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND
					4.0)</a
				>.
			</p>

			<p>
				You're free to share and distribute with attribution. Commercial use and derivatives require
				permission from PARI.
			</p>

			<ul>
				<li>
					<a
						href="https://ruralindiaonline.org/termsofservices"
						target="_blank"
						rel="noopener noreferrer">Terms of Service</a
					>
				</li>
				<li>
					<a href="https://ruralindiaonline.org/en/copyrights" target="_blank" rel="noopener noreferrer"
						>Copyright Details</a
					>
				</li>
				<li>Contact: contact@ruralindiaonline.org</li>
			</ul>

			<p>We encourage you to:</p>

			<ul>
				<li>Cite PARI and this dataset when publishing research or building applications</li>
				<li>
					Support PARI's mission by <a
						href="https://ruralindiaonline.org/en/volunteer/"
						target="_blank"
						rel="noopener noreferrer">becoming a volunteer</a
					>
					or
					<a href="https://ruralindiaonline.org/en/donate/" target="_blank" rel="noopener noreferrer"
						>donating</a
					> to fund their work
				</li>
				<li>
					Respect the journalism and maintain proper attribution to the original content creators
				</li>
			</ul>

			<h2>Get Started</h2>
			<p>
				All datasets are available on <a
					href="https://huggingface.co/keplersystems"
					target="_blank"
					rel="noopener noreferrer">Hugging Face</a
				> under open licenses. Visit the individual dataset pages for more details and download links.
			</p>

			<h2>Usage Example</h2>
			<p>Here's how to use these datasets with the Hugging Face <code>datasets</code> library:</p>

			<pre><code
					>from datasets import load_dataset

# Load the dataset (example: Hindi)
dataset = load_dataset("keplersystems/PAARI-Hindi")

# Access examples
for article in dataset["train"]:
    print(f"Title: {'{'}article['title']{'}'}")
    print(f"Text: {'{'}article['text'][:200]{'}'} ...")
</code></pre>

			<h2>Citation</h2>
			<p>If you use these datasets in your research, please cite:</p>

			<pre><code
					>@misc{'{'}pari-datasets-2025,
    title={'{'}PARI Multilingual Datasets{'}'},
    author={'{'}People's Archive of Rural India and Kepler Systems{'}'},
    howpublished={'{'}\url{'{'}https://huggingface.co/keplersystems{'}'}{'}'},
    year={'{'}2025{'}'}
{'}'}
</code></pre>

			<h2>Acknowledgments</h2>
			<p>
				These datasets are derived from the journalism work of the <a
					href="https://ruralindiaonline.org"
					target="_blank"
					rel="noopener noreferrer">People's Archive of Rural India (PAARI)</a
				> and Rural India Online. We thank all the journalists, photographers, and contributors who created
				this invaluable content documenting rural Indian life and culture.
			</p>

			<p>
				PARI's mission to document and preserve stories from rural India has created a unique
				resource that not only serves journalism but also enables AI research and development for
				underrepresented languages and communities.
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

		h3 {
			font-size: 1.8rem;
			color: var(--text);
			font-weight: 600;
			margin: 2.5rem 0 1rem 0;
			position: relative;
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

			em {
				color: var(--primary-light);
				font-style: italic;
			}

			code {
				background: rgba(0, 255, 213, 0.1);
				color: var(--primary);
				padding: 0.2rem 0.4rem;
				border-radius: 4px;
				font-family: var(--font-two);
				font-size: 0.9rem;
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

		pre {
			background: rgba(0, 255, 213, 0.05);
			border: 1px solid rgba(0, 255, 213, 0.3);
			border-radius: 10px;
			padding: 1.5rem;
			margin: 1.5rem 0;
			overflow-x: auto;
			position: relative;

			code {
				background: transparent;
				color: var(--text);
				padding: 0;
				font-family: var(--font-two);
				font-size: 0.85rem;
				line-height: 1.6;
			}
		}
	}

	/* HuggingFace Embed Container */
	.hf-embed-container {
		margin: 2rem 0;
		border-radius: 10px;
		overflow: hidden;
		border: 1px solid rgba(0, 255, 213, 0.3);
		background: rgba(0, 255, 213, 0.05);

		iframe {
			display: block;
			border: none;
		}
	}

	/* Copy Button */
	:global(.copy-button) {
		position: absolute;
		top: 0.75rem;
		right: 0.75rem;
		background: rgba(0, 255, 213, 0.2);
		border: 1px solid rgba(0, 255, 213, 0.4);
		color: var(--primary);
		padding: 0.4rem 0.8rem;
		border-radius: 6px;
		font-size: 0.8rem;
		font-family: var(--font-two);
		cursor: pointer;
		transition: all 0.2s ease;
		z-index: 10;

		&:hover {
			background: rgba(0, 255, 213, 0.3);
			transform: scale(1.05);
		}

		&.copied {
			background: rgba(0, 255, 100, 0.2);
			border-color: rgba(0, 255, 100, 0.4);
			color: #00ff64;
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

	/* Hero Stats Section */
	.hero-stats {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
		gap: 1rem;
		margin: 2rem 0;
	}

	.stat-card {
		background: rgba(0, 255, 213, 0.1);
		border: 1px solid rgba(0, 255, 213, 0.3);
		border-radius: 12px;
		padding: 1.25rem;
		text-align: center;
		backdrop-filter: blur(5px);
		transition: all 0.3s ease;

		&:hover {
			transform: translateY(-3px);
			background: rgba(0, 255, 213, 0.15);
			box-shadow: 0 8px 20px rgba(0, 255, 213, 0.2);
		}

		.stat-number {
			font-size: 2rem;
			font-weight: bold;
			color: var(--primary);
			display: block;
		}

		.stat-label {
			color: var(--text);
			text-transform: uppercase;
			letter-spacing: 0.1rem;
			font-size: 0.75rem;
			font-family: var(--font-two);
		}
	}

	/* Charts Section */
	.charts-section {
		margin: 3rem 0;

		.chart-container {
			background: rgba(0, 255, 213, 0.05);
			border: 1px solid rgba(0, 255, 213, 0.3);
			border-radius: 15px;
			padding: 2rem;
			margin: 2rem 0;
			backdrop-filter: blur(10px);

			.chart-title {
				text-align: center;
				color: var(--primary);
				margin-bottom: 2rem;
				font-size: 1.5rem;
				font-weight: 600;
			}

			.chart-wrapper {
				position: relative;
				height: 400px;
				margin: 1rem 0;
			}

			.chart-wrapper-small {
				height: 300px;
			}
		}
	}

	/* Language Cards Grid */
	.language-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
		gap: 1.5rem;
		margin: 3rem 0;
	}

	:global(.card) {
		background: rgba(0, 255, 213, 0.05);
		border: 1px solid rgba(0, 255, 213, 0.3);
		border-radius: 12px;
		padding: 1.25rem;
		backdrop-filter: blur(10px);
		transition: all 0.3s ease;
		position: relative;
		overflow: hidden;

		&:hover {
			transform: translateY(-5px);
			background: rgba(0, 255, 213, 0.08);
			box-shadow: 0 10px 30px rgba(0, 255, 213, 0.15);
		}
	}

	:global(.card-header) {
		display: flex;
		align-items: center;
		margin-bottom: 1rem;
	}

	:global(.card-icon) {
		font-size: 1.5rem;
		margin-right: 0.75rem;
	}

	:global(.card-title) {
		font-size: 1.2rem;
		font-weight: 600;
		color: var(--primary);
	}

	:global(.card-subtitle) {
		color: var(--text);
		font-size: 0.8rem;
		margin-top: 0.25rem;
		font-family: var(--font-two);
	}

	:global(.language-badge) {
		padding: 0.3rem 0.6rem;
		border-radius: 6px;
		font-size: 0.75rem;
		font-weight: 600;
		text-transform: uppercase;
		letter-spacing: 0.05em;
		font-family: var(--font-two);
	}

	:global(.card-stats) {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: 0.75rem;
		margin: 1rem 0;
	}

	:global(.card-stat) {
		text-align: center;
	}

	:global(.card-stat-number) {
		font-size: 1.2rem;
		font-weight: bold;
		color: var(--primary);
		display: block;
	}

	:global(.card-stat-label) {
		color: var(--text);
		font-size: 0.7rem;
		text-transform: uppercase;
		letter-spacing: 0.05rem;
		font-family: var(--font-two);
	}

	:global(.hf-link) {
		color: var(--accent);
		text-decoration: none;
		margin-top: 0.75rem;
		transition: all 0.3s ease;
		font-weight: 500;
		font-family: var(--font-two);
		font-size: 0.85rem;

		&:hover {
			color: var(--accent-dark);
		}
	}

	/* Animation */
	:global(.fade-in) {
		opacity: 0;
		transform: translateY(30px);
		animation: fadeIn 0.8s ease forwards;
	}

	@keyframes fadeIn {
		to {
			opacity: 1;
			transform: translateY(0);
		}
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

			pre {
				padding: 1rem;

				code {
					font-size: 0.75rem;
				}
			}
		}

		.hero-stats {
			grid-template-columns: repeat(2, 1fr);
			gap: 0.75rem;
		}

		.stat-card {
			padding: 1rem;

			.stat-number {
				font-size: 1.5rem;
			}

			.stat-label {
				font-size: 0.7rem;
			}
		}

		.language-grid {
			grid-template-columns: 1fr;
			gap: 1rem;
		}

		:global(.card) {
			padding: 1rem;
		}

		:global(.card-stats) {
			grid-template-columns: 1fr;
			gap: 0.5rem;
		}

		.hf-embed-container {
			iframe {
				height: 400px;
			}
		}

		:global(.copy-button) {
			padding: 0.3rem 0.6rem;
			font-size: 0.7rem;
		}
	}
</style>
