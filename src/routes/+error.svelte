<script>
  import Nav from '$lib/components/Nav.svelte';
</script>

<svelte:head>
  <title>404 - Page Not Found | Kepler Systems</title>
  <meta name="description" content="The page you're looking for doesn't exist." />
  <script
    defer
    src="https://analytics.auna.li/script.js  "
    data-website-id="c2811ea4-cc1f-4b5b-ad40-8cd7b4ed02a3"
  ></script>
</svelte:head>

<main>
  <div class="background-grid"></div>

  <Nav />

  <section class="wrapper">
    <div class="error-container">
      <div class="error-code">404</div>
      <h1>Page Not Found</h1>
      <p>The page you're looking for doesn't exist or has been moved.</p>
      <a href="/" class="home-link">← Back to Home</a>
    </div>
  </section>
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

  .wrapper {
    min-height: calc(100vh - 80px);
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 2rem;
    position: relative;
    z-index: 2;
  }

  .error-container {
    text-align: center;
    max-width: 600px;
  }

  .error-code {
    font-size: 8rem;
    color: var(--accent);
    font-weight: bold;
    margin-bottom: 1rem;
    text-shadow: 0 0 30px rgba(255, 0, 238, 0.3);
    animation: pulse 2s ease-in-out infinite alternate;
  }

  @keyframes pulse {
    from {
      opacity: 0.7;
    }
    to {
      opacity: 1;
    }
  }

  h1 {
    font-size: 3rem;
    color: var(--primary);
    margin-bottom: 1.5rem;
    text-shadow: 0 0 20px rgba(0, 255, 213, 0.2);
  }

  p {
    color: var(--text-secondary);
    font-size: 1.2rem;
    line-height: 1.6;
    margin-bottom: 2.5rem;
  }

  .home-link {
    display: inline-block;
    color: var(--accent);
    text-decoration: none;
    font-size: 1.1rem;
    padding: 1rem 2rem;
    border: 1px solid var(--accent);
    border-radius: 8px;
    transition: all 0.3s ease;
    background: rgba(255, 0, 238, 0.05);

    &:hover {
      background: rgba(255, 0, 238, 0.1);
      transform: translateY(-2px);
      box-shadow: 0 5px 15px rgba(255, 0, 238, 0.2);
    }
  }

  @media (max-width: 768px) {
    .error-code {
      font-size: 6rem;
    }

    h1 {
      font-size: 2.5rem;
    }

    p {
      font-size: 1.1rem;
    }

    .home-link {
      font-size: 1rem;
      padding: 0.8rem 1.5rem;
    }
  }
</style>
