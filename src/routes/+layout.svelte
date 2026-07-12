<script lang="ts">
    import "../app.css";
    import Navbar from "../components/Navbar.svelte";
    import Footer from "../components/Footer.svelte";
    // The theme class is set by a blocking script in app.html, before first paint.
</script>

<a
    href="#main"
    class="sr-only focus:not-sr-only focus:absolute focus:top-4 focus:left-4 focus:z-[60] focus:rounded-lg focus:bg-rose-600 focus:px-4 focus:py-2 focus:text-sm focus:font-medium focus:text-white"
>
    Skip to content
</a>

<div class="min-h-screen flex flex-col">
    <Navbar />
    <main id="main" class="flex-1">
        <slot />
    </main>
    <Footer />
</div>
