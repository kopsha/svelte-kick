<script>
    import { onMount } from "svelte";
    import { link } from "svelte-spa-router";
    import Router from "svelte-spa-router";
    import { wrap } from "svelte-spa-router/wrap"; // TODO: later aligator
    import Home from "./pages/home.svelte";
    import About from "./pages/about.svelte";
    import Contact from "./pages/contact.svelte";

    let loading = true;
    let progress = 0;

    onMount(() => {
        const loadingDuration = 987;
        const intervalDuration = 89;

        const increment = (intervalDuration / loadingDuration) * 100;

        const interval = setInterval(() => {
            progress += increment;
            if (progress >= 100) {
                progress = 100;
                clearInterval(interval);
            }
        }, intervalDuration);

        setTimeout(() => {
            loading = false;
        }, loadingDuration);
    });

    const routes = {
        "/": Home,
        "/about": About,
        "/contact": Contact,
    };
</script>

<nav>
    <a href="/" use:link>Home</a>
    <a href="/contact" use:link>Contact</a>
    <a href="/about" use:link>About</a>
</nav>
<main>
    {#if loading}
        <progress value={Math.trunc(progress)} max="100" />
    {:else}
        <Router routes={routes} />
    {/if}
</main>

<style>
    nav {
        display: flex;
        gap: 1rem;
        padding: 1rem;
        background-color: #f0f0f0;
        height: 1.618em;
    }
    nav a {
        text-decoration: none;
        color: #0366d6;
    }
    nav a:hover {
        text-decoration: underline;
    }
    progress {
        -webkit-appearance: none;
        appearance: none;
        width: 100%;
        height: 13px;
        background-color: #f0f0f0;
        border: none;
    }

    progress::-webkit-progress-bar {
        background-color: #f0f0f0;
        border-radius: 5px;
        border: none;
    }

    progress::-webkit-progress-value {
        background-color: cornflowerblue;
        transition: width 0.081s ease-in-out;
        border-radius: 5px;
    }

    progress::-moz-progress-bar {
        background-color: cornflowerblue;
        transition: all 0.081s ease;
        border-radius: 5px;
    }

    main {
        padding: 8px;
        margin: 0 144px;
        /* border: solid 1px red; */
    }
</style>
