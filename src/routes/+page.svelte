<script lang="ts">
	import { onMount } from 'svelte';
	let glowCanvas: HTMLCanvasElement;

	onMount(() => {
		const ctx = glowCanvas.getContext('2d');
		const width = glowCanvas.width = window.innerWidth;
		const height = glowCanvas.height = window.innerHeight;

		function drawGlow() {
			ctx.clearRect(0, 0, width, height);
			const gradient = ctx.createRadialGradient(
				width/2, height/2, 0,
				width/2, height/2, width/2
			);
			gradient.addColorStop(0, 'rgba(0, 255, 255, 0.1)');
			gradient.addColorStop(0.5, 'rgba(0, 255, 255, 0.05)');
			gradient.addColorStop(1, 'rgba(0, 255, 255, 0)');
			
			ctx.fillStyle = gradient;
			ctx.fillRect(0, 0, width, height);
			requestAnimationFrame(drawGlow);
		}

		drawGlow();
	});
</script>

<svelte:head>
	<title>Kepler Systems | Next-Generation AI</title>
	<meta name="description" content="Pioneering the future of artificial intelligence" />
</svelte:head>

<main>
	<canvas bind:this={glowCanvas} class="glow-effect"></canvas>
	<div class="noise-overlay"></div>

	<nav>
		<div class="logo">K</div>
		<div class="nav-links">
			<a href="#about">About</a>
			<a href="#contact" class="contact-btn">Contact</a>
		</div>
	</nav>

	<section class="hero">
		<div class="hero-content">
			<div class="hero-text">
				<h1>kepler<span class="accent">.</span>systems</h1>
				<p class="tagline">Pioneering the next wave of artificial intelligence</p>
			</div>
			<div class="hero-visual">
				<div class="orbital-ring"></div>
				<div class="orbital-ring ring-2"></div>
				<div class="orbital-ring ring-3"></div>
				<div class="core-letter">K</div>
			</div>
		</div>
	</section>

	<section class="focus-areas">
		<div class="container">
			<div class="focus-card">
				<div class="card-content">
					<div class="icon">🧠</div>
					<h3>Language Models</h3>
					<p>Advanced natural language processing systems</p>
				</div>
				<div class="card-border"></div>
			</div>

			<div class="focus-card">
				<div class="card-content">
					<div class="icon">🔊</div>
					<h3>Speech Systems</h3>
					<p>Next-generation voice synthesis technology</p>
				</div>
				<div class="card-border"></div>
			</div>

			<div class="focus-card">
				<div class="card-content">
					<div class="icon">👁️</div>
					<h3>Computer Vision</h3>
					<p>Cutting-edge visual processing solutions</p>
				</div>
				<div class="card-border"></div>
			</div>
		</div>
	</section>

	<footer>
		<div class="container">
			<p>© 2025 Kepler Systems</p>
			<a href="mailto:hello@auna.li" class="contact-link">hello@auna.li</a>
		</div>
	</footer>
</main>

