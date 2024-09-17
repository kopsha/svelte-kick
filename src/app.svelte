<script>
    import { onMount } from "svelte";
    import { link } from "svelte-spa-router";
    import Router from "svelte-spa-router";
    import { wrap } from "svelte-spa-router/wrap"; // TODO: later aligator
    import Home from "./pages/home.svelte";
    import About from "./pages/about.svelte";
    import Contact from "./pages/contact.svelte";

    let loading = true;

    onMount(() => {
        setTimeout(() => {
            loading = false;
        }, 2000); // Loader will show for 2 seconds
    });

    const routes = {
        "/": Home,
        "/about": About,
        "/contact": Contact,
    };
</script>

<main>
    {#if loading}
        <div class="loader">Loading...</div>
    {:else}
        <nav>
            <a href="/" use:link>Home</a>
            <a href="/about" use:link>About</a>
            <a href="/contact" use:link>Contact</a>
        </nav>
        <Router routes={routes} />
    {/if}
</main>

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
