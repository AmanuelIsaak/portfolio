<script lang="ts">
    export let name = "";
    export let description = "";
    export let tech: string[] = [];
    export let featured = false;
    export let highlights: string[] = [];
    // Optional destinations. A card may have a live deployment, a public repo,
    // both, or neither (private work).
    export let demo = "";
    export let repo = "";
    export let repoLabel = "Source";
    // "live" | "source" | "private" | "soon"
    export let status = "";

    const techColors: Record<string, string> = {
        Go: "bg-sky-500",
        Python: "bg-blue-500",
        JavaScript: "bg-amber-500",
        TypeScript: "bg-blue-600",
        Rust: "bg-orange-600",
        Java: "bg-red-500",
        PHP: "bg-indigo-400",
        Svelte: "bg-orange-500",
        SvelteKit: "bg-orange-500",
        Tauri: "bg-yellow-500",
        Tailwind: "bg-cyan-500",
        MySQL: "bg-teal-500",
        "Three.js": "bg-slate-500",
        "PDF.js": "bg-red-400",
    };
    const dot = (t: string) => techColors[t] ?? "bg-slate-400";

    const statusStyles: Record<string, { label: string; class: string }> = {
        live: {
            label: "Live",
            class: "bg-emerald-50 text-emerald-600 dark:bg-emerald-900/30 dark:text-emerald-400",
        },
        source: {
            label: "Source",
            class: "bg-slate-100 text-slate-600 dark:bg-slate-700/60 dark:text-slate-300",
        },
        private: {
            label: "Private",
            class: "bg-violet-50 text-violet-600 dark:bg-violet-900/30 dark:text-violet-400",
        },
        soon: {
            label: "Soon",
            class: "bg-amber-50 text-amber-600 dark:bg-amber-900/30 dark:text-amber-400",
        },
    };

    // The card as a whole navigates to its most interesting destination: a live
    // deployment if there is one, otherwise the source. Secondary links sit
    // above the stretched overlay so they stay independently clickable.
    $: primary = demo || repo;
    $: badge = statusStyles[status];
</script>

<article
    class="card-glow group relative flex h-full flex-col rounded-xl border p-6 transition-all duration-300
           {primary
        ? 'border-slate-200 dark:border-slate-700/80 bg-white dark:bg-slate-800/50 hover:shadow-xl hover:shadow-rose-500/5 hover:-translate-y-1.5 focus-within:-translate-y-1.5'
        : 'border-slate-200 dark:border-slate-700/80 bg-white dark:bg-slate-800/50'}
           {featured ? 'md:col-span-2' : ''}"
>
    <div class="flex items-start justify-between gap-4 mb-3">
        <div class="flex items-center gap-2.5 flex-wrap">
            {#if featured}
                <span
                    class="inline-flex items-center gap-1 text-[11px] font-semibold uppercase tracking-wider px-2 py-0.5 rounded-full bg-gradient-to-r from-rose-500 to-orange-500 text-white"
                >
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="w-3 h-3"
                        viewBox="0 0 24 24"
                        fill="currentColor"
                    >
                        <path
                            d="M11.48 3.499a.562.562 0 011.04 0l2.125 5.111a.563.563 0 00.475.345l5.518.442c.499.04.701.663.321.988l-4.204 3.602a.563.563 0 00-.182.557l1.285 5.385a.562.562 0 01-.84.61l-4.725-2.885a.562.562 0 00-.586 0L6.982 20.54a.562.562 0 01-.84-.61l1.285-5.386a.562.562 0 00-.182-.557l-4.204-3.602a.563.563 0 01.321-.988l5.518-.442a.563.563 0 00.475-.345L11.48 3.5z"
                        />
                    </svg>
                    Featured
                </span>
            {/if}
            <h3
                class="font-semibold text-slate-900 dark:text-white transition-colors duration-300
                       {primary
                    ? 'group-hover:text-rose-600 dark:group-hover:text-rose-400'
                    : ''}
                       {featured ? 'text-xl md:text-2xl' : 'text-lg'}"
            >
                {#if primary}
                    <a
                        href={primary}
                        target="_blank"
                        rel="noopener noreferrer"
                        class="stretched-link rounded-sm focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-rose-500 focus-visible:ring-offset-2 dark:focus-visible:ring-offset-slate-900"
                    >
                        {name}
                    </a>
                {:else}
                    {name}
                {/if}
            </h3>
        </div>

        {#if badge}
            <span
                class="flex-shrink-0 text-[11px] font-semibold px-2 py-0.5 rounded-full {badge.class}"
            >
                {badge.label}
            </span>
        {/if}
    </div>

    <p
        class="text-sm text-slate-600 dark:text-slate-400 leading-relaxed mb-4 {featured
            ? 'max-w-2xl'
            : ''}"
    >
        {description}
    </p>

    {#if highlights.length}
        <ul class="flex flex-wrap gap-x-5 gap-y-1.5 mb-4">
            {#each highlights as h}
                <li
                    class="inline-flex items-center gap-1.5 text-xs text-slate-500 dark:text-slate-400"
                >
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="w-3.5 h-3.5 text-rose-500 flex-shrink-0"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                        stroke-width="2.5"
                    >
                        <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            d="M5 13l4 4L19 7"
                        />
                    </svg>
                    {h}
                </li>
            {/each}
        </ul>
    {/if}

    <div class="mt-auto pt-1">
        {#if tech.length}
            <div class="flex flex-wrap gap-2">
                {#each tech as t}
                    <span
                        class="inline-flex items-center gap-1.5 text-xs font-medium px-2.5 py-1 rounded-full bg-slate-100 dark:bg-slate-700/50 text-slate-600 dark:text-slate-300"
                    >
                        <span class="w-1.5 h-1.5 rounded-full {dot(t)}"></span>
                        {t}
                    </span>
                {/each}
            </div>
        {/if}

        {#if demo || repo}
            <div
                class="mt-4 flex flex-wrap items-center gap-4 border-t border-slate-100 dark:border-slate-700/60 pt-4"
            >
                {#if demo}
                    <a
                        href={demo}
                        target="_blank"
                        rel="noopener noreferrer"
                        class="relative z-10 inline-flex items-center gap-1.5 text-xs font-semibold text-rose-600 dark:text-rose-400 hover:gap-2 transition-all duration-300"
                    >
                        Live demo
                        <svg
                            xmlns="http://www.w3.org/2000/svg"
                            class="w-3.5 h-3.5"
                            fill="none"
                            viewBox="0 0 24 24"
                            stroke="currentColor"
                            stroke-width="2"
                        >
                            <path
                                stroke-linecap="round"
                                stroke-linejoin="round"
                                d="M7 17L17 7M17 7H7M17 7v10"
                            />
                        </svg>
                    </a>
                {/if}
                {#if repo}
                    <a
                        href={repo}
                        target="_blank"
                        rel="noopener noreferrer"
                        class="relative z-10 inline-flex items-center gap-1.5 text-xs font-semibold text-slate-500 dark:text-slate-400 hover:text-rose-600 dark:hover:text-rose-400 transition-colors"
                    >
                        <svg class="w-3.5 h-3.5" fill="currentColor" viewBox="0 0 24 24">
                            <path
                                d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"
                            />
                        </svg>
                        {repoLabel}
                    </a>
                {/if}
            </div>
        {/if}
    </div>
</article>
