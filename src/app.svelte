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
        }, 1000);
    });

    const routes = {
        "/": Home,
        "/about": About,
        "/contact": Contact,
    };
</script>

{#if loading}
    <div class="loader">Loading...</div>
{:else}
    <nav>
        <a href="/" use:link>Home</a>
        <a href="/contact" use:link>Contact</a>
        <a href="/about" use:link>About</a>
    </nav>
    <main>
        <Router routes={routes} />
    </main>
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
    main {
        padding: 8px;
        margin: 0 144px;
        /* border: solid 1px red; */
    }
</style>
