<script lang="ts">
</script>

<nav class="wrapper nav-container">
	<div class="logo">K</div>
	<div class="nav-links">
		<a href="/">Home</a>
		<a href="/blog">Blog</a>
	</div>
</nav>

<style lang="scss">
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
		--font-one: "Chakra Petch", sans-serif;
		--font-two: "Space Mono", monospace;
	}

	.wrapper {
		margin-inline: auto;
		width: min(90%, 60rem);
		position: relative;
		z-index: 2;
	}

	.nav-container {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 2rem 0;
		position: relative;
		z-index: 2;
	}

	.logo {
		font-size: 2rem;
		color: var(--primary);
		font-weight: bold;
		text-shadow: 0px 0px 71px rgba(131, 95, 232, 0.3);
	}

	.nav-links {
		display: flex;
		gap: 2rem;
		align-items: center;

		a {
			color: var(--text);
			text-decoration: none;
			font-family: var(--font-two);
			transition: color 0.3s ease;

			&:hover {
				color: var(--primary);
			}
		}
	}

	@media (max-width: 768px) {
		.nav-container {
			flex-direction: column;
			gap: 1rem;
			padding: 1rem 0;
		}

		.logo {
			font-size: 1.5rem;
		}

		.nav-links {
			gap: 1rem;
			font-size: 0.9rem;
		}
	}
</style>