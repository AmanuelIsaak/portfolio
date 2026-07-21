<script lang="ts">
    import ScrollReveal from "../components/ScrollReveal.svelte";

    import typescript from "../assets/typescript.svg";
    import svelte from "../assets/svelte.svg";
    import tailwind from "../assets/tailwind.svg";
    import go from "../assets/go.svg";
    import postgres from "../assets/postgres.svg";
    import redis from "../assets/redis.svg";
    import neon from "../assets/neon.svg";
    import vercel from "../assets/vercel.svg";
    import rust from "../assets/rust.svg";
    import tauri from "../assets/tauri.svg";
    import git from "../assets/git.svg";
    import neovim from "../assets/neovim.svg";
    import arch from "../assets/arch.svg";

    // Single source of truth for the scrolling marquee.
    const logos = [
        { name: "TypeScript", src: typescript },
        { name: "Svelte", src: svelte },
        { name: "Tailwind", src: tailwind },
        { name: "Go", src: go },
        { name: "Postgres", src: postgres },
        { name: "Redis", src: redis },
        { name: "Neon", src: neon },
        { name: "Vercel", src: vercel },
        { name: "Rust", src: rust },
        { name: "Tauri", src: tauri },
        { name: "Git", src: git },
        { name: "Neovim", src: neovim },
        { name: "Arch", src: arch },
    ];

    const categories = [
        {
            title: "Languages",
            icon: "M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4",
            items: ["TypeScript", "Go", "Rust"],
        },
        {
            title: "Web & Desktop",
            icon: "M21 12a9 9 0 01-9 9m9-9a9 9 0 00-9-9m9 9H3m9 9a9 9 0 01-9-9m9 9c1.657 0 3-4.03 3-9s-1.343-9-3-9m0 18c-1.657 0-3-4.03-3-9s1.343-9 3-9m-9 9a9 9 0 019-9",
            items: ["Svelte", "SvelteKit", "Tauri", "Tailwind CSS", "HTML & CSS"],
        },
        {
            title: "Data & Infrastructure",
            icon: "M4 7v10c0 2.21 3.582 4 8 4s8-1.79 8-4V7M4 7c0 2.21 3.582 4 8 4s8-1.79 8-4M4 7c0-2.21 3.582-4 8-4s8 1.79 8 4",
            items: ["Postgres", "Neon", "Redis", "Vercel"],
        },
        {
            title: "Tools & Environment",
            icon: "M11.42 15.17L17.25 21A2.652 2.652 0 0021 17.25l-5.877-5.877M11.42 15.17l2.496-3.03c.317-.384.74-.626 1.208-.766M11.42 15.17l-4.655 5.653a2.548 2.548 0 11-3.586-3.586l6.837-5.63m5.106-2.41l2.063-2.065a2 2 0 00-2.828-2.828L9.5 9.5",
            items: ["Git", "Neovim", "Arch Linux", "Docker"],
        },
    ];

    // Not claimed as experience — things I'm deliberately heading toward next.
    const exploring = ["Rust", "Kotlin"];
</script>

<section id="stack" class="relative py-24 md:py-32 overflow-hidden">
    <!-- Decorative blob -->
    <div
        class="absolute top-10 right-0 w-72 h-72 bg-amber-200/15 dark:bg-amber-500/5 rounded-full blur-3xl pointer-events-none"
    ></div>

    <div class="relative max-w-5xl mx-auto px-6">
        <ScrollReveal>
            <p
                class="inline-block text-sm font-semibold mb-4 tracking-wide uppercase px-3 py-1 rounded-full bg-rose-50 dark:bg-rose-900/30 text-rose-600 dark:text-rose-400 border border-rose-200/50 dark:border-rose-700/50"
            >
                Tech Stack
            </p>
            <h2
                class="text-3xl md:text-4xl font-bold text-slate-900 dark:text-white mb-6"
            >
                Tools I <span class="gradient-text">Work With</span>
            </h2>
            <p
                class="text-slate-600 dark:text-slate-400 max-w-2xl leading-relaxed mb-12"
            >
                A short list on purpose. These are the things I actually reach
                for — TypeScript and Svelte on the front, Go and Postgres behind
                it, shipped on Vercel.
            </p>
        </ScrollReveal>
    </div>

    <!-- Infinite logo marquee (full-bleed) -->
    <div class="marquee marquee-mask relative mb-14">
        <div class="flex w-max animate-marquee">
            {#each [...logos, ...logos] as logo, i}
                <div
                    class="flex items-center gap-2.5 mx-3 px-5 py-3 rounded-xl border border-slate-200 dark:border-slate-700/70 bg-white/70 dark:bg-slate-800/40 backdrop-blur-sm shadow-sm whitespace-nowrap"
                    aria-hidden={i >= logos.length ? "true" : undefined}
                >
                    <img
                        src={logo.src}
                        alt={i < logos.length ? logo.name : ""}
                        class="w-6 h-6 object-contain"
                        loading="lazy"
                        draggable="false"
                    />
                    <span
                        class="text-sm font-medium text-slate-700 dark:text-slate-200"
                        >{logo.name}</span
                    >
                </div>
            {/each}
        </div>
    </div>

    <!-- Skill category cards -->
    <div class="relative max-w-5xl mx-auto px-6">
        <div class="grid grid-cols-1 sm:grid-cols-2 gap-5">
            {#each categories as cat, i}
                <ScrollReveal delay={i * 90}>
                    <div
                        class="h-full rounded-xl border border-slate-200 dark:border-slate-700/80 bg-white dark:bg-slate-800/50 p-6 hover:border-rose-200 dark:hover:border-rose-800/60 transition-colors duration-300"
                    >
                        <div class="flex items-center gap-3 mb-4">
                            <span
                                class="flex items-center justify-center w-9 h-9 rounded-lg bg-rose-50 dark:bg-rose-900/40 text-rose-600 dark:text-rose-400"
                            >
                                <svg
                                    xmlns="http://www.w3.org/2000/svg"
                                    class="w-5 h-5"
                                    fill="none"
                                    viewBox="0 0 24 24"
                                    stroke="currentColor"
                                    stroke-width="1.8"
                                >
                                    <path
                                        stroke-linecap="round"
                                        stroke-linejoin="round"
                                        d={cat.icon}
                                    />
                                </svg>
                            </span>
                            <h3
                                class="text-base font-semibold text-slate-900 dark:text-white"
                            >
                                {cat.title}
                            </h3>
                        </div>
                        <div class="flex flex-wrap gap-2">
                            {#each cat.items as item}
                                <span
                                    class="text-xs font-medium px-2.5 py-1 rounded-full bg-slate-100 dark:bg-slate-700/50 text-slate-600 dark:text-slate-300"
                                >
                                    {item}
                                </span>
                            {/each}
                        </div>
                    </div>
                </ScrollReveal>
            {/each}
        </div>

        <ScrollReveal>
            <p
                class="mt-8 flex flex-wrap items-center gap-2 text-sm text-slate-600 dark:text-slate-400"
            >
                <span>Going deeper next, for app development:</span>
                {#each exploring as item}
                    <span
                        class="text-xs font-medium px-2.5 py-1 rounded-full border border-dashed border-rose-300 dark:border-rose-700/70 text-rose-600 dark:text-rose-400"
                    >
                        {item}
                    </span>
                {/each}
            </p>
        </ScrollReveal>
    </div>
</section>
