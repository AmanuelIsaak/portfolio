<script>
import ProjectCard from "../components/ProjectCard.svelte";
</script>

<section class="md:w-[80%] mx-auto pb-32" id="projects">
  <h1 class="text-3xl font-extrabold text-gray-900 dark:text-white md:text-5xl lg:text-6xl"><span class="text-transparent bg-clip-text bg-gradient-to-r to-emerald-600 from-sky-400">My Projects</span></h1>

  <p class="text-base font-normal text-gray-500 dark:text-gray-400 lg:w-[80%]">At last here are some of the projects I've worked on.Most of them are fairly simple but have tought me alot. For example how I should go about structuring a project, researching multiple solutions and picking the "best" and general programming knowledge.</p>


  <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4 bg-gray-900">
    <ProjectCard
      projectLink="https://github.com/AmanuelIsaak/URL-shortner"
      projectName="URL-shortner"
      projectDesc="A simple url shortner written in Go to make the use of urls convenient"
    />

    <ProjectCard
      projectLink="https://github.com/AmanuelIsaak/M165"
      projectName="MongoDB terminal client"
      projectDesc="A simple MongoDB terminal client written in Python for simple task"
    />

    <ProjectCard
      projectLink="https://github.com/AmanuelIsaak/RockPaperScissor"
      projectName="Rock paper & Scissors"
      projectDesc="Written in Javascript this was one of the first projects I built"
    />
</div>
</section>
