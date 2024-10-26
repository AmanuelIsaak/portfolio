<script>
import Bild from "../assets/photos.jpg"
import GoSVG from "../assets/go.svg"
import SvelteSVG from "../assets/svelte.svg"
import ArchSVG from "../assets/arch.svg"
import JavaScriptSVG from "../assets/javascript.svg"
import StarSVG from "../assets/star.svg"
import GitSVG from "../assets/git.svg"
import NeovimSVG from "../assets/neovim.svg"
import MysqlSVG from "../assets/mysql.svg"
import Modal from "../components/Modal.svelte"
</script>

<section class="grid grid-cols-1 md:grid-cols-2 gap-4 bg-gray-900">
  <div class="lg:ml-24 flex flex-col">
    <h1 class="mb-8 text-center text-4xl font-extrabold text-gray-900 dark:text-white md:text-5xl lg:text-6xl"><span class="text-transparent bg-clip-text bg-gradient-to-r to-emerald-600 from-sky-400">Welcome here!</span></h1>
    <p class=" text-center text-xl text-gray-900 dark:text-white">I'm Amanuel, 19 and I'm currently in the 3rd year of <a class="font-medium text-blue-600 dark:text-blue-500 hover:underline" href="https://wg.edubs.ch/schulprofil/ims">IMS</a>. I'm an aspiring software engineer looking for internship</p>
  <div class="relative overflow-hidden bg-gray-900 py-8">
      <div class="flex flex-col">
        <h2>4<img src={StarSVG} alt="Languages">  </h2>
        <div class="flex space-x-8 animate-scroll">
          <img src={GitSVG} alt="Git" class="w-16 h-16">
          <img src={SvelteSVG} alt="Svelte" class="w-16 h-16">
          <img src={NeovimSVG} alt="Neovim" class="w-16 h-16">
        </div>
        <h2>3<img src={StarSVG} alt="Languages">  </h2>

        <div class="flex space-x-8 animate-scroll">
          <img src={JavaScriptSVG} alt="JavaScript" class="w-16 h-16">
          <img src={ArchSVG} alt="Arch" class="w-16 h-16">
          <img src={GoSVG} alt="Go" class="w-16 h-16">
        </div>
        <h2>2<img src={StarSVG} alt="Languages">  </h2>
        <div class="flex space-x-8 animate-scroll">
          <img src={JavaScriptSVG} alt="JavaScript" class="w-16 h-16">
          <img src={ArchSVG} alt="Arch" class="w-16 h-16">
        </div>
      </div>
  </div>
  </div>
  <img class="md:h-auto max-sm:w-full md:max-w-[75%] max-w-[75%] rounded-lg shadow-xl dark:shadow-gray-400" src={Bild} alt="Amanuel, 19">

  <Modal />

</section>
