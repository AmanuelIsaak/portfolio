<script>
    import Timeline from "../components/Timeline.svelte";
    import ScrollReveal from "../components/ScrollReveal.svelte";
</script>

<section id="about" class="relative py-24 md:py-32 px-6 overflow-hidden">
    <!-- Background dot pattern -->
    <div class="absolute inset-0 dot-pattern opacity-40 dark:opacity-20"></div>
    <!-- Decorative blob -->
    <div class="absolute -top-20 -right-40 w-80 h-80 bg-orange-200/20 dark:bg-orange-500/5 rounded-full blur-3xl"></div>

    <div class="relative max-w-5xl mx-auto">
        <ScrollReveal>
            <p class="inline-block text-sm font-semibold mb-4 tracking-wide uppercase px-3 py-1 rounded-full bg-rose-50 dark:bg-rose-900/30 text-rose-600 dark:text-rose-400 border border-rose-200/50 dark:border-rose-700/50">
                About Me
            </p>
            <h2 class="text-3xl md:text-4xl font-bold text-slate-900 dark:text-white mb-6">
                My <span class="gradient-text">Journey</span>
            </h2>
            <p class="text-slate-600 dark:text-slate-400 max-w-2xl leading-relaxed mb-16">
                From curiosity during the pandemic to pursuing software engineering at IMS, here's how my path in tech has unfolded.
            </p>
        </ScrollReveal>

        <ScrollReveal>
            <Timeline />
        </ScrollReveal>
    </div>
</section>
