
# Svelte Progress Bar Loader Application

A simple Svelte application that includes:

- An application loader with a progress bar that moves from 0% to 100%.
- Three pages: Home, About, and Contact.
- Client-side routing using `svelte-spa-router`.

## Table of Contents

- [Demo](#demo)
- [Features](#features)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Running the Application](#running-the-application)
- [Project Structure](#project-structure)
- [Usage](#usage)
- [License](#license)

## Demo

*(Optional: Include a screenshot or GIF of your application in action.)*

## Features

- **Progress Bar Loader**: Displays a progress bar that fills from 0% to 100% upon application start.
- **Client-Side Routing**: Navigate between Home, About, and Contact pages without reloading the page.
- **Responsive Design**: Simple and clean UI that works across different screen sizes.

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (v12 or newer)
- [npm](https://www.npmjs.com/) (comes with Node.js)

### Installation

Clone the repository:

\`\`\`
git clone https://github.com/yourusername/svelte-progress-bar-loader.git
cd svelte-progress-bar-loader
\`\`\`

Install the dependencies:

\`\`\`
npm install
\`\`\`

### Running the Application

Start the development server:

\`\`\`
npm run dev
\`\`\`

Open your browser and navigate to [http://localhost:5000](http://localhost:5000).

## Project Structure

\`\`\`
svelte-progress-bar-loader/
├── public/
│   ├── global.css          # Global CSS styles
│   └── index.html          # Entry point HTML
├── src/
│   ├── app.svelte          # Main application component
│   └── pages/
│       ├── home.svelte     # Home page component
│       ├── about.svelte    # About page component
│       └── contact.svelte  # Contact page component
├── package.json            # Project metadata and scripts
└── README.md               # Project description (this file)
\`\`\`

## Usage

### Application Loader

Upon starting the application, a progress bar loader will appear, filling from 0% to 100% over a specified duration.

\`\`\`svelte
<!-- app.svelte -->
<script>
    import { onMount } from "svelte";
    // ... other imports ...

    let loading = true;
    let progress = 0;

    onMount(() => {
        const loadingDuration = 1000; // Total loading time in milliseconds
        const intervalDuration = 50;   // Update progress every 50ms

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
</script>

{#if loading}
    <div class="progress-container">
        <div class="progress-bar" style="width: {progress}%;">
            {Math.floor(progress)}%
        </div>
    </div>
{:else}
    <!-- Main content -->
{/if}
\`\`\`

### Navigation

Use the navigation links to switch between pages:

\`\`\`svelte
<nav>
    <a href="/" use:link>Home</a>
    <a href="/contact" use:link>Contact</a>
    <a href="/about" use:link>About</a>
</nav>
\`\`\`

### Routing

Client-side routing is handled by \`svelte-spa-router\`:

\`\`\`svelte
<script>
    import Router from "svelte-spa-router";
    import Home from "./pages/home.svelte";
    import About from "./pages/about.svelte";
    import Contact from "./pages/contact.svelte";

    const routes = {
        "/": Home,
        "/about": About,
        "/contact": Contact,
    };
</script>

<Router {routes} />
\`\`\`

### Styling

The progress bar and other elements are styled using CSS within each component or globally via \`global.css\`.

\`\`\`css
/* Example styles for the progress bar */
.progress-container {
    width: 50%;
    height: 30px;
    background-color: #e0e0e0;
    margin: 20% auto;
    border-radius: 5px;
    overflow: hidden;
    position: relative;
}

.progress-bar {
    height: 100%;
    background-color: #0366d6;
    text-align: center;
    line-height: 30px;
    color: white;
    transition: width 0.05s ease;
}
\`\`\`

## License

This project is licensed under the MIT License.
