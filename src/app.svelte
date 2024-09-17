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
        const intervalDuration = 144;

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

{#if loading}
    <div class="progress-container">
        <div class="progress-bar" style="width: {progress}%;">
            {Math.floor(progress)}%
        </div>
    </div>
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
    .progress-container {
        width: 61.8%;
        height: 34px;
        background-color: #e0e0e0;
        margin: 21% auto;
        border-radius: 5px;
        overflow: hidden;
        position: relative;
    }

    .progress-bar {
        height: 100%;
        background-color: #0366d6;
        text-align: center;
        vertical-align: middle;
        line-height: 34px;
        font-size: 8pt;
        color: white;
        transition: width 0.144s ease;
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
