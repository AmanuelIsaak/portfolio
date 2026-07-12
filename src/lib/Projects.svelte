<script lang="ts">
    import ProjectCard from "../components/ProjectCard.svelte";
    import ScrollReveal from "../components/ScrollReveal.svelte";

    type Project = {
        name: string;
        description: string;
        tech: string[];
        status: string;
        demo?: string;
        repo?: string;
        repoLabel?: string;
        highlights?: string[];
    };

    const featured: Project = {
        name: "PDF Reader",
        description:
            "A lightweight desktop PDF reader and editor. It renders documents with PDF.js and writes edited copies with pdf-lib, while native Rust commands handle the file dialogs, filesystem access, and recent-file history. You can fill interactive form fields, add text, highlights, and freehand drawings, then export without ever touching the source file.",
        tech: ["Tauri", "Rust", "Svelte", "TypeScript", "Tailwind"],
        status: "private",
        highlights: [
            "Native Rust file I/O",
            "Form filling & annotations",
            "Full-document text search",
        ],
    };

    const projects: Project[] = [
        {
            name: "My Circle",
            description:
                "A personal relationship tracker that maps the people in your life across concentric circles of closeness. Three ways to view the same data — circle, timeline, and grid — with everything stored locally in the browser.",
            tech: ["Svelte", "TypeScript", "Tailwind"],
            demo: "https://family-tree-tau-nine.vercel.app",
            repo: "https://github.com/AmanuelIsaak/my-circle",
            status: "live",
        },
        {
            name: "URL Shortener",
            description:
                "A minimal URL shortener written in Go — takes a long link, hands back a short one, and redirects. Server-rendered templates, no external dependencies, small enough to read end to end.",
            tech: ["Go"],
            repo: "https://github.com/AmanuelIsaak/URL-shortner",
            status: "source",
        },
        {
            name: "This Portfolio",
            description:
                "The site you're reading right now — SvelteKit and Tailwind, with an interactive Three.js particle field behind the hero and a dark mode that remembers your choice.",
            tech: ["SvelteKit", "Tailwind", "Three.js"],
            demo: "https://amanuel-isaak.vercel.app",
            repo: "https://github.com/AmanuelIsaak/portfolio",
            status: "live",
        },
        {
            name: "More in progress",
            description:
                "I'm usually building something. Recent work has pulled me toward desktop apps, Rust, and AI-assisted tooling — the newest things land on GitHub first.",
            tech: [],
            repo: "https://github.com/AmanuelIsaak",
            repoLabel: "GitHub",
            status: "soon",
        },
    ];
</script>

<section id="projects" class="relative py-24 md:py-32 px-6 overflow-hidden">
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
                Each of these started as something I actually wanted to exist.
                Most began simple, and every one taught me something about
                structuring code, reading documentation, and shipping software
                end to end.
            </p>
        </ScrollReveal>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-5">
            <ScrollReveal>
                <ProjectCard
                    name={featured.name}
                    description={featured.description}
                    tech={featured.tech}
                    status={featured.status}
                    highlights={featured.highlights ?? []}
                    featured
                />
            </ScrollReveal>

            {#each projects as project, i}
                <ScrollReveal delay={i * 80}>
                    <ProjectCard
                        name={project.name}
                        description={project.description}
                        tech={project.tech}
                        demo={project.demo ?? ""}
                        repo={project.repo ?? ""}
                        repoLabel={project.repoLabel ?? "Source"}
                        status={project.status}
                    />
                </ScrollReveal>
            {/each}
        </div>
    </div>
</section>
