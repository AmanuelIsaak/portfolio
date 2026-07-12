<script>
    import Home from "$lib/Home.svelte";
    import About from "$lib/About.svelte";
    import Stack from "$lib/Stack.svelte";
    import Projects from "$lib/Projects.svelte";
    import Contact from "$lib/Contact.svelte";

    const title = "Amanuel Isaak — Software Engineer";
    const description =
        "Software engineer in Basel, studying Business Information Technology at FHNW. I build with Go, Rust, Python, and Svelte — from desktop apps to web tools.";
    const url = "https://amanuel-isaak.vercel.app";
</script>

<svelte:head>
    <title>{title}</title>
    <meta name="description" content={description} />
    <meta name="author" content="Amanuel Isaak" />
    <link rel="canonical" href={url} />

    <meta property="og:type" content="website" />
    <meta property="og:title" content={title} />
    <meta property="og:description" content={description} />
    <meta property="og:url" content={url} />
    <meta property="og:site_name" content="Amanuel Isaak" />

    <meta name="twitter:card" content="summary_large_image" />
    <meta name="twitter:title" content={title} />
    <meta name="twitter:description" content={description} />
</svelte:head>

<Home />
<About />
<Stack />
<Projects />
<Contact />
