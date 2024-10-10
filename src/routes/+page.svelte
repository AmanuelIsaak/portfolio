<script>
  import About from "$lib/About.svelte";
  import Home from "$lib/Home.svelte";
  import Project from "$lib/Projects.svelte";
</script>

<svelte:head>
  <meta property="description" content="Home" />
</svelte:head>

<slot />

<section>
  <Home/>
</section>

<section>
  <About />
</section>
<section>
  <Project />
</section>
