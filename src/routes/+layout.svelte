<script lang="ts">
    import "../app.css";
    import Navbar from "../components/Navbar.svelte";
    import Footer from "../components/Footer.svelte";
    import { onMount } from "svelte";

    onMount(() => {
        const saved = localStorage.getItem("theme");
        if (saved === "dark" || (!saved && window.matchMedia("(prefers-color-scheme: dark)").matches)) {
            document.documentElement.classList.add("dark");
        } else {
            document.documentElement.classList.remove("dark");
        }
    });
</script>

<div class="min-h-screen flex flex-col">
    <Navbar />
    <main class="flex-1">
        <slot />
    </main>
    <Footer />
</div>
