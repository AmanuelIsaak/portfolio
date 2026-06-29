<script lang="ts">
    import ProjectCard from "../components/ProjectCard.svelte";
    import ScrollReveal from "../components/ScrollReveal.svelte";

    const featured = {
        name: "AI Study Assistant",
        description:
            "A retrieval-augmented study tool that turns lecture PDFs into an interactive tutor — upload your notes, ask questions, and get answers with citations back to the source. Built around the Claude API.",
        tech: ["Python", "FastAPI", "Claude API", "Svelte"],
        link: "https://github.com/AmanuelIsaak",
        status: "concept",
        highlights: [
            "RAG pipeline",
            "Streaming answers",
            "Source citations",
        ],
    };

    const projects = [
        {
            name: "URL Shortener",
            description:
                "A fast, minimal URL shortener written in Go — clean redirect service with a tiny footprint and zero external dependencies.",
            tech: ["Go"],
            link: "https://github.com/AmanuelIsaak/URL-shortner",
            status: "source",
        },
        {
            name: "This Portfolio",
            description:
                "The site you're looking at right now — SvelteKit and Tailwind, with an interactive Three.js particle hero.",
            tech: ["Svelte", "Tailwind", "Three.js"],
            link: "https://github.com/AmanuelIsaak/portfolio",
            status: "source",
        },
        {
            name: "Expense Tracker",
            description:
                "A small full-stack app to log and visualise spending, backed by a MySQL database — an example project from my IMS coursework.",
            tech: ["PHP", "MySQL"],
            link: "https://github.com/AmanuelIsaak",
            status: "concept",
        },
        {
            name: "CLI Toolkit",
            description:
                "A grab-bag of command-line utilities I use day to day — a password generator, a file organiser, and a few handy scripts.",
            tech: ["Go", "Python"],
            link: "https://github.com/AmanuelIsaak",
            status: "concept",
        },
        {
            name: "More on the way",
            description:
                "I'm always tinkering. New projects around AI and business IT are in progress — check back soon, or follow along on GitHub.",
            tech: [],
            status: "soon",
        },
    ];
</script>

<section
    id="projects"
    class="relative py-24 md:py-32 px-6 overflow-hidden"
>
    <!-- Decorative blobs -->
    <div
        class="absolute -bottom-20 -left-40 w-80 h-80 bg-orange-200/20 dark:bg-orange-500/5 rounded-full blur-3xl animate-float-delayed pointer-events-none"
    ></div>
    <div
        class="absolute top-40 -right-20 w-60 h-60 bg-rose-200/15 dark:bg-rose-500/5 rounded-full blur-3xl animate-float pointer-events-none"
    ></div>

    <div class="relative max-w-5xl mx-auto">
        <ScrollReveal>
            <p
                class="inline-block text-sm font-semibold mb-4 tracking-wide uppercase px-3 py-1 rounded-full bg-rose-50 dark:bg-rose-900/30 text-rose-600 dark:text-rose-400 border border-rose-200/50 dark:border-rose-700/50"
            >
                Projects
            </p>
            <h2
                class="text-3xl md:text-4xl font-bold text-slate-900 dark:text-white mb-6"
            >
                Things I've <span class="gradient-text">Built</span>
            </h2>
            <p
                class="text-slate-600 dark:text-slate-400 max-w-2xl leading-relaxed mb-12"
            >
                A mix of shipped projects and concepts I'm exploring. Most started
                simple, but each one taught me something about structuring code,
                researching solutions, and shipping software end to end.
            </p>
        </ScrollReveal>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-5">
            <ScrollReveal>
                <ProjectCard
                    name={featured.name}
                    description={featured.description}
                    tech={featured.tech}
                    link={featured.link}
                    status={featured.status}
                    highlights={featured.highlights}
                    featured
                />
            </ScrollReveal>

            {#each projects as project, i}
                <ScrollReveal delay={i * 80}>
                    <ProjectCard
                        name={project.name}
                        description={project.description}
                        tech={project.tech}
                        link={project.link}
                        status={project.status}
                    />
                </ScrollReveal>
            {/each}
        </div>
    </div>
</section>
