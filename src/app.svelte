<script>
  import svelteLogo from './assets/svelte.svg'
  import viteLogo from '/vite.svg'
  import Counter from './lib/Counter.svelte'
  import { onMount } from 'svelte';
  import { Router, link } from 'svelte-spa-router';
  import Home from './pages/home.svelte';
  import About from './pages/about.svelte';
  import Contact from './pages/contact.svelte';

  let loading = true;

  onMount(() => {
    setTimeout(() => {
      loading = false;
    }, 2000); // Loader will show for 2 seconds
  });

  const routes = {
    '/': Home,
    '/about': About,
    '/contact': Contact
  };
</script>

{#if loading}
  <div class="loader">Loading...</div>
{:else}
  <nav>
    <a href="/" use:link>Home</a>
    <a href="/about" use:link>About</a>
    <a href="/contact" use:link>Contact</a>
  </nav>
  <Router {routes} />
{/if}


<style>
  .loader {
    font-size: 2em;
    text-align: center;
    margin-top: 20%;
  }
  nav {
    display: flex;
    gap: 1rem;
    padding: 1rem;
    background-color: #f0f0f0;
  }
  nav a {
    text-decoration: none;
    color: #0366d6;
  }
  nav a:hover {
    text-decoration: underline;
  }
</style>