<style lang="scss">
	:root {
		--bg: #000810;
		--primary: #00ffff;
		--primary-dark: #00a3a3;
		--accent: #ff3d71;
		--text: #e0ffff;
		--text-secondary: #7fecec;
	}

	main {
		background: var(--bg);
		min-height: 100vh;
		position: relative;
		overflow: hidden;
	}

	.glow-effect {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		pointer-events: none;
		z-index: 1;
	}

	.noise-overlay {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background: url('data:image/svg+xml,%3Csvg viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg"%3E%3Cfilter id="noiseFilter"%3E%3CfeTurbulence type="fractalNoise" baseFrequency="0.65" numOctaves="3" stitchTiles="stitch"/%3E%3C/filter%3E%3Crect width="100%" height="100%" filter="url(%23noiseFilter)"/%3E%3C/svg%3E');
		opacity: 0.05;
		pointer-events: none;
		z-index: 2;
	}

	.container {
		max-width: 1200px;
		margin: 0 auto;
		padding: 0 2rem;
		position: relative;
		z-index: 3;
	}

	nav {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 2rem;
		position: relative;
		z-index: 3;

		.logo {
			font-size: 2rem;
			font-weight: bold;
			color: var(--primary);
			text-shadow: 0 0 20px rgba(0, 255, 255, 0.5);
		}

		.nav-links {
			display: flex;
			gap: 2rem;
			align-items: center;

			a {
				color: var(--text);
				text-decoration: none;
				transition: color 0.3s ease;

				&:hover {
					color: var(--primary);
				}
			}

			.contact-btn {
				padding: 0.5rem 1.5rem;
				border: 1px solid var(--primary);
				border-radius: 4px;
				transition: all 0.3s ease;

				&:hover {
					background: var(--primary);
					color: var(--bg);
				}
			}
		}
	}

	.hero {
		min-height: 80vh;
		display: flex;
		align-items: center;
		position: relative;
		z-index: 3;
	}

	.hero-content {
		width: 100%;
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 0 2rem;
	}

	.hero-text {
		flex: 1;
		
		h1 {
			font-size: 5rem;
			color: var(--text);
			margin-bottom: 1.5rem;
			line-height: 1;
			font-weight: 700;
			letter-spacing: -0.02em;

			.accent {
				color: var(--accent);
			}
		}

		.tagline {
			font-size: 1.5rem;
			color: var(--text-secondary);
			max-width: 500px;
			line-height: 1.4;
		}
	}

	.hero-visual {
		flex: 1;
		position: relative;
		height: 500px;

		.orbital-ring {
			position: absolute;
			top: 50%;
			left: 50%;
			width: 300px;
			height: 300px;
			border: 1px dashed var(--primary-dark);
			border-radius: 50%;
			animation: rotate 20s linear infinite;

			&.ring-2 {
				width: 400px;
				height: 400px;
				animation-duration: 25s;
				animation-direction: reverse;
			}

			&.ring-3 {
				width: 500px;
				height: 500px;
				animation-duration: 30s;
			}
		}

		.core-letter {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            color: var(--primary);
            font-size: 4rem;
            font-weight: bold;
            text-shadow: 0 0 30px var(--primary);
        }
	}

	.focus-areas {
		padding: 6rem 0;
		position: relative;
		z-index: 3;

		.container {
			display: grid;
			grid-template-columns: repeat(3, 1fr);
			gap: 2rem;

			@media (max-width: 968px) {
				grid-template-columns: 1fr;
			}
		}
	}

	.focus-card {
		position: relative;
		padding: 2rem;
		background: rgba(0, 255, 255, 0.03);
		border-radius: 8px;
		overflow: hidden;
		transition: all 0.3s ease;

		&:hover {
			transform: translateY(-5px);

			.card-border {
				opacity: 1;
			}
		}

		.card-content {
			position: relative;
			z-index: 2;
		}

		.icon {
			font-size: 2.5rem;
			margin-bottom: 1.5rem;
		}

		h3 {
			color: var(--primary);
			font-size: 1.5rem;
			margin-bottom: 1rem;
		}

		p {
			color: var(--text-secondary);
			line-height: 1.6;
		}

		.card-border {
			position: absolute;
			top: 0;
			left: 0;
			right: 0;
			bottom: 0;
			border: 1px solid var(--primary);
			border-radius: 8px;
			opacity: 0;
			transition: opacity 0.3s ease;
		}
	}

	footer {
		padding: 2rem 0;
		border-top: 1px dashed var(--primary-dark);
		position: relative;
		z-index: 3;

		.container {
			display: flex;
			justify-content: space-between;
			align-items: center;
		}

		p {
			color: var(--text-secondary);
		}

		.contact-link {
			color: var(--primary);
			text-decoration: none;
			transition: color 0.3s ease;

			&:hover {
				color: var(--accent);
			}
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

	@media (max-width: 968px) {
		.hero-content {
			flex-direction: column;
			text-align: center;
			gap: 4rem;
		}

		.hero-text {
			h1 {
				font-size: 3.5rem;
			}

			.tagline {
				margin: 0 auto;
			}
		}

		.hero-visual {
			height: 400px;
		}
	}

	@media (max-width: 640px) {
		nav {
			.nav-links {
				gap: 1rem;
			}
		}

		.hero-text {
			h1 {
				font-size: 2.5rem;
			}

			.tagline {
				font-size: 1.2rem;
			}
		}
	}
</style>