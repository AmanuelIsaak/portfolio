<script lang="ts">
    import { onMount } from "svelte";

    export let delay = 0;

    let element: HTMLDivElement;
    let visible = false;

    onMount(() => {
        const observer = new IntersectionObserver(
            (entries) => {
                entries.forEach((entry) => {
                    if (entry.isIntersecting) {
                        setTimeout(() => {
                            visible = true;
                        }, delay);
                        observer.unobserve(entry.target);
                    }
                });
            },
            { threshold: 0.1 }
        );

        observer.observe(element);

        return () => observer.disconnect();
    });
</script>

<div
    bind:this={element}
    class="transition-all duration-600 ease-out
           {visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-6'}"
    style="transition-duration: 600ms;"
>
    <slot />
</div>
