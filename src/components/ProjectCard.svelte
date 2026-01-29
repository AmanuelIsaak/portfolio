<script lang="ts">
    export let projectName = "";
    export let projectLink = "";
    export let projectDesc = "";
    export let projectTech = "";

    const techColors: Record<string, { bg: string; text: string; darkBg: string; darkText: string; dot: string }> = {
        Go:         { bg: "bg-sky-50",    text: "text-sky-700",    darkBg: "dark:bg-sky-900/30",    darkText: "dark:text-sky-400",    dot: "bg-sky-500" },
        Python:     { bg: "bg-yellow-50", text: "text-yellow-700", darkBg: "dark:bg-yellow-900/30", darkText: "dark:text-yellow-400", dot: "bg-yellow-500" },
        JavaScript: { bg: "bg-amber-50",  text: "text-amber-700",  darkBg: "dark:bg-amber-900/30",  darkText: "dark:text-amber-400",  dot: "bg-amber-500" },
        Svelte:     { bg: "bg-orange-50", text: "text-orange-700", darkBg: "dark:bg-orange-900/30", darkText: "dark:text-orange-400", dot: "bg-orange-500" },
    };

    $: colors = techColors[projectTech] ?? {
        bg: "bg-slate-100", text: "text-slate-600", darkBg: "dark:bg-slate-700/50", darkText: "dark:text-slate-300", dot: "bg-slate-400"
    };
</script>

<a
    href={projectLink}
    target="_blank"
    rel="noopener noreferrer"
    class="card-glow group block rounded-xl border border-slate-200 dark:border-slate-700/80 bg-white dark:bg-slate-800/50 p-6
           hover:shadow-xl hover:shadow-rose-500/5 hover:-translate-y-1.5 transition-all duration-300"
>
    <div class="flex items-start justify-between mb-3">
        <h3 class="text-lg font-semibold text-slate-900 dark:text-white group-hover:text-rose-600 dark:group-hover:text-rose-400 transition-colors duration-300">
            {projectName}
        </h3>
        <svg
            xmlns="http://www.w3.org/2000/svg"
            class="w-4 h-4 text-slate-400 group-hover:text-rose-500 transition-all duration-300 group-hover:translate-x-0.5 group-hover:-translate-y-0.5 flex-shrink-0 mt-1"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
            stroke-width="2"
        >
            <path stroke-linecap="round" stroke-linejoin="round" d="M7 17L17 7M17 7H7M17 7v10" />
        </svg>
    </div>
    <p class="text-sm text-slate-600 dark:text-slate-400 leading-relaxed mb-4">
        {projectDesc}
    </p>
    {#if projectTech}
        <span class="inline-flex items-center gap-1.5 text-xs font-semibold px-2.5 py-1 rounded-full {colors.bg} {colors.darkBg} {colors.text} {colors.darkText}">
            <span class="w-1.5 h-1.5 rounded-full {colors.dot}"></span>
            {projectTech}
        </span>
    {/if}
</a>
