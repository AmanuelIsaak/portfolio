<script lang="ts">
    import { onMount } from "svelte";
    import { slide } from "svelte/transition";

    let isNavOpen = false;
    let scrolled = false;
    let darkMode = false;
    let progress = 0;
    let activeSection = "hero";

    const links = [
        { href: "#hero", id: "hero", label: "Home" },
        { href: "#about", id: "about", label: "About" },
        { href: "#stack", id: "stack", label: "Stack" },
        { href: "#projects", id: "projects", label: "Projects" },
        { href: "#contact", id: "contact", label: "Contact" },
    ];

    onMount(() => {
        darkMode = document.documentElement.classList.contains("dark");

        const handleScroll = () => {
            scrolled = window.scrollY > 20;
            const max =
                document.documentElement.scrollHeight - window.innerHeight;
            progress = max > 0 ? Math.min(1, window.scrollY / max) : 0;
        };
        handleScroll();
        window.addEventListener("scroll", handleScroll, { passive: true });

        // Scroll-spy: highlight the nav item for the section in view.
        const sections = links
            .map((l) => document.getElementById(l.id))
            .filter((el): el is HTMLElement => !!el);
        const observer = new IntersectionObserver(
            (entries) => {
                for (const entry of entries) {
                    if (entry.isIntersecting) activeSection = entry.target.id;
                }
            },
            { rootMargin: "-45% 0px -50% 0px" },
        );
        sections.forEach((s) => observer.observe(s));

        const onKey = (e: KeyboardEvent) => {
            if (e.key === "Escape") isNavOpen = false;
        };
        window.addEventListener("keydown", onKey);

        return () => {
            window.removeEventListener("scroll", handleScroll);
            window.removeEventListener("keydown", onKey);
            observer.disconnect();
        };
    });

    function toggleDarkMode() {
        darkMode = !darkMode;
        document.documentElement.classList.toggle("dark", darkMode);
        localStorage.setItem("theme", darkMode ? "dark" : "light");
    }
</script>

<nav
    class="fixed top-0 w-full z-50 transition-all duration-500
        {scrolled
        ? 'bg-white/80 dark:bg-slate-900/80 backdrop-blur-xl shadow-sm border-b border-slate-200/50 dark:border-slate-700/50'
        : 'bg-transparent'}"
>
    <!-- Scroll progress bar -->
    <div
        class="absolute bottom-0 left-0 h-0.5 bg-gradient-to-r from-rose-500 via-orange-500 to-amber-500 transition-[width] duration-150 ease-out"
        style="width: {progress * 100}%"
    ></div>

    <div
        class="max-w-5xl mx-auto px-6 py-4 flex items-center justify-between"
    >
        <a href="#hero" class="text-lg font-bold tracking-tight gradient-text">
            Amanuel
        </a>

        <!-- Desktop nav -->
        <div class="hidden md:flex items-center gap-8">
            {#each links as { href, id, label }}
                <a
                    {href}
                    class="nav-link text-sm font-medium transition-colors
                        {activeSection === id
                        ? 'text-rose-600 dark:text-rose-400'
                        : 'text-slate-600 dark:text-slate-300 hover:text-rose-600 dark:hover:text-rose-400'}"
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
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="w-5 h-5"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                        stroke-width="2"
                    >
                        <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z"
                        />
                    </svg>
                {:else}
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="w-5 h-5"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                        stroke-width="2"
                    >
                        <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z"
                        />
                    </svg>
                {/if}
            </button>
        </div>

        <!-- Mobile controls -->
        <div class="flex items-center gap-2 md:hidden">
            <button
                on:click={toggleDarkMode}
                class="p-2 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-800 transition-colors"
                aria-label="Toggle dark mode"
            >
                {#if darkMode}
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="w-5 h-5"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                        stroke-width="2"
                    >
                        <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z"
                        />
                    </svg>
                {:else}
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="w-5 h-5"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                        stroke-width="2"
                    >
                        <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z"
                        />
                    </svg>
                {/if}
            </button>

            <button
                on:click={() => (isNavOpen = !isNavOpen)}
                class="p-2 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-800 transition-colors"
                aria-label="Toggle menu"
                aria-expanded={isNavOpen}
            >
                {#if isNavOpen}
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="w-5 h-5"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                        stroke-width="2"
                    >
                        <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            d="M6 18L18 6M6 6l12 12"
                        />
                    </svg>
                {:else}
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="w-5 h-5"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                        stroke-width="2"
                    >
                        <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            d="M4 6h16M4 12h16M4 18h16"
                        />
                    </svg>
                {/if}
            </button>
        </div>
    </div>

    <!-- Mobile menu -->
    {#if isNavOpen}
        <div
            transition:slide={{ duration: 250 }}
            class="md:hidden bg-white/95 dark:bg-slate-900/95 backdrop-blur-xl border-t border-slate-200/50 dark:border-slate-700/50"
        >
            <div class="px-6 py-4 flex flex-col gap-1">
                {#each links as { href, id, label }}
                    <a
                        {href}
                        on:click={() => (isNavOpen = false)}
                        class="text-sm font-medium rounded-lg transition-all py-2.5 px-3
                            {activeSection === id
                            ? 'text-rose-600 dark:text-rose-400 bg-rose-50 dark:bg-rose-900/20'
                            : 'text-slate-600 dark:text-slate-300 hover:text-rose-600 dark:hover:text-rose-400 hover:bg-slate-50 dark:hover:bg-slate-800/50'}"
                    >
                        {label}
                    </a>
                {/each}
            </div>
        </div>
    {/if}
</nav>
