<script lang="ts">
    import { onMount } from "svelte";
    import Bild from "../assets/photos.jpg";

    let loaded = false;
    onMount(() => {
        loaded = true;
    });
</script>

<section
    id="hero"
    class="relative min-h-screen flex items-center justify-center px-6 pt-20 overflow-hidden"
>
    <!-- Floating background blobs -->
    <div class="absolute top-20 -left-32 w-72 h-72 bg-rose-300/20 dark:bg-rose-500/10 rounded-full blur-3xl animate-float"></div>
    <div class="absolute bottom-20 -right-32 w-96 h-96 bg-orange-300/20 dark:bg-orange-500/10 rounded-full blur-3xl animate-float-delayed"></div>
    <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[500px] h-[500px] bg-amber-200/10 dark:bg-amber-500/5 rounded-full blur-3xl animate-pulse-glow"></div>

    <div
        class="relative max-w-5xl mx-auto w-full flex flex-col md:flex-row items-center gap-12 md:gap-16
               transition-all duration-1000 {loaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'}"
    >
        <div class="flex-1 text-center md:text-left">
            <p class="inline-block text-sm font-semibold mb-4 tracking-wide uppercase px-3 py-1 rounded-full bg-rose-50 dark:bg-rose-900/30 text-rose-600 dark:text-rose-400 border border-rose-200/50 dark:border-rose-700/50">
                Business IT &amp; AI
            </p>
            <h1 class="text-4xl md:text-5xl lg:text-6xl font-bold leading-tight mb-4">
                <span class="text-slate-900 dark:text-white">Hi, I'm </span>
                <span class="gradient-text">Amanuel</span>
            </h1>
            <p class="text-lg text-slate-600 dark:text-slate-400 max-w-lg leading-relaxed">
                Combining computer science fundamentals, AI, and business knowledge.
                Currently doing my software engineering internship and starting
                Business Information Technology at
                <a
                    href="https://www.fhnw.ch"
                    class="text-rose-600 dark:text-rose-400 hover:underline font-medium"
                    target="_blank"
                    rel="noopener noreferrer"
                >FHNW Basel</a> this year, working towards a future in IT consulting.
            </p>
            <div class="mt-8 flex flex-wrap gap-4 justify-center md:justify-start">
                <a
                    href="#projects"
                    class="group inline-flex items-center gap-2 px-6 py-3 text-sm font-medium rounded-lg bg-rose-600 text-white hover:bg-rose-700 hover:shadow-lg hover:shadow-rose-500/25 transition-all duration-300"
                >
                    View Projects
                    <svg xmlns="http://www.w3.org/2000/svg" class="w-4 h-4 group-hover:translate-x-0.5 transition-transform" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M17 8l4 4m0 0l-4 4m4-4H3" />
                    </svg>
                </a>
                <a
                    href="#contact"
                    class="inline-flex items-center px-6 py-3 text-sm font-medium rounded-lg border border-slate-300 dark:border-slate-600 text-slate-700 dark:text-slate-300 hover:bg-slate-50 dark:hover:bg-slate-800 hover:border-slate-400 dark:hover:border-slate-500 transition-all duration-300"
                >
                    Get in Touch
                </a>
            </div>
        </div>

        <div class="relative flex-shrink-0 group">
            <!-- Animated glow ring -->
            <div class="absolute -inset-4 rounded-3xl bg-gradient-to-tr from-rose-500/20 via-orange-500/20 to-amber-500/20 blur-2xl opacity-50 group-hover:opacity-80 transition-opacity duration-700 animate-pulse-glow"></div>
            <!-- Decorative ring -->
            <div class="absolute -inset-1 rounded-2xl bg-gradient-to-tr from-rose-500 via-orange-500 to-amber-500 opacity-20 group-hover:opacity-40 transition-opacity duration-500"></div>
            <img
                src={Bild}
                alt="Amanuel"
                class="relative w-72 h-72 md:w-80 md:h-80 lg:w-96 lg:h-96 rounded-2xl object-cover object-top shadow-2xl"
            />
        </div>
    </div>

    <!-- Scroll indicator -->
    <div class="absolute bottom-8 left-1/2 -translate-x-1/2 transition-opacity duration-1000 {loaded ? 'opacity-100' : 'opacity-0'}" style="transition-delay: 1200ms;">
        <div class="flex flex-col items-center gap-2 text-slate-400 dark:text-slate-500">
            <span class="text-xs tracking-widest uppercase">Scroll</span>
            <div class="w-5 h-8 rounded-full border-2 border-slate-300 dark:border-slate-600 flex items-start justify-center p-1">
                <div class="w-1 h-2 bg-slate-400 dark:bg-slate-500 rounded-full animate-bounce"></div>
            </div>
        </div>
    </div>
</section>
