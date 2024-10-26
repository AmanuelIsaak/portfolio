<script>

let context = {
  curiosity: {
    short:
      "During the pandemic in 2021, while everyone was at home and computers were being purchased widely, I became curious about how computers work. My background in gaming also sparked my fascination with coding and software development.",
    long: "Before 2021 I was not really interested in computers or software. But at that time during the pandemic everyone was at home bored and computers were getting bought everywhere. I also was taking notice of the trend and got really curios on how computer really work. And since I used to game alot I also got fascinated by how the software or games were coded.",
  },
  firstStep: {
    short:
      "In 2021, I joined IMS to learn software engineering and built small projects like calculators and password generators, which felt like big achievements. In 2022, I enrolled in IMS, learning databases, HTML, and CSS. Though initially hesitant about JavaScript, I overcame that fear. Now, I aim to become a passionate software engineer with a deeper understanding to deliver valuable work.",
    long: "In 2021 I decided to enter <a class=\"font-medium text-blue-600 dark:text-blue-500 hover:underline\" href=\"https://wg.edubs.ch/schulprofil/ims\">IMS</a> in order to learn about software engineering. Meanwhile I did some research and wrote some 'toy-application' like calculators and password generators. Even though I was building something simple, it really felt like I've built something big and hard.Fast forward to 2022 and I was enrolled in IMS and there were just too many topics that we've learned about. Databases and building static websites with HTML and CSS. These were the main topics at that time. But suddenly I was scared to make some progress like start using Javascript. But it wasn't long before I overcame it.But nevertheless, I aspire to become a software engineer with passion and a deeper level of understanding in order to provide valuable work!",
  },
  whereDoIStandNow: {
    short: "I have a limited programming experience in Go and JavaScript. I've built some simple websites and apps but still feel like a beginner. I lack a deep understanding of software fundamentals, data structures, algorithms, and haven't developed a complex application that covers both frontend and backend, along with topics like security and networking.",
    long: "At this point I have some experience at programming in general. I mostly used Goland and Javascript, Svelte specifically, and in school we mostly used PHP and Java. I've build some silly websites but I also build some decent apps as well. But I still feel like a beginner since I have no deep understanding of how software actually works under the hood. I still don't know much about Data structures and Algorithms, I still haven't build a complex application to really cover frontend and backend and just other skills and topics like security, network, design pattern etc.",
  },
};
</script>

<ol class="relative border-s border-gray-200 dark:border-gray-700 md:w-[60%]">
  <li class="mb-10 ms-4">
    <div
      class="absolute w-3 h-3 bg-gray-200 rounded-full mt-1.5 -start-1.5 border border-white dark:border-gray-900 dark:bg-gray-700"
    ></div>
    <time
      class="mb-1 text-sm font-normal leading-none text-gray-400 dark:text-gray-500"
    >>=2021</time
    >
    <h3 class="text-lg font-semibold text-gray-900 dark:text-white">
      Curiosity
    </h3>
    <p class="text-base font-normal text-gray-500 dark:text-gray-400 block lg:hidden">{@html context.curiosity.short}</p>
    <p class="text-base font-normal text-gray-500 dark:text-gray-400 hidden lg:block">{@html context.curiosity.long}</p>
  </li>

  <li class="mb-10 ms-4">
    <div
      class="absolute w-3 h-3 bg-gray-200 rounded-full mt-1.5 -start-1.5 border border-white dark:border-gray-900 dark:bg-gray-700"
    ></div>
    <time
      class="mb-1 text-sm font-normal leading-none text-gray-400 dark:text-gray-500"
    >2021-2022</time
    >
    <h3 class="text-lg font-semibold text-gray-900 dark:text-white">
      First steps
    </h3>
    <p class="text-base font-normal text-gray-500 dark:text-gray-400 block lg:hidden">{@html context.firstStep.short}</p>
    <p class="text-base font-normal text-gray-500 dark:text-gray-400 hidden lg:block">{@html context.firstStep.long}</p>
  </li>
  <li class="ms-4">
    <div
      class="absolute w-3 h-3 bg-gray-200 rounded-full mt-1.5 -start-1.5 border border-white dark:border-gray-900 dark:bg-gray-700"
    ></div>
    <time
      class="mb-1 text-sm font-normal leading-none text-gray-400 dark:text-gray-500"
    >2022-now</time
    >
    <h3 class="text-lg font-semibold text-gray-900 dark:text-white">
      Where do I stand now?
    </h3>
    <p class="text-base font-normal text-gray-500 dark:text-gray-400 block lg:hidden">{@html context.whereDoIStandNow.short}</p>
    <p class="text-base font-normal text-gray-500 dark:text-gray-400 hidden lg:block">{@html context.whereDoIStandNow.long}</p>
  </li>
</ol>
