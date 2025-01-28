<script>
    import Bild from "../assets/photos.jpg";
    import GoSVG from "../assets/go.svg";
    import SvelteSVG from "../assets/svelte.svg";
    import ArchSVG from "../assets/arch.svg";
    import JavaScriptSVG from "../assets/javascript.svg";
    import StarSVG from "../assets/star.svg";
    import GitSVG from "../assets/git.svg";
    import MysqlSVG from "../assets/mysql.svg";
    import JavaSVG from "../assets/java.svg";
    import PhpSVG from "../assets/php.svg";
    import VimSVG from "../assets/neovim.svg";
    import Modal from "../components/Modal.svelte";
</script>

<section class="grid grid-cols-1 md:grid-cols-2 gap-4 bg-gray-900">
    <div class="lg:ml-24 flex flex-col">
        <h1
            class="mb-4 text-3xl font-extrabold text-gray-900 dark:text-white md:text-5xl lg:text-6xl text-center"
        >
            <span
                class="text-transparent bg-clip-text bg-gradient-to-r to-emerald-600 from-sky-400"
                >Welcome here!</span
            >
        </h1>
        <p class=" text-center text-xl text-gray-900 dark:text-white">
            I'm Amanuel, 19 and I'm currently in the 3rd year of <a
                class="font-medium text-blue-600 dark:text-blue-500 hover:underline"
                href="https://wg.edubs.ch/schulprofil/ims">IMS</a
            >. I'm an aspiring software engineer looking for internship
        </p>

        <div class="relative overflow-hidden bg-gray-900 py-8">
            <div class="flex flex-col">
                <div class="flex items-center space-x-8">
                    <h1
                        class="flex items-center space-x-2 h-16 text-gray-900 dark:text-white"
                    >
                        4<img src={StarSVG} alt="Languages" />
                    </h1>
                    <div class="flex space-x-8 animate-scroll">
                        <img src={GitSVG} alt="Git" class="w-16 h-16" />
                        <img src={SvelteSVG} alt="Svelte" class="w-16 h-16" />
                        <img src={VimSVG} alt="Svelte" class="w-16 h-16" />
                    </div>
                </div>

                <div class="flex items-center space-x-8 mt-4">
                    <h1
                        class="flex items-center space-x-2 h-16 text-gray-900 dark:text-white"
                    >
                        3<img src={StarSVG} alt="Languages" />
                    </h1>
                    <div class="flex space-x-8 animate-scroll">
                        <img
                            src={JavaScriptSVG}
                            alt="JavaScript"
                            class="w-16 h-16"
                        />
                        <img src={ArchSVG} alt="Arch" class="w-16 h-16" />
                        <img src={GoSVG} alt="Go" class="w-16 h-16" />
                    </div>
                </div>

                <div class="flex items-center space-x-8 mt-4">
                    <h1
                        class="flex items-center space-x-2 h-16 text-gray-900 dark:text-white"
                    >
                        2<img src={StarSVG} alt="Languages" />
                    </h1>
                    <div class="flex space-x-8 animate-scroll">
                        <img src={MysqlSVG} alt="MySQL" class="w-16 h-16" />
                        <img src={JavaSVG} alt="Java" class="w-16 h-16" />
                        <img src={PhpSVG} alt="PHP" class="w-16 h-16" />
                    </div>
                </div>
            </div>
        </div>

        <Modal />
    </div>
    <img
        class="md:w-[70%] lg:w-[60%] h-auto rounded-lg shadow-xl dark:shadow-gray-400"
        src={Bild}
        alt="Amanuel, 19"
    />
</section>
