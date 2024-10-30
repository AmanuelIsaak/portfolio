<script lang="ts">

import StarSVG from "../assets/star.svg"

let score = {
  first: "Grundkenntnisse, keine praktische Erfahrung",
  second: "Zusammenhänge, wenig praktische Erfahrung",
  third: "Theoretische Kenntnisse, praktische Erfahrungen",
  fourth: "Gute Kenntnisse, viel Erfahrung",
  fifth: "Experte, viel praktische Erfahrung",
}


function range(count: number) {
  return [...Array(count).keys()];
}

let isOpen = false; 
const toggleModal = () => {
  isOpen = !isOpen;
};
const closeModal = () => {
  isOpen = false;
};
</script>

<button on:click={toggleModal} class="w-[50%] mx-auto block text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm p-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800" type="button">
  Bewertungskriterien
</button>

<!-- Main modal -->
<div class={`backdrop-blur-sm overflow-hidden fixed top-0 right-0 left-0 z-50 justify-center items-center max-sm:w-auto w-full md:inset-0 h-[calc(100%-1rem)] max-h-full ${isOpen ? '' : 'hidden'}`}>
  <div class="relative p-4 w-full max-w-2xl max-h-full">
    <!-- Modal content -->
    <div class="relative bg-white rounded-lg shadow dark:bg-gray-700">
      <!-- Modal header -->
      <div class="flex items-center justify-between p-4 md:p-5 border-b rounded-t dark:border-gray-600">
        <h3 class="text-xl font-semibold text-gray-900 dark:text-white">
          Bewertungskriterien
        </h3>
        <button on:click={closeModal} type="button" class="text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm w-8 h-8 ms-auto inline-flex justify-center items-center dark:hover:bg-gray-600 dark:hover:text-white">
          <svg class="w-3 h-3" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 14 14">
            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m1 1 6 6m0 0 6 6M7 7l6-6M7 7l-6 6"/>
          </svg>
          <span class="sr-only">Close modal</span>
        </button>
      </div>
      <!-- Modal body -->
      <div class="p-4 md:p-5 space-y-4">
        <div class="relative overflow-x-auto">
          <table class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400">
            <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
              <tr>
                <th scope="col" class="px-6 py-3">
                  Anzahl Sterne
                </th>
                <th scope="col" class="px-6 py-3">
                  Genaue Beschreibung 
                </th>
              </tr>
            </thead>
            <tbody>
              <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                  {#each range(1) as index}
                    <img src={StarSVG} alt="">
                  {/each}
                </th>
                <td class="px-6 py-4 max-sm:text-end">
                  {@html score.first}
                </td>
              </tr>
              <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <th scope="row" class="flex px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                  {#each range(2) as index}
                    <img src={StarSVG} alt="">
                  {/each}
                </th>
                <td class="px-6 py-4 max-sm:text-end">
                  {@html score.second}
                </td>
             </tr>
              <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <th scope="row" class="flex px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                  {#each range(3) as index}
                    <img src={StarSVG} alt="">
                  {/each}
                </th>
                <td class="px-6 py-4 max-sm:text-end">
                  {@html score.third}
                </td>
              </tr>
              <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <th scope="row" class="flex px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                  {#each range(4) as index}
                    <img src={StarSVG} alt="">
                  {/each}
                </th>
                <td class="px-6 py-4 max-sm:text-end">
                  {@html score.fourth}
                </td>
              </tr>             
              <tr class="bg-white dark:bg-gray-800">
                <th scope="row" class="flex px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                  {#each range(5) as index}
                    <img src={StarSVG} alt="">
                  {/each}
                </th>
                <td class="px-6 py-4 max-sm:text-end">
                  {@html score.fifth}
                </td>
             </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</div>

