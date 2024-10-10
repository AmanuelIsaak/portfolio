<script>
  import ProjectCard from "../components/ProjectCard.svelte";
  import ComingSoonProjectCard from "../components/ComingSoonProjectCard.svelte";
  import Photo from "../assets/photos.jpg"
</script>
<svelte:head>
  <meta property="description" content="hello world" />
</svelte:head>

<section class="" id="projects">
  <h1 class="mb-4 text-3xl font-extrabold text-gray-900 dark:text-white md:text-5xl lg:text-6xl"><span class="text-transparent bg-clip-text bg-gradient-to-r to-emerald-600 from-sky-400">My Projects</span></h1>
<div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4 bg-gray-900">
  <ProjectCard
          projectImage="{Photo}"
          projectLink="https://github.com/AmanuelIsaak/URL-shortner"
          projectName="URL-shortner"
          projectDesc="A simple url shortner written in Go to make the use of urls convenient"
  />

  <ProjectCard
          projectImage="{Photo}"
          projectLink="https://github.com/AmanuelIsaak/M165"
          projectName="MongoDB terminal client"
          projectDesc="A simple MongoDB terminal client written in Python for simple task"
  />

  <ProjectCard
          projectImage="{Photo}"
          projectLink="https://github.com/AmanuelIsaak/RockPaperScissor"
          projectName="Rock paper & Scissors"
          projectDesc="Written in Javascript this was one of the first projects I built"
  />

  <ProjectCard
          projectImage="{Photo}"
          projectLink="https://github.com/AmanuelIsaak/URL-shortner"
          projectName="URL-shortner"
          projectDesc="A simple url shortner written in Go to make the use of urls convenient"
  />

  <ComingSoonProjectCard
          projectName="Chat app"
  />

  <ComingSoonProjectCard
          projectName="Currency converter"
  />
</div>


</section>