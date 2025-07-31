<script>
	import { onMount } from 'svelte';

	// Dataset from analysis results
	const datasetResults = [
		{
			file_name: 'paari_pa_tts.parquet',
			num_rows: 11105,
			columns: ['title', 'text', 'language', 'language_name'],
			text_columns: [
				{ column: 'title', characters: 598440, tokens: 299220 },
				{ column: 'text', characters: 8593038, tokens: 4296519 },
				{ column: 'language', characters: 44420, tokens: 22210 },
				{ column: 'language_name', characters: 66630, tokens: 33315 }
			],
			total_characters: 9302528,
			total_tokens: 4651264,
			estimated_audio_seconds: 145352.0,
			estimated_audio_minutes: 2422.53,
			estimated_audio_hours: 40.38,
			input_cost_usd: 4.65,
			output_cost_usd: 93.03,
			total_cost_usd: 97.68,
			file_size_mb: 7.6
		}
		// ... (other datasets will be added)
	];

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

	// Language stats from analysis (TTS datasets only)
	const ttsLanguageStats = {
		PA: { tokens: 4651264, hours: 40.38, cost: 97.68, rows: 11105 },
		GU: { tokens: 3178773, hours: 27.59, cost: 66.75, rows: 10891 },
		UR: { tokens: 2603934, hours: 22.6, cost: 54.68, rows: 10654 },
		TA: { tokens: 2438925, hours: 21.17, cost: 51.22, rows: 10323 },
		TE: { tokens: 2403379, hours: 20.86, cost: 50.47, rows: 8386 },
		HI: { tokens: 2315342, hours: 20.1, cost: 48.62, rows: 10687 },
		MR: { tokens: 2275165, hours: 19.75, cost: 47.78, rows: 9961 },
		EN: { tokens: 1899623, hours: 16.49, cost: 39.89, rows: 10395 }
	};

	// Language stats for LLM training datasets (no TTS costs)
	const llmLanguageStats = {
		PA: { tokens: 4277490, articles: 978, size: 7.4 },
		GU: { tokens: 2918993, articles: 976, size: 7.3 },
		UR: { tokens: 2365924, articles: 963, size: 6.0 },
		TA: { tokens: 2232056, articles: 975, size: 6.7 },
		TE: { tokens: 2211858, articles: 743, size: 5.9 },
		HI: { tokens: 2102270, articles: 976, size: 6.9 },
		MR: { tokens: 2097149, articles: 974, size: 6.9 },
		EN: { tokens: 1741555, articles: 965, size: 4.4 }
	};

	// Combined for charts (use TTS stats for consistency)
	const languageStats = ttsLanguageStats;

	onMount(async () => {
		// Import Chart.js dynamically
		const Chart = (await import('chart.js/auto')).default;

		// Initialize charts
		function initCharts() {
			// Cost chart
			const costCtx = document.getElementById('costChart').getContext('2d');
			new Chart(costCtx, {
				type: 'bar',
				data: {
					labels: Object.keys(languageStats),
					datasets: [
						{
							label: 'TTS Cost (USD)',
							data: Object.values(languageStats).map((lang) => lang.cost),
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

			// Token distribution pie chart
			const tokenCtx = document.getElementById('tokenChart').getContext('2d');
			new Chart(tokenCtx, {
				type: 'doughnut',
				data: {
					labels: Object.keys(languageStats),
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

		// Populate TTS language cards
		function populateTTSLanguageCards() {
			const ttsGrid = document.getElementById('ttsLanguageGrid');

			Object.entries(ttsLanguageStats).forEach(([lang, stats]) => {
				const card = document.createElement('div');
				card.className = 'card fade-in';
				card.innerHTML = `
                    <div class="card-header">
                        <div class="card-icon">🎙️</div>
                        <div>
                            <div class="card-title">${languageNames[lang.toLowerCase()]}</div>
                            <div class="card-subtitle">${lang} TTS Dataset</div>
                        </div>
                    </div>
                    <div class="card-stats">
                        <div class="card-stat">
                            <span class="card-stat-number">${(stats.tokens / 1000000).toFixed(1)}M</span>
                            <span class="card-stat-label">Tokens</span>
                        </div>
                        <div class="card-stat">
                            <span class="card-stat-number">${stats.hours}</span>
                            <span class="card-stat-label">Audio Hours</span>
                        </div>
                        <div class="card-stat">
                            <span class="card-stat-number">$${stats.cost}</span>
                            <span class="card-stat-label">TTS Cost</span>
                        </div>
                        <div class="card-stat">
                            <span class="card-stat-number">${stats.rows.toLocaleString()}</span>
                            <span class="card-stat-label">Rows</span>
                        </div>
                    </div>
                    <div class="tags">
                        <span class="tag">Audio Generation</span>
                        <span class="tag">TTS Ready</span>
                        <span class="tag">${languageNames[lang.toLowerCase()]}</span>
                    </div>
                `;
				ttsGrid.appendChild(card);
			});
		}

		// Populate LLM language cards
		function populateLLMLanguageCards() {
			const llmGrid = document.getElementById('llmLanguageGrid');

			Object.entries(llmLanguageStats).forEach(([lang, stats]) => {
				const card = document.createElement('div');
				card.className = 'card fade-in';
				card.innerHTML = `
                    <div class="card-header">
                        <div class="card-icon">📚</div>
                        <div>
                            <div class="card-title">${languageNames[lang.toLowerCase()]}</div>
                            <div class="card-subtitle">${lang} LLM Training Dataset</div>
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
                            <span class="card-stat-label">File Size</span>
                        </div>
                        <div class="card-stat">
                            <span class="card-stat-number">No Cost</span>
                            <span class="card-stat-label">Training Only</span>
                        </div>
                    </div>
                    <div class="tags">
                        <span class="tag">LLM Training</span>
                        <span class="tag">Text Only</span>
                        <span class="tag">${languageNames[lang.toLowerCase()]}</span>
                    </div>
                `;
				llmGrid.appendChild(card);
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

		// Smooth scrolling for navigation
		document.querySelectorAll('nav a').forEach((anchor) => {
			anchor.addEventListener('click', function (e) {
				e.preventDefault();
				const target = document.querySelector(this.getAttribute('href'));
				target.scrollIntoView({
					behavior: 'smooth',
					block: 'start'
				});
			});
		});

		// Initialize everything
		initCharts();
		populateTTSLanguageCards();
		populateLLMLanguageCards();
		initAnimations();
	});
</script>

<svelte:head>
	<title>PAARI Dataset Analysis - TTS Cost & Token Analysis</title>
	<link
		href="https://fonts.googleapis.com/css2?family=Chakra+Petch:ital,wght@0,300;0,400;0,500;0,600;0,700;1,300;1,400;1,500;1,600;1,700&family=Space+Mono:ital,wght@0,400;0,700;1,400;1,700&display=swap"
		rel="stylesheet"
	/>
	<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
	<script
		defer
		src="https://analytics.auna.li/script.js"
		data-website-id="c2811ea4-cc1f-4b5b-ad40-8cd7b4ed02a3"
	></script>
</svelte:head>

<!-- Background circles -->
<div class="bg-circles">
	<div class="circle circle1"></div>
	<div class="circle circle2"></div>
	<div class="circle circle3"></div>
</div>

<!-- Header -->
<header>
	<div class="logo">PAARI Analysis</div>
	<nav>
		<a href="#overview">Overview</a>
		<a href="#languages">Languages</a>
		<a href="#insights">Insights</a>
	</nav>
</header>

<div class="container">
	<!-- Hero Section -->
	<section class="hero" id="overview">
		<h1>PAARI Dataset Analysis</h1>
		<p>Comprehensive TTS Cost & Token Analysis across 8 Languages</p>

		<div class="hero-stats">
			<div class="stat-card fade-in">
				<span class="stat-number">$462</span>
				<span class="stat-label">TTS Cost (TTS datasets only)</span>
			</div>
			<div class="stat-card fade-in">
				<span class="stat-number">191</span>
				<span class="stat-label">TTS Audio Hours</span>
			</div>
			<div class="stat-card fade-in">
				<span class="stat-number">41.7M</span>
				<span class="stat-label">Total Tokens (All datasets)</span>
			</div>
			<div class="stat-card fade-in">
				<span class="stat-number">16</span>
				<span class="stat-label">Total Datasets</span>
			</div>
		</div>
	</section>

	<!-- TTS vs LLM Training Comparison -->
	<section class="section">
		<h2 class="section-title">TTS vs LLM Training Datasets</h2>
		<div class="comparison-grid">
			<div class="comparison-card">
				<h3 class="comparison-title">🎙️ TTS Datasets</h3>
				<div class="card-stats">
					<div class="card-stat">
						<span class="card-stat-number">8</span>
						<span class="card-stat-label">Files</span>
					</div>
					<div class="card-stat">
						<span class="card-stat-number">22.0M</span>
						<span class="card-stat-label">Tokens</span>
					</div>
					<div class="card-stat">
						<span class="card-stat-number">191</span>
						<span class="card-stat-label">Hours</span>
					</div>
					<div class="card-stat">
						<span class="card-stat-number">$462</span>
						<span class="card-stat-label">Cost</span>
					</div>
				</div>
				<p class="card-subtitle">
					Pre-processed datasets optimized for TTS with additional metadata columns
				</p>
			</div>

			<div class="comparison-card">
				<h3 class="comparison-title">📄 LLM Training Datasets</h3>
				<div class="card-stats">
					<div class="card-stat">
						<span class="card-stat-number">8</span>
						<span class="card-stat-label">Files</span>
					</div>
					<div class="card-stat">
						<span class="card-stat-number">19.7M</span>
						<span class="card-stat-label">Tokens</span>
					</div>
					<div class="card-stat">
						<span class="card-stat-number">7,650</span>
						<span class="card-stat-label">Articles</span>
					</div>
					<div class="card-stat">
						<span class="card-stat-number">N/A</span>
						<span class="card-stat-label">TTS Cost</span>
					</div>
				</div>
				<p class="card-subtitle">Clean text datasets for LLM training - title and content only</p>
			</div>
		</div>
	</section>

	<!-- Charts Section -->
	<section class="section">
		<div class="chart-container">
			<h3 class="chart-title">Cost Distribution by Language</h3>
			<div class="chart-wrapper">
				<canvas id="costChart"></canvas>
			</div>
		</div>

		<div class="chart-container">
			<h3 class="chart-title">Token Distribution</h3>
			<div class="chart-wrapper">
				<canvas id="tokenChart"></canvas>
			</div>
		</div>
	</section>

	<!-- Language Breakdown -->
	<section class="section" id="languages">
		<h2 class="section-title">Language Analysis</h2>
		<p class="section-subtitle">Comprehensive breakdown by dataset type and language</p>

		<h3 style="color: #00ffd5; text-align: center; margin: 3rem 0 2rem 0;">
			🎙️ TTS Datasets (Audio Generation)
		</h3>
		<div class="language-grid" id="ttsLanguageGrid">
			<!-- TTS Language cards will be populated by JavaScript -->
		</div>

		<h3 style="color: #40e0d0; text-align: center; margin: 4rem 0 2rem 0;">
			📚 LLM Training Datasets (Text Only)
		</h3>
		<div class="language-grid" id="llmLanguageGrid">
			<!-- LLM Language cards will be populated by JavaScript -->
		</div>
	</section>

	<!-- Key Insights -->
	<section class="insights" id="insights">
		<h3>🔍 Key Insights</h3>
		<div class="insights-grid">
			<div class="insight-item">
				<h4>Most Expensive TTS Dataset</h4>
				<p>Punjabi (PA) - $97.68 for 40.38 hours of audio</p>
			</div>
			<div class="insight-item">
				<h4>Best TTS Value</h4>
				<p>English (EN) - $39.89 for 16.49 hours, most economical</p>
			</div>
			<div class="insight-item">
				<h4>Total TTS Budget</h4>
				<p>$462.12 for 191 hours of synthetic audio generation</p>
			</div>
			<div class="insight-item">
				<h4>Dataset Purpose</h4>
				<p>TTS datasets = Audio generation. LLM datasets = Text training only</p>
			</div>
		</div>
	</section>
</div>

<!-- Footer -->
<footer>
	<div class="container">
		<div class="footer-content">
			<div class="footer-section">
				<h4>PAARI Dataset</h4>
				<p>Comprehensive multilingual dataset analysis for TTS cost estimation and planning.</p>
			</div>
			<div class="footer-section">
				<h4>Analysis Details</h4>
				<p>Token counts via Gemini API, cost calculations based on Gemini Pro TTS pricing.</p>
			</div>
			<div class="footer-section">
				<h4>Generated</h4>
				<p>Analysis generated with precise token counting and cost estimation algorithms.</p>
			</div>
		</div>
		<p style="color: #666; margin-top: 2rem;">
			&copy; 2025 PAARI Dataset Analysis. Built with ❤️ for AI research.
		</p>
	</div>
</footer>

<style>
	:global(:root) {
		--white: #aca1cb;
		--white-two: #7f7796;
		--purple: #835fe8;
		--purple-two: #494d86;
		--purple-low-opacity: rgba(187, 163, 255, 0.36);
		--purple-low-opacity-two: rgba(187, 163, 255, 0.2);
		--purple-border: rgba(140, 98, 255, 0.2);
		--purple-border-two: rgba(140, 98, 255, 0.3);
		--bg-color: #030713;
		--neutral-one: #28214b6e;
		--neutral-two: #101024;
		--neutral-three: #040711;
		--font-one: 'Chakra Petch', sans-serif;
		--font-two: 'Space Mono', monospace;
		--primary: #00ffd5;
		--primary-dark: #00b4a3;
		--primary-light: #7fffef;
		--accent: #ff00ee;
		--accent-dark: #b400a7;
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
		font-family: var(--font-one);
		background: var(--bg-color);
		color: var(--white);
		line-height: 1.4;
		overflow-x: hidden;
		margin: 0;
		padding: 0;
	}

	:global(::selection) {
		background: var(--purple-low-opacity-two);
	}

	/* Background grid pattern */
	.background-grid {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background-image: linear-gradient(var(--purple-border) 1px, transparent 1px),
			linear-gradient(90deg, var(--purple-border) 1px, transparent 1px);
		background-size: 30px 30px;
		z-index: -1;
		pointer-events: none;
	}

	/* Orbital system */
	.orbital-system {
		position: fixed;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		z-index: -1;
	}

	.orbit {
		position: absolute;
		border: 1px dashed var(--purple-border-two);
		border-radius: 50%;
		animation: rotate 20s linear infinite;
	}

	.orbit-1 {
		width: 300px;
		height: 300px;
	}

	.orbit-2 {
		width: 500px;
		height: 500px;
		animation-direction: reverse;
	}

	.orbit-3 {
		width: 700px;
		height: 700px;
	}

	@keyframes rotate {
		from {
			transform: translate(-50%, -50%) rotate(0deg);
		}

		to {
			transform: translate(-50%, -50%) rotate(360deg);
		}
	}

	/* Header */
	header {
		padding: 2rem;
		position: relative;
		z-index: 2;
		display: flex;
		justify-content: space-between;
		align-items: center;
		max-width: 1400px;
		margin: 0 auto;
	}

	.logo {
		font-size: 2rem;
		color: var(--primary);
		font-weight: bold;
		text-shadow: 0 0 20px rgba(0, 255, 213, 0.5);
	}

	nav {
		display: flex;
		gap: 2rem;
	}

	nav a {
		color: var(--white);
		text-decoration: none;
		transition: color 0.3s ease;
		font-weight: 500;
	}

	nav a:hover {
		color: var(--primary);
	}

	/* Main content */
	.container {
		max-width: 1400px;
		margin: 0 auto;
		padding: 0 2rem;
		position: relative;
		z-index: 2;
	}

	.wrapper {
		margin-inline: auto;
		width: min(90%, 60rem);
	}

	/* Hero section */
	.hero {
		text-align: center;
		padding: 8rem 0;
		margin-bottom: 4rem;
		position: relative;
	}

	.hero h1 {
		color: var(--purple);
		font-weight: 600;
		letter-spacing: -0.055em;
		line-height: 101.6%;
		font-size: 4rem;
		margin-bottom: 2rem;
		text-shadow: 0px 0px 71px var(--purple-low-opacity);
	}

	.hero p {
		font-family: var(--font-two);
		letter-spacing: -0.04em;
		line-height: 1.5rem;
		color: var(--white-two);
		font-weight: 300;
		font-size: 1.2rem;
		margin-bottom: 3rem;
		max-width: 800px;
		margin-left: auto;
		margin-right: auto;
	}

	.hero-stats {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
		gap: 2rem;
		margin-top: 3rem;
	}

	.stat-card {
		background: rgba(0, 255, 213, 0.1);
		border: 1px solid rgba(0, 255, 213, 0.3);
		border-radius: 15px;
		padding: 2rem;
		text-align: center;
		backdrop-filter: blur(5px);
		transition: all 0.3s ease;
	}

	.stat-card:hover {
		transform: translateY(-5px);
		background: rgba(0, 255, 213, 0.15);
		box-shadow: 0 10px 30px rgba(0, 255, 213, 0.2);
	}

	.stat-number {
		font-size: 3rem;
		font-weight: bold;
		color: #00ffd5;
		display: block;
	}

	.stat-label {
		color: #cccccc;
		text-transform: uppercase;
		letter-spacing: 0.1rem;
		font-size: 0.9rem;
	}

	/* Section styling */
	.section {
		margin-bottom: 5rem;
	}

	.section-title {
		color: var(--white);
		font-weight: 500;
		font-size: 2.25rem;
		line-height: 2.5rem;
		text-align: center;
		margin-bottom: 3rem;
	}

	.section-subtitle {
		text-align: center;
		color: var(--white-two);
		font-family: var(--font-two);
		letter-spacing: -0.04em;
		margin-bottom: 2rem;
		font-size: 1.1rem;
		font-weight: 300;
	}

	/* Card grids */
	.card-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
		gap: 2rem;
		margin: 3rem 0;
	}

	.language-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
		gap: 2rem;
		margin: 3rem 0;
	}

	.dataset-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
		gap: 2rem;
		margin: 3rem 0;
	}

	/* Card styling */
	:global(.card) {
		background: var(--neutral-one);
		border: 1px solid var(--purple-border);
		border-radius: 15px;
		padding: 2rem;
		backdrop-filter: blur(10px);
		transition: all 0.3s ease;
		position: relative;
		overflow: hidden;
	}

	:global(.card::before) {
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		height: 3px;
		background: linear-gradient(90deg, var(--purple), var(--purple-two));
		transform: scaleX(0);
		transition: transform 0.3s ease;
	}

	:global(.card:hover::before) {
		transform: scaleX(1);
	}

	:global(.card:hover) {
		transform: translateY(-8px);
		background: rgba(0, 255, 213, 0.08);
		box-shadow: 0 15px 40px rgba(0, 255, 213, 0.15);
	}

	:global(.card-header) {
		display: flex;
		align-items: center;
		margin-bottom: 1.5rem;
	}

	:global(.card-icon) {
		font-size: 2rem;
		margin-right: 1rem;
	}

	:global(.card-title) {
		font-size: 1.5rem;
		font-weight: 600;
		color: #00ffd5;
	}

	:global(.card-subtitle) {
		color: #cccccc;
		font-size: 0.9rem;
		margin-top: 0.5rem;
	}

	.card-stats {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
		gap: 1rem;
		margin: 1.5rem 0;
	}

	.card-stat {
		text-align: center;
	}

	.card-stat-number {
		font-size: 1.5rem;
		font-weight: bold;
		color: #00ffd5;
		display: block;
	}

	.card-stat-label {
		color: #cccccc;
		font-size: 0.8rem;
		text-transform: uppercase;
		letter-spacing: 0.05rem;
	}

	/* Tags */
	:global(.tags) {
		display: flex;
		flex-wrap: wrap;
		gap: 0.5rem;
		margin: 1rem 0;
	}

	:global(.tag) {
		background: rgba(64, 224, 208, 0.2);
		color: #40e0d0;
		padding: 0.3rem 0.8rem;
		border-radius: 20px;
		font-size: 0.8rem;
		border: 1px solid rgba(64, 224, 208, 0.3);
	}

	/* Chart containers */
	.chart-container {
		background: rgba(255, 255, 255, 0.05);
		border: 1px solid rgba(64, 224, 208, 0.3);
		border-radius: 15px;
		padding: 2rem;
		margin: 2rem 0;
		backdrop-filter: blur(10px);
	}

	.chart-title {
		text-align: center;
		color: #40e0d0;
		margin-bottom: 2rem;
		font-size: 1.5rem;
	}

	.chart-wrapper {
		position: relative;
		height: 400px;
		margin: 1rem 0;
	}

	/* Comparison section */
	.comparison-grid {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 3rem;
		margin: 3rem 0;
	}

	.comparison-card {
		background: rgba(255, 255, 255, 0.05);
		border: 1px solid rgba(64, 224, 208, 0.3);
		border-radius: 15px;
		padding: 2rem;
		backdrop-filter: blur(10px);
	}

	.comparison-title {
		font-size: 1.8rem;
		color: #40e0d0;
		text-align: center;
		margin-bottom: 2rem;
	}

	/* Insights section */
	.insights {
		background: linear-gradient(135deg, rgba(64, 224, 208, 0.1), rgba(0, 206, 209, 0.1));
		border: 1px solid rgba(64, 224, 208, 0.3);
		border-radius: 20px;
		padding: 3rem;
		margin: 4rem 0;
		text-align: center;
	}

	.insights h3 {
		font-size: 2rem;
		color: #40e0d0;
		margin-bottom: 2rem;
	}

	.insights-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
		gap: 2rem;
		margin-top: 2rem;
	}

	.insight-item {
		padding: 1.5rem;
		background: rgba(255, 255, 255, 0.05);
		border-radius: 10px;
		border: 1px solid rgba(64, 224, 208, 0.2);
	}

	.insight-item h4 {
		color: #40e0d0;
		margin-bottom: 1rem;
	}

	/* Footer */
	footer {
		background: rgba(0, 0, 0, 0.3);
		padding: 3rem 0;
		margin-top: 5rem;
		text-align: center;
		border-top: 1px solid rgba(64, 224, 208, 0.3);
	}

	.footer-content {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
		gap: 2rem;
		margin-bottom: 2rem;
	}

	.footer-section h4 {
		color: #40e0d0;
		margin-bottom: 1rem;
	}

	.footer-section p {
		color: #cccccc;
		font-size: 0.9rem;
	}

	/* Responsive design */
	@media (max-width: 768px) {
		.hero h1 {
			font-size: 2.5rem;
		}

		.container {
			padding: 0 1rem;
		}

		.comparison-grid {
			grid-template-columns: 1fr;
			gap: 2rem;
		}

		.card-grid,
		.language-grid,
		.dataset-grid {
			grid-template-columns: 1fr;
		}
	}

	/* Animation classes */
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

	/* Loading animation */
	.loading {
		display: inline-block;
		width: 20px;
		height: 20px;
		border: 3px solid rgba(64, 224, 208, 0.3);
		border-radius: 50%;
		border-top-color: #40e0d0;
		animation: spin 1s ease-in-out infinite;
	}

	@keyframes spin {
		to {
			transform: rotate(360deg);
		}
	}
</style>
