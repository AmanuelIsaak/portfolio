<script lang="ts">
    import { onMount, onDestroy } from "svelte";
    import { fade } from "svelte/transition";
    import Bild from "../assets/photos.jpg";
    import ThreeBackground from "../components/ThreeBackground.svelte";

    let loaded = false;

    const roles = [
        "Software Engineer",
        "AI Enthusiast",
        "Business IT Student",
        "Future IT Consultant",
    ];
    let roleIndex = 0;
    let interval: ReturnType<typeof setInterval>;

    onMount(() => {
        loaded = true;
        const reduce = window.matchMedia(
            "(prefers-reduced-motion: reduce)",
        ).matches;
        if (!reduce) {
            interval = setInterval(() => {
                roleIndex = (roleIndex + 1) % roles.length;
            }, 2600);
        }
    });

    onDestroy(() => clearInterval(interval));

    const facts = [
        {
            label: "FHNW · Business IT",
            icon: "M12 14l9-5-9-5-9 5 9 5z M12 14l6.16-3.422a12.083 12.083 0 01.665 6.479A11.952 11.952 0 0012 20.055a11.952 11.952 0 00-6.824-2.998 12.078 12.078 0 01.665-6.479L12 14z",
        },
        {
            label: "Go · Python · JS",
            icon: "M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4",
        },
        {
            label: "AI · IT Consulting",
            icon: "M5 3v4M3 5h4M6 17v4m-2-2h4m5-16l2.286 6.857L21 12l-5.714 2.143L13 21l-2.286-6.857L5 12l5.714-2.143L13 3z",
        },
    ];
</script>

<section
    id="hero"
    class="relative min-h-[100svh] flex items-center justify-center px-6 pt-24 pb-16 overflow-hidden"
