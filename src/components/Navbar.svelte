<script lang="ts">
    import { onMount } from "svelte";

    let isNavOpen = false;
    let scrolled = false;
    let darkMode = false;

    onMount(() => {
        darkMode = document.documentElement.classList.contains("dark");

        const handleScroll = () => {
            scrolled = window.scrollY > 20;
        };
        window.addEventListener("scroll", handleScroll);
        return () => window.removeEventListener("scroll", handleScroll);
    });

    function toggleNavbar() {
        isNavOpen = !isNavOpen;
    }

    function closeNav() {
        isNavOpen = false;
    }

    function toggleDarkMode() {
        darkMode = !darkMode;
        if (darkMode) {
            document.documentElement.classList.add("dark");
            localStorage.setItem("theme", "dark");
        } else {
            document.documentElement.classList.remove("dark");
            localStorage.setItem("theme", "light");
        }
    }

    const links = [
        { href: "#hero", label: "Home" },
        { href: "#about", label: "About" },
        { href: "#projects", label: "Projects" },
        { href: "#contact", label: "Contact" },
    ];
</script>

<nav
    class="fixed top-0 w-full z-50 transition-all duration-500
        {scrolled
            ? 'bg-white/80 dark:bg-slate-900/80 backdrop-blur-xl shadow-sm border-b border-slate-200/50 dark:border-slate-700/50'
            : 'bg-transparent'}"
>
    <div class="max-w-5xl mx-auto px-6 py-4 flex items-center justify-between">
        <a
            href="#hero"
            class="text-lg font-bold tracking-tight gradient-text"
        >
            Amanuel
        </a>

        <!-- Desktop nav -->
        <div class="hidden md:flex items-center gap-8">
            {#each links as { href, label }}
                <a
                    {href}
                    class="nav-link text-sm font-medium text-slate-600 dark:text-slate-300 hover:text-rose-600 dark:hover:text-rose-400 transition-colors"
                >
                    {label}
                </a>
            {/each}

            <button
                on:click={toggleDarkMode}
                class="p-2 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-800 hover:text-rose-600 dark:hover:text-rose-400 transition-all duration-300"
                aria-label="Toggle dark mode"
            >
                {#if darkMode}
                    <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
                    </svg>
                {:else}
                    <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
                    </svg>
                {/if}
            </button>
        </div>

        <!-- Mobile hamburger -->
        <div class="flex items-center gap-2 md:hidden">
            <button
                on:click={toggleDarkMode}
                class="p-2 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-800 transition-colors"
                aria-label="Toggle dark mode"
            >
                {#if darkMode}
                    <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
                    </svg>
                {:else}
                    <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
                    </svg>
                {/if}
            </button>

            <button
                on:click={toggleNavbar}
                class="p-2 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-800 transition-colors"
                aria-label="Toggle menu"
            >
                {#if isNavOpen}
                    <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                    </svg>
                {:else}
                    <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M4 6h16M4 12h16M4 18h16" />
                    </svg>
                {/if}
            </button>
        </div>
    </div>

    <!-- Mobile menu -->
    {#if isNavOpen}
        <div class="md:hidden bg-white/95 dark:bg-slate-900/95 backdrop-blur-xl border-t border-slate-200/50 dark:border-slate-700/50">
            <div class="px-6 py-4 flex flex-col gap-1">
                {#each links as { href, label }}
                    <a
                        {href}
                        on:click={closeNav}
                        class="text-sm font-medium text-slate-600 dark:text-slate-300 hover:text-rose-600 dark:hover:text-rose-400 hover:bg-slate-50 dark:hover:bg-slate-800/50 rounded-lg transition-all py-2.5 px-3"
                    >
                        {label}
                    </a>
                {/each}
            </div>
        </div>
    {/if}
</nav>
