<script lang="ts">
    export let name = "";
    export let link = "";
    export let description = "";
    export let tech: string[] = [];
    export let featured = false;
    export let highlights: string[] = [];
    // "source" | "live" | "concept" | "soon"
    export let status = "";

    const techColors: Record<string, string> = {
        Go: "bg-sky-500",
        Python: "bg-blue-500",
        JavaScript: "bg-amber-500",
        TypeScript: "bg-blue-600",
        Java: "bg-red-500",
        PHP: "bg-indigo-400",
        Svelte: "bg-orange-500",
        Tailwind: "bg-cyan-500",
        MySQL: "bg-teal-500",
        "Three.js": "bg-slate-500",
        FastAPI: "bg-emerald-500",
        "Claude API": "bg-rose-500",
        SvelteKit: "bg-orange-500",
    };
    const dot = (t: string) => techColors[t] ?? "bg-slate-400";

    const statusStyles: Record<
        string,
        { label: string; class: string }
    > = {
        source: {
            label: "Source",
            class: "bg-slate-100 text-slate-600 dark:bg-slate-700/60 dark:text-slate-300",
        },
        live: {
            label: "Live",
            class: "bg-emerald-50 text-emerald-600 dark:bg-emerald-900/30 dark:text-emerald-400",
        },
        concept: {
            label: "Concept",
            class: "bg-violet-50 text-violet-600 dark:bg-violet-900/30 dark:text-violet-400",
        },
        soon: {
            label: "Soon",
            class: "bg-amber-50 text-amber-600 dark:bg-amber-900/30 dark:text-amber-400",
        },
    };

    $: isLink = !!link && status !== "soon";
    $: badge = statusStyles[status];
</script>

<svelte:element
    this={isLink ? "a" : "div"}
    href={isLink ? link : undefined}
    target={isLink ? "_blank" : undefined}
    rel={isLink ? "noopener noreferrer" : undefined}
    class="card-glow group flex h-full flex-col rounded-xl border p-6 transition-all duration-300
           {status === 'soon'
        ? 'border-dashed border-slate-300 dark:border-slate-700 bg-transparent'
        : 'border-slate-200 dark:border-slate-700/80 bg-white dark:bg-slate-800/50 hover:shadow-xl hover:shadow-rose-500/5 hover:-translate-y-1.5'}
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
                       {status !== 'soon'
                    ? 'group-hover:text-rose-600 dark:group-hover:text-rose-400'
                    : ''}
                       {featured ? 'text-xl md:text-2xl' : 'text-lg'}"
            >
                {name}
            </h3>
        </div>

        {#if badge}
            <span
                class="flex-shrink-0 text-[11px] font-semibold px-2 py-0.5 rounded-full {badge.class}"
            >
                {badge.label}
            </span>
        {:else if isLink}
            <svg
                xmlns="http://www.w3.org/2000/svg"
                class="w-4 h-4 text-slate-400 group-hover:text-rose-500 transition-all duration-300 group-hover:translate-x-0.5 group-hover:-translate-y-0.5 flex-shrink-0 mt-1"
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
                        class="w-3.5 h-3.5 text-rose-500"
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

    {#if tech.length}
        <div class="mt-auto flex flex-wrap gap-2 pt-1">
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
</svelte:element>