>
    <!-- Interactive 3D particle field (lazy, client-only) -->
    <ThreeBackground />

    <!-- Soft CSS blobs add depth and act as a WebGL fallback -->
    <div
        class="absolute top-24 -left-32 w-72 h-72 bg-rose-300/20 dark:bg-rose-500/10 rounded-full blur-3xl animate-float pointer-events-none"
    ></div>
    <div
        class="absolute bottom-24 -right-32 w-96 h-96 bg-orange-300/20 dark:bg-orange-500/10 rounded-full blur-3xl animate-float-delayed pointer-events-none"
    ></div>

    <!-- Legibility overlay: keeps text readable over the particles -->
    <div
        class="absolute inset-0 -z-10 pointer-events-none"
        style="background:
            radial-gradient(ellipse 70% 55% at 50% 45%, transparent 0%, rgb(var(--color-bg) / 0.35) 100%),
            linear-gradient(to bottom, rgb(var(--color-bg) / 0.3) 0%, transparent 18%, transparent 70%, rgb(var(--color-bg)) 100%);"
    ></div>

    <div
        class="relative max-w-5xl mx-auto w-full flex flex-col md:flex-row items-center gap-12 md:gap-16
               transition-all duration-1000 {loaded
            ? 'opacity-100 translate-y-0'
            : 'opacity-0 translate-y-8'}"
    >
        <div class="flex-1 text-center md:text-left">
            <p
                class="inline-flex items-center gap-2 text-xs font-semibold mb-5 tracking-wide uppercase px-3 py-1.5 rounded-full bg-rose-50/90 dark:bg-rose-900/40 text-rose-600 dark:text-rose-400 border border-rose-200/60 dark:border-rose-700/50 backdrop-blur-sm"
            >
                <span class="inline-flex h-2 w-2 rounded-full bg-rose-500"
                ></span>
                Software Engineer · Basel
            </p>

            <h1
                class="text-4xl md:text-5xl lg:text-6xl font-bold leading-tight mb-3"
            >
                <span class="text-slate-900 dark:text-white">Hi, I'm </span>
                <span class="gradient-text">Amanuel</span>
            </h1>

            <!-- Animated role rotator -->
            <div
                class="h-8 md:h-9 mb-5 text-xl md:text-2xl font-semibold text-slate-700 dark:text-slate-200"
            >
                <span class="text-slate-400 dark:text-slate-500">&gt;</span>
                {#key roleIndex}
                    <span
                        class="gradient-text inline-block"
                        in:fade={{ duration: 350 }}
                    >
                        {roles[roleIndex]}
                    </span>
                {/key}
            </div>

            <p
                class="text-lg text-slate-600 dark:text-slate-400 max-w-lg leading-relaxed mx-auto md:mx-0"
            >
                Combining computer science fundamentals, AI, and business
                knowledge. I work as a software engineer while studying Business
                Information Technology at
                <a
                    href="https://www.fhnw.ch"
                    class="text-rose-600 dark:text-rose-400 hover:underline font-medium"
                    target="_blank"
                    rel="noopener noreferrer">FHNW Basel</a
                >, with my sights set on a future in IT consulting.
            </p>

            <!-- Quick facts -->
            <div
                class="mt-6 flex flex-wrap items-center gap-x-5 gap-y-2 justify-center md:justify-start text-sm text-slate-500 dark:text-slate-400"
            >
                {#each facts as fact}
                    <span class="inline-flex items-center gap-1.5">
                        <svg
                            xmlns="http://www.w3.org/2000/svg"
                            class="w-4 h-4 text-rose-500/80"
                            fill="none"
                            viewBox="0 0 24 24"
                            stroke="currentColor"
                            stroke-width="1.8"
                        >
                            <path
                                stroke-linecap="round"
                                stroke-linejoin="round"
                                d={fact.icon}
                            />
                        </svg>
                        {fact.label}
                    </span>
                {/each}
            </div>

            <div
                class="mt-8 flex flex-wrap gap-4 justify-center md:justify-start"
            >
                <a
                    href="#projects"
                    class="group inline-flex items-center gap-2 px-6 py-3 text-sm font-medium rounded-lg bg-rose-600 text-white hover:bg-rose-700 hover:shadow-lg hover:shadow-rose-500/25 transition-all duration-300"
                >
                    View Projects
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="w-4 h-4 group-hover:translate-x-0.5 transition-transform"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                        stroke-width="2"
                    >
                        <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            d="M17 8l4 4m0 0l-4 4m4-4H3"
                        />
                    </svg>
                </a>
                <a
                    href="#contact"
                    class="inline-flex items-center px-6 py-3 text-sm font-medium rounded-lg border border-slate-300 dark:border-slate-600 text-slate-700 dark:text-slate-300 hover:bg-slate-50 dark:hover:bg-slate-800 hover:border-slate-400 dark:hover:border-slate-500 transition-all duration-300 backdrop-blur-sm"
                >
                    Get in Touch
                </a>
            </div>
        </div>

        <div class="relative flex-shrink-0 group">
            <!-- Animated glow ring -->
            <div
                class="absolute -inset-4 rounded-3xl bg-gradient-to-tr from-rose-500/20 via-orange-500/20 to-amber-500/20 blur-2xl opacity-50 group-hover:opacity-80 transition-opacity duration-700 animate-pulse-glow"
            ></div>
            <!-- Decorative ring -->
            <div
                class="absolute -inset-1 rounded-2xl bg-gradient-to-tr from-rose-500 via-orange-500 to-amber-500 opacity-20 group-hover:opacity-40 transition-opacity duration-500"
            ></div>
            <img
                src={Bild}
                alt="Amanuel"
                class="relative w-64 h-64 sm:w-72 sm:h-72 md:w-80 md:h-80 lg:w-96 lg:h-96 rounded-2xl object-cover object-top shadow-2xl"
            />
        </div>
    </div>

    <!-- Scroll indicator -->
    <div
        class="absolute bottom-8 left-1/2 -translate-x-1/2 transition-opacity duration-1000 {loaded
            ? 'opacity-100'
            : 'opacity-0'}"
        style="transition-delay: 1200ms;"
    >
        <div
            class="flex flex-col items-center gap-2 text-slate-400 dark:text-slate-500"
        >
            <span class="text-xs tracking-widest uppercase">Scroll</span>
            <div
                class="w-5 h-8 rounded-full border-2 border-slate-300 dark:border-slate-600 flex items-start justify-center p-1"
            >
                <div
                    class="w-1 h-2 bg-slate-400 dark:bg-slate-500 rounded-full animate-bounce"
                ></div>
            </div>
        </div>
    </div>
</section>
