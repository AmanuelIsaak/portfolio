<script>
    import ProjectCard from "../components/ProjectCard.svelte";
    import ScrollReveal from "../components/ScrollReveal.svelte";

    const projects = [
        {
            name: "URL Shortener",
            description: "A simple URL shortener written in Go to make the use of URLs convenient.",
            tech: "Go",
            link: "https://github.com/AmanuelIsaak/URL-shortner",
        },
        {
            name: "My Portfolio",
            description: "My personal portfolio built with Svelte and Tailwind CSS.",
            tech: "Svelte",
            link: "https://github.com/AmanuelIsaak/portfolio",
        },
    ];
</script>

<section id="projects" class="relative py-24 md:py-32 px-6 overflow-hidden">
    <!-- Decorative blobs -->
    <div class="absolute -bottom-20 -left-40 w-80 h-80 bg-orange-200/20 dark:bg-orange-500/5 rounded-full blur-3xl animate-float-delayed"></div>
    <div class="absolute top-40 -right-20 w-60 h-60 bg-rose-200/15 dark:bg-rose-500/5 rounded-full blur-3xl animate-float"></div>

    <div class="relative max-w-5xl mx-auto">
        <ScrollReveal>
            <p class="inline-block text-sm font-semibold mb-4 tracking-wide uppercase px-3 py-1 rounded-full bg-rose-50 dark:bg-rose-900/30 text-rose-600 dark:text-rose-400 border border-rose-200/50 dark:border-rose-700/50">
                Projects
            </p>
            <h2 class="text-3xl md:text-4xl font-bold text-slate-900 dark:text-white mb-6">
                Things I've <span class="gradient-text">Built</span>
            </h2>
            <p class="text-slate-600 dark:text-slate-400 max-w-2xl leading-relaxed mb-12">
                Here are some of the projects I've worked on. Most of them are fairly
                simple but have taught me a lot about structuring a project, researching
                solutions, and general programming knowledge.
            </p>
        </ScrollReveal>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-5">
            {#each projects as project, i}
                <ScrollReveal delay={i * 100}>
                    <ProjectCard
                        projectName={project.name}
                        projectDesc={project.description}
                        projectTech={project.tech}
                        projectLink={project.link}
                    />
                </ScrollReveal>
            {/each}
        </div>
    </div>
</section>
