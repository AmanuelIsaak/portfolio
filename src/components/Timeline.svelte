<script lang="ts">
    import ScrollReveal from "./ScrollReveal.svelte";

    const milestones = [
        {
            year: "2021",
            title: "Curiosity",
            icon: "M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z",
            description:
                "During the pandemic, while everyone was at home and computers were being purchased widely, I became curious about how computers work. My background in gaming sparked a fascination with coding and software development.",
        },
        {
            year: "2021 - 2022",
            title: "First Steps",
            icon: "M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.832 18.477 18.247 18 16.5 18c-1.746 0-3.332.477-4.5 1.253",
            description:
                "I decided to enter IMS to learn software engineering. I started building small projects like calculators and password generators. Even though they were simple, each one felt like a real achievement. Once enrolled, I dove into databases, HTML, CSS, and eventually overcame my hesitation around JavaScript.",
        },
        {
            year: "2022 - 2025",
            title: "Learning the Craft",
            icon: "M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4",
            description:
                "I gained experience with Go, Python, and JavaScript, building projects and deepening my understanding of software engineering. These years at IMS gave me a solid theoretical CS foundation.",
        },
        {
            year: "2025 - Present",
            title: "Shifting Focus",
            icon: "M13 10V3L4 14h7v7l9-11h-7z",
            description:
                "Started my software engineering internship and beginning Business Information Technology at FHNW Basel. My focus has shifted toward AI and business IT — combining my CS knowledge with AI and business fundamentals, working towards a career in IT consulting.",
        },
    ];
</script>

<div class="relative max-w-2xl">
    <!-- Gradient timeline line -->
    <div class="absolute left-[15px] top-2 bottom-2 w-px bg-gradient-to-b from-rose-500 via-orange-500 to-amber-500 opacity-30"></div>

    <ol class="space-y-12">
        {#each milestones as { year, title, icon, description }, i}
            <ScrollReveal delay={i * 120}>
                <li class="relative pl-12 group">
                    <!-- Animated dot -->
                    <div class="absolute left-0 top-0 w-[31px] h-[31px] rounded-full bg-rose-100 dark:bg-rose-900/40 flex items-center justify-center group-hover:scale-110 transition-transform duration-300">
                        <svg xmlns="http://www.w3.org/2000/svg" class="w-4 h-4 text-rose-600 dark:text-rose-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                            <path stroke-linecap="round" stroke-linejoin="round" d={icon} />
                        </svg>
                    </div>
                    <span class="text-xs font-semibold text-rose-600 dark:text-rose-400 uppercase tracking-wider">
                        {year}
                    </span>
                    <h3 class="text-lg font-semibold text-slate-900 dark:text-white mt-1 mb-2">
                        {title}
                    </h3>
                    <p class="text-slate-600 dark:text-slate-400 leading-relaxed">
                        {description}
                    </p>
                </li>
            </ScrollReveal>
        {/each}
    </ol>
</div>
