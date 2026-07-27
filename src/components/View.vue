<script setup>
import {ref, onMounted, nextTick} from "vue";
import Masonry from "masonry-layout";
import OfertaElement from "./OfertaElement.vue";
import Gallery from "./Gallery.vue";


const grid = ref(null)
const ofertaOpen = ref(false);
const searchOpen = ref(false);
const mobileMenuOpen = ref(false);
const photoId = ref(null);

const images =[
  {id: 1, url: "/Photo_realizacje (1).png"},
    {id: 2, url: "/Photo_realizacje (2).png"},
    {id: 3, url: "/Photo_realizacje (3).png"},
    {id: 4, url: "/Photo_realizacje (5).png"},
    {id: 5, url: "/Photo_realizacje (6).png"},
    {id: 6, url: "/Photo_realizacje (7).png"},
    {id: 7, url: "/Photo_realizacje (8).png"},
    {id: 8, url: "/Photo_realizacje (9).png"},
    {id: 9, url: "/Photo_realizacje (10).png"},
    {id: 10, url: "/Photo_realizacje (11).png"},
    {id: 11, url: "/Photo_realizacje (12).png"},
    {id: 12, url: "/Photo_realizacje (13).png"},
    {id: 13, url: "/Photo_realizacje (14).png"},
    {id: 14, url: "/Photo_realizacje (15).png"},
    {id: 15, url: "/Photo_realizacje (16).png"},
    {id: 16, url: "/Photo_realizacje (17).png"},
    {id: 17, url: "/Photo_realizacje (18).png"},
]

const expanded = ref(false)

import imagesLoaded from "imagesloaded";

onMounted(async () => {
  await nextTick();

  imagesLoaded(grid.value, () => {
    new Masonry(grid.value, {
      itemSelector: ".grid-item",
      percentPosition: true,
      gutter: 0,
    });
  });
});
const gridHeight = ref(0)

const expandGrid = () => {
  expanded.value = !expanded.value

  if (expanded.value) {
    nextTick(() => {
      gridHeight.value = grid.value.offsetHeight
    })
  }
}


</script>

  <template>
    <Gallery v-if="photoId" :photo-id="photoId" @close="photoId = null"></Gallery>
    <div class="w-[full] min-h-screen overflow-y-auto flex flex-col">


      <!-----------------NAVI-------------------------->
    <div class="relative flex flex-row justify-between items-center bg-white h-[72px] py-6 px-4 sm:px-8 lg:px-12 w-[100%]">
      <img src="/giarddesign.png" class="w-[114.37px] h-[19px]">
      <button
          @click="mobileMenuOpen = !mobileMenuOpen"
          class="md:hidden flex flex-col gap-[5px]"
      >
        <span class="w-6 h-[2px] bg-[#111111]"></span>
        <span class="w-6 h-[2px] bg-[#111111]"></span>
        <span class="w-6 h-[2px] bg-[#111111]"></span>
      </button>
      <div class="hidden md:flex flex-row items-center gap-[48px]">
        <div class="relative">
          <div
              @click="ofertaOpen = !ofertaOpen"
              class="flex items-center justify-center gap-[2px] cursor-pointer"
          >
            <p class="text-[14px] font-normal leading-[-150%] tracking-[-0.01em] text-[#111111]">
              Oferta
            </p>
            <svg :class="{ 'rotate-180': ofertaOpen }"
                 class="transition-transform duration-200" width="12" height="12" viewBox="0 0 12 12" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path fill-rule="evenodd" clip-rule="evenodd" d="M2.13017 4.81427C1.95661 4.6407 1.95661 4.3593 2.13017 4.18573C2.28796 4.02794 2.53487 4.0136 2.70887 4.1427L2.75871 4.18573L6 7.42681L9.24129 4.18573C9.39907 4.02794 9.64599 4.0136 9.81998 4.1427L9.86983 4.18573C10.0276 4.34352 10.042 4.59043 9.91286 4.76442L9.86983 4.81427L6.31427 8.36983C6.15648 8.52761 5.90957 8.54196 5.73558 8.41286L5.68573 8.36983L2.13017 4.81427Z" fill="#111111"/>
            </svg>
          </div>

          <Transition name="dropdown">
            <div
                v-if="ofertaOpen"
                class="absolute top-full left-0 mt-2 w-[150px] rounded-md bg-white shadow-lg overflow-hidden"
            >
              <ul>
                <li class="px-4 py-2 cursor-pointer transition-colors duration-150 hover:bg-[#F5F5F5]">
                  Projekty
                </li>
                <li class="px-4 py-2 cursor-pointer transition-colors duration-150 hover:bg-[#F5F5F5]">
                  Wizualizacje
                </li>
                <li class="px-4 py-2 cursor-pointer transition-colors duration-150 hover:bg-[#F5F5F5]">
                  Realizacje
                </li>
              </ul>
            </div>
          </Transition>
        </div>

          <p class=" text-[14px] font-normal leading-[-150%] tracking-[-0.01em] text-[#111111]">O firmie</p>

          <p class=" text-[14px] font-normal leading-[-150%] tracking-[-0.01em] text-[#111111]">Realizacje</p>

          <p class=" text-[14px] font-normal leading-[-150%] tracking-[-0.01em] text-[#111111]">Kontakt</p>

        <Transition name="search">
          <input
              v-if="searchOpen"
              type="text"
              placeholder="Szukaj..."
              class="w-[220px] h-[36px] rounded-md border border-gray-300 px-3 text-sm bg-white"
          />
        </Transition>

          <svg @click="searchOpen =!searchOpen" width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path fill-rule="evenodd" clip-rule="evenodd" d="M10 2.25C5.71979 2.25 2.25 5.71979 2.25 10C2.25 14.2802 5.71979 17.75 10 17.75C11.87 17.75 13.5853 17.0877 14.9242 15.9848L20.4697 21.5303L20.5538 21.6029C20.8474 21.8208 21.2641 21.7966 21.5303 21.5303C21.8232 21.2374 21.8232 20.7626 21.5303 20.4697L15.9848 14.9242C17.0877 13.5853 17.75 11.87 17.75 10C17.75 5.71979 14.2802 2.25 10 2.25ZM10 3.75C13.4518 3.75 16.25 6.54822 16.25 10C16.25 13.4518 13.4518 16.25 10 16.25C6.54822 16.25 3.75 13.4518 3.75 10C3.75 6.54822 6.54822 3.75 10 3.75Z" fill="#111111"/>
      </svg>

      </div>

      <Transition name="dropdown">
        <div
            v-if="mobileMenuOpen"
            class="md:hidden absolute top-[72px] left-0 w-full bg-white shadow-lg"
        >
          <ul class="flex flex-col p-6 gap-6">
            <li><div @click="ofertaOpen =! ofertaOpen" class="flex flex-row items-center gap-2">
              <p>Oferta</p>
              <svg :class="{ 'rotate-180': ofertaOpen }"
                            class="transition-transform duration-200" width="12" height="12" viewBox="0 0 12 12" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path fill-rule="evenodd" clip-rule="evenodd" d="M2.13017 4.81427C1.95661 4.6407 1.95661 4.3593 2.13017 4.18573C2.28796 4.02794 2.53487 4.0136 2.70887 4.1427L2.75871 4.18573L6 7.42681L9.24129 4.18573C9.39907 4.02794 9.64599 4.0136 9.81998 4.1427L9.86983 4.18573C10.0276 4.34352 10.042 4.59043 9.91286 4.76442L9.86983 4.81427L6.31427 8.36983C6.15648 8.52761 5.90957 8.54196 5.73558 8.41286L5.68573 8.36983L2.13017 4.81427Z" fill="#111111"/>
            </svg>
            </div>
            </li>
            <li v-if="ofertaOpen" class="ml-4">Projekty</li>
            <li v-if="ofertaOpen" class="ml-4">Wizualizacje</li>
            <li v-if="ofertaOpen" class="ml-4">Realizacje</li>
            <li>O firmie</li>
            <li>Realizacje</li>
            <li>Kontakt</li>
            <li>
              <div class="flex items-center justify-between w-full gap-4">
              <input
                  type="text"
                  placeholder="Szukaj..."
                  class="w-[220px] h-[36px] rounded-md border border-gray-300 px-3 text-sm bg-white"
              />
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd" clip-rule="evenodd" d="M10 2.25C5.71979 2.25 2.25 5.71979 2.25 10C2.25 14.2802 5.71979 17.75 10 17.75C11.87 17.75 13.5853 17.0877 14.9242 15.9848L20.4697 21.5303L20.5538 21.6029C20.8474 21.8208 21.2641 21.7966 21.5303 21.5303C21.8232 21.2374 21.8232 20.7626 21.5303 20.4697L15.9848 14.9242C17.0877 13.5853 17.75 11.87 17.75 10C17.75 5.71979 14.2802 2.25 10 2.25ZM10 3.75C13.4518 3.75 16.25 6.54822 16.25 10C16.25 13.4518 13.4518 16.25 10 16.25C6.54822 16.25 3.75 13.4518 3.75 10C3.75 6.54822 6.54822 3.75 10 3.75Z" fill="#111111"/>
              </svg>
              </div>
            </li>
          </ul>
        </div>
      </Transition>

      </div>


      <!-----------------HERO-------------------------->
      <div id="hero" class="flex flex-row items-center justify-center bg-[#DCC1AB] w-[100%] px-12">
      <div id="hero-left" class = "flex h-auto w-[53%]">
        <div id="hero-text" class="h-[60%] w-[80%] flex flex-col gap-10">
          <div class="text-[#111111]">
            <h1>Nowoczesna aranżacja
            Twojego ogrodu</h1> </div>

          <div class="text-[#111111]">
            <h3>Marka GiardDesign to wieloletnie doświadczenie i wysoka estetyka realizacji. Oferujemy kompleksowy zakres usług z indywidualnym podejściem do każdego projektu.</h3>
          </div>

          <div id="buttons-row" class="flex flex-row items-center justify-start gap-6 text-sm">
          <div id="button" class="bg-[#1B5B31] text-white rounded-3xl pt-3 px-6 pb-[14px]">
            <p> Skontaktuj się z nami</p>
          </div>
            <div id="button" class="border-[1px] rounded-3xl pt-3 px-6 pb-[14px] flex flex-row gap-2 justify-center items-center text-[#1B5B31]">
              <p>Zobacz nasze realizacje</p>
              <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M15.9999 7.99529L15.1042 7.09959L8.63636 13.5769L8.63636 1.02988e-07L7.36352 8.78099e-08L7.36352 13.5675L0.895638 7.09959L-6.09397e-05 7.99529L8.00465 16L15.9999 7.99529Z" fill="#1B5B31"/>
              </svg>


            </div>

          </div>

        </div>
      </div>
        <img src="/Photo.png" class="w-[47%]">

      </div>


      <!-------------OFERTA------>
      <div id="oferta" class="flex flex-col items-center justify-center bg-[#F5F0EC] w-[100%] h-auto px-12 pt-[120px] pb-[160px] gap-[96px]">
        <div id="oferta-text" class="h-[60%] w-[80%] flex flex-col gap-10">

          <div class="font-[30px] text-[#1B5B31] text-sm">
            <p>Oferta</p>
          </div>

          <div class="text-[#111111]">
            <h1>Działamy <i>kompleksowo</i></h1> </div>

          <div class="text-[#111111]">
            <h3>Oferujemy kompletną obsługę inwestycji terenów zielonych. Projektujemy nowoczesne ogrody przydomowe oraz rezydencjonalne. Stworzymy dla Ciebie projekt, zwizualizujemy go i wcielimy w życie, a na każdym etapie posłużymy radą i wieloletnim doświadczeniem. </h3>
          </div>

            </div>

        <div id="oferta-elements" class="flex flex-col lg:flex-row items-center justify-center w-[100wv] gap-[64px]">

          <oferta-element title="Projekty" description="Zaprojektujemy Twój ogród w nowoczesnym stylu i z najlepszym wykorzystaniem istniejącej przestrzeni.">
            <template #icon>
              <svg width="44" height="44" viewBox="0 0 44 44" fill="none" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                <rect x="2" y="2" width="40" height="40" fill="url(#pattern0_1_233)"/>
                <defs>
                  <pattern id="pattern0_1_233" patternContentUnits="objectBoundingBox" width="1" height="1">
                    <use xlink:href="#image0_1_233" transform="translate(0 -0.00130548) scale(0.00261097)"/>
                  </pattern>
                  <image id="image0_1_233" width="383" height="384" preserveAspectRatio="none" xlink:href="data:image/png;base64,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"/>
                </defs>
              </svg>
            </template>
          </oferta-element>


          <oferta-element title="Wizualizacje" description="Przedstawimy Ci projekty koncepcyjne  w postaci wirtualnego spaceru animowanego w technologii 3D.">
          <template #icon>
            <svg width="49" height="44" viewBox="0 0 49 44" fill="none" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
              <rect x="0.333374" y="8" width="48" height="28.96" fill="url(#pattern0_1_241)"/>
              <defs>
                <pattern id="pattern0_1_241" patternContentUnits="objectBoundingBox" width="1" height="1">
                  <use xlink:href="#image0_1_241" transform="scale(0.00333333 0.00552486)"/>
                </pattern>
                <image id="image0_1_241" width="300" height="181" preserveAspectRatio="none" xlink:href="data:image/png;base64,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"/>
              </defs>
            </svg>
          </template>
        </oferta-element>

          <oferta-element title="Realizacje" description="Zrealizujemy Twoje marzenie przy użyciu najnowszych rozwiązań i zaawansowanych technologii.">
            <template #icon>
              <svg width="44" height="44" viewBox="0 0 44 44" fill="none" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                <rect width="44" height="44" fill="url(#pattern0_1_250)"/>
                <defs>
                  <pattern id="pattern0_1_250" patternContentUnits="objectBoundingBox" width="1" height="1">
                    <use xlink:href="#image0_1_250" transform="scale(0.00195312)"/>
                  </pattern>
                  <image id="image0_1_250" width="512" height="512" preserveAspectRatio="none" xlink:href="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAgAAAAIACAYAAAD0eNT6AAAACXBIWXMAAA7DAAAOwwHHb6hkAAAAGXRFWHRTb2Z0d2FyZQB3d3cuaW5rc2NhcGUub3Jnm+48GgAAIABJREFUeJzt3XvUXXV95/H3kzy5cgmQQAIMJCFGEExQvHFHAQVUlKpAFcF2dKC208JomdoZR7FeinhZ2s5C1K7OqowzglWsloKijiggIBFDBINCiKBcQhIICbmRy/zxOynhIXme55yz9/7uvX/v11qfFWABv+/ZZ5/z+559+W2QJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSJElFGoguQKNyInB2wLg3Av8nYFxJUskGowvQqBwBnB8w7gA2AJLUSmOiC9CojM9sXElSyWwAmmFC0Lg2AJLUUjYAzRA1EUc1HpKkktkANEPURGwDIEktZQPQDHsEjTslaFxJUslsAJphWmbjSpJKZgPQDFMzG1eSVDIbgGaI+iW+F+4jktRKfrk3Q1QDMJa46w8kSSWyAai/CcROwvsGji1JKokNQP3NJPZ9mhk4tiSpJDYA9TcrePzZweNLkkpgA1B/0RPwrODxJUklsAGoPxsASVLhbADq76Dg8ecEjy9JUpYWA1sDsx4YLP1VSpKkfzcJ2ERsA7AVOLTsFypJqpanAOrtUNJiPNHmRxcgSSqWDUC91WXinRddgCSpWDYA9VaXiffw6AIkScrJrcSf/98KLAcGSn6tkiSJdAHgBuIn/205pNyXK0mqkqcA6uuVwPjoIrZzTHQBkqTi2ADU17HRBQxhAyBJLWIDUF9HRxcwhA2AJEklGw+sJv68/9DMLPNFS5Kq4xGAejoe2DW6iB04NboASVIxbADqqa4T7WnRBUiS1GZ3E3+4f0dZA0wo8XVLkpStmcRP9MPlpPJeuiSpKp4CqJ+3RhcwgrrXJ0lSI91G/K/84bIMGCzt1UuSlKEDgS3ET/KeBpCklvMUQL28nWY8dOfs6AIkSWqTBcT/uh9NllOv5xRIktRY84mf2LvJ28rZDJKkKngKoD4uiC6gS/8pugBJUu+acL45B5OA3wN7RhfSha3AXOD+6EKkFtgaNK5zQMY8AlAPZ9GsyR/SF8cfRxchSVKT3UL8Of1e8jBeDCgVIeozrIx5BCDeMcBR0UX0aF/SrYuSJKlL1xD/S76fLMLziFK/PAIgZWYusJn4SbzfnFL0hpEyYwOgynkKINb7acd78P7oAiRJaor9gLXE/3ovIluAVxS7eaSseARAlWvDr8+m+u+k+//bYAD4m+giJEmquwOB9cT/ci86xxe5kaSMeARAysSXiZ+sy8iPi9xIUkZsAKQMvADYSPxkXVZOKm5TSdmwAZAy8C3iJ+ky80tgsLCtJeXBBkBquROJn6CrSNOebChFswGQWmwscBfxk3MVWQbsUcxmk7JgA6DKeRtgdS4A5kUXUZG9gf8RXYQkSdGmAyuI/2VeZTYC84vYeFIGPAIgtdTXiJ+QI3I76dSHpOHZAEgt9HriJ+LI/Jf+N6HUejYAqpyPcS3XbsDdwAHRhQRaS7r2YUl0IVKNRU3GzgEZ8yLAcl1G3pM/wGTgi7ivSZIycRrpKXnRh+Drkvf1tzmlVvMUgNQS+wCPEj/p1inrgZf0s1GlFrMBkFpgALiW+Am3jrmb9jwCWSqSDYDUAu8nfqKtc77Q+6aVWssGQGq4o2n3k/6Kyh/3uoGllrIBkBpsBvAw8ZNrE7IOeFlvm1lqJRsAqaHGAT8hfmJtUpYC03rY1lIb2QBIDfUF4ifUJuZ6YLCH7S21jQ2A1EB/SfxE2uR8uftNLrWODYDUMKcDm4ifRJuei7vd8JIkRXk5sIb4ybMN2QK8o7vNL0lS9Q4GlhE/cbYp64ATunkTJEmq0gGkK9ijJ8w2Zg1w7KjfCUmSKjIdWEz8RNnmPAkcMdo3RJKksk0jrWUfPUHmkGXAoaN7WyRJKs90YCHxE2NOeRSYP5o3R5KkMhwI/Jr4CTHHrAReNfJbJElSsWYD9xM/Eeac1cBrRnqjJEkqyuHAI8RPgCbdHXDq8G+XJEn9ey2wiviJzzybTcCfDvemSZLUj3cDG4mf8MyO83lgzE7fPUmSujQGuJT4Cc6MnK8BE3f8NkqSNHq7A9cQP7GZ0edO0kWakiT15HDgPuInNNN9lgOnPP8tlSRpeOcCTxM/kZneswn4a2AASZJGsBvwReInL1NcbgD2Q5KknXgFruzX1jwOvAlJkrYzFvgg8AzxE5UpL1uAy4HJSJKyNw+4jfjJyVSXJaQFnSRJGZoIXAJsIH5CMjG5mvQoZ0lSJk7Cc/0m5RHgD5EktdoBwFeIn3RM/XIbcCSSpFbZhXS4fx3xE42pb7aQGsQZSJIabQLw5/joXtNdVpEaxilIkhplHHAecD/xk4lpblaQGoHdkSTV2gTgPaTbvKInD9OeLAMuxkZAkmpnd+BC4HfETxamvXkK+DxwIJKkUAeTvpDXED85mHyyEbiStHS0JLVOXZ+gNoG0pvv5pPv561qn8vAr4J+AfyBdMyBp5z4EXBQw7qXAZQHjqgADpHu0/w5YSfwvQGOGZi2pEXgt6dkSkp7vs8R8Pj9WxYtrk8HoAoDDgDOBc4AXBNciDWcS6c6T80hN6rXA14HrgE2BdUl1MiFo3PFB4zZWRAMwCTgBOA14AzAnoAapX3sB53byCKkZuB74PmmNASlXUQ1A1LiNVUUDMBaYDxwPnEqa/CdVMK5UlX1Jt6a+h3Qk4BZSM3AjsID0MCopF7tlNm5jldEA7AUcARzTyZH4xigfg6Rm9/jO368H7gBu7mQB8HBMaVIlpmY2bmP10wDsDcwGXgjMI/3KnwfsX0BdUltMBI7tZJsVwEJgUSeLgQd4djlrqcmiHr/tY7+7NADsSWoEtv1K35V0McU0Uke1LdNIT9qb3ckuVRcrtdx6YGknD5FWJ1wBLO/8uYJ0OuGpzr+/dru/31xtqdJOPUiaK6p2L3BIwLiNNYC/OKSmO5S0VoEUbSzpiazjAsZ+mvQDVqM0JroASVJrHEDM5A/pqLSnAbpgAyBJKsrs4PFnBY/fKDYAkqSiRDcABwWP3yg2AJKkohwWPP6hweM3ig2AJKko84LHnx88fqPYAEiSihI9AR8ePH6j2ABIkoowvZNIs4EpwTU0hg2AJKkIx0QXwLOPldco2ABIkopQhwYA6lNH7dkASJKKcOzI/0olbABGyQZAktSv3YGXRhfRcSTpIVwagQ2AJKlfJxO3BPBQk4HjootoAhsASVK/To0uYIjTogtoAhsASVI/BrABaCQbAElSP15BegpgnRxC/LLEtWcDIEnqx9nRBezEWdEF1J0NgCSpVwPAW6OL2Im6Nia1YQMgSerVccDM6CJ24mDgiOgi6swGQJLUq/dEFzCCd0cXUGcDwNboIiT15VDgV9FFKDtTgIdJ993X1Spgf+Dp6ELqyCMAkqRevJN6T/6QmhQvBtwJGwBJUrcGgD+LLmKULiLVqyFsACRJ3Xoz8KLoIkZpPnBidBF1ZAMgSerW+6ML6FLT6q2EDYAkqRvHUJ9H/47WqdTnaYW1YQMgSerGR6ML6MEA8JHoIurGBkCSNFonAq+JLqJHpwNHRhdRJzYAkqTRGAA+Fl1En5p49KI0Y0gLJUhqpjXA5ugilIW3A0dFF9Gnk0lHAsTz742cQFrYYRwwtZNpnT/3Bv4DMAuY3fmz7otASE2xAfgtsLSTh4DHO1mxXdZ3/t21EUUqW5NIq03Wdd3/btxPelTwhuhCog0O+fsNPLtRlo3iv98HeCHpPstteTGwW1EFSi2zHrgbWATc1cli0pKqLsutuvoA7Zj8AeYAfwF8KrqQaGWsjjQAzAWOJt0qcjRwSEljSXW3FLgZuAW4CbgH2BRZkNSlFwILgYnRhRRoLTAPWBJdSKSqJuWppMdGngKcRns6SWmoZcB3geuAG0m/7KWmGgP8iPT93TY/JF0T4JG3ir0IeB/wA9Kvoa3GNDi3Ax8EXo531qhd/oT4z1eZObe4TdU8dTgsPxV4A3AmabWmodclSHV0D/B14KvAb4JrkcowB7iTdl/T9STwEtIFuAq2H+nIwD3Ed4bGDM1DpNXE5iK12yBwK/GfuSryY2BsMZtNRXkZ8EXSfc7RO4jJN5uBG0hHqDw6pVx8gvjPXpX5b8VsNhVtT9KTnB4kficx+WQF8HFgf6S8vJHU+EZ/BqvMJuB1RWw8lWMMaQWnXA5LmZgsAS4EdkHKzyxgOfGfw4g8RlrsTjV3Eum8TfQOY9qTRaTD/J4LVK52Id3vH/1ZjMyttGu9g1Y7lnSvdfROY5qbJcD5OPErb2OAa4j/PNYhV+HtvI1yOnauprssBd6FE78E8HfEfybrlI/3tzlVtTHAecCjxO88pr55GriE9HATSfCXxH8u65gL+tmoirEr6Qt+PfE7kKlPtgBXAwciaZs/In02oj+fdcxm4Jyet6xCHUxawzp6JzLxWQQciaTtvQ2XYh8pm4Czet3AijVAOi2wgvgdyVSfjcClwAQkbe/twDPEf0abkA3AH/S2mVUHM0jrtkfvSKa63AIciqShzsXJv9tsIl00rAY7E1hJ/M5kysszpGtAvLpfer734Tn/XrOZdMuwGmwmLiLU1iwmPUNC0nMNkBrj6M9oG/J5XCeg0QaBD+NhsDblCmAykoaaSFrcJvoz2qZ8HW8lbrzjgEeI35lM71lHupVJ0vPNAhYQ/zltY27Bh4U13v6kNzJ6ZzLd5zfAvOe/pZKA15AecBP9OW1zlpGeTaMGGyTdLha9M5nR51rSo6IlPddY0vl+7/GvJs8AF+N1AY33XrwuoAn5JH7YpB2ZiRc5R+WH+DjhxnsdsIr4nck8P5uAP9v5Wydl7Y+AJ4n/nOac5cDZI7xPqrl5wIPE70zm2awG3jjcmyZlajbwXeI/o+bZXIvPHWm0A4B7iN+RTHrC40uGf7uk7IwH/ivpCZfRn1Hz/KwC/oJ0jZkaaC/gduJ3pJzzMHDYSG+UlJmTgbuJ/3yakbMYeP2O30bV3R54m2BUlgJzRnyHpHy8EriB+M+m6T7/Chz+/LdUdbcbPlq46izGK2qlbV4MXI3r+Dc9W4DvYCPQOJOBG4nfgXLIfcB+o3tbpFY7ljTxbyb+c2mKy2ZSI3AyaozdgZ8Rv/O0OQ+RrmqWcjUReCdwB/GfR1N+biHdOjge1d4ewJ3E7zRtzGPAIaN/K6RWmUd60pyPLM8zy4BP43dg7c0gHaaO3mHalJWk85xSTmYCFwI3Ef8ZNPXJ3aTlnOdSooEy/+ctNwf4KbB3dCEt8AxwGvCD6EKkko0DjgZOJe3zXgym4WwFfg5cB1wP3Eq6fqAQNgD9OY50S86E6EIabCtpCdOvBNchlWES8HLSxXzHkL4zdg+tSE32BPAT4OZO7gA29Po/swHo31nA13Bb9upDwEeji5D6NIl08epBpIWr5pNOab2I9KtfKsNG0oq1izr5JfAAaQ2V9SP9x05axfgQ8JHoIhroSuC86CKkYQwCFwC7dv5+d2AXYGon00jLhs8IqU7auUdId1UtB1Z08jTpuSoAa2wAijEA/DPwluhCGmQh6Vzo2uhCpGFMwn1ULWUDUJzdgNtIh/w0vCdI50WXRBcijcAGQK01JrqAFllNOgLwVHQhNbcFOAcnf0kKZQNQrMXAe6OLqLmPkG5pkSQF8hRAOa4kLeWp57oZOIEC72OVSuYpALWWDUA5diUt3lDqKk4Nswp4Cen2FKkpbADUWp4CKMca0uI2m4LrqJP/jJO/JNWGDUB5bgH+NrqImrgK+N/RRUiSnuUpgHKNJ50KOCy6kEArgENJT7qSmsZTAGotjwCUayPwbvK+6O0inPwlqXZsAMp3G/CF6CKCXI+H/iWpljwFUI3dSA9pODC6kAqtIT0M5bfRhUh98BSAWssjANVYDVwcXUTFPoGTvyTVlkcAqnUjcHx0ERV4gHTh34iPo5RqziMAai2PAFTrItJa+G13MU7+klRrNgDVuhP4X9FFlOwm4JvRRUiShucpgOrtC9wHTI4upARbgVcAC6ILkQriKQC1lkcAqvcIcHl0ESW5Bid/SWoEjwDEmAYsId0e2BZbgCOAhdGFSAXyCIBayyMAMZYDfx9dRMGuxslfkhrDIwBx9iTdLjclupACbCYt+rM4uhCpYB4BUGt5BCDOE8AV0UUU5Bqc/CWpUTwCEGs/0lGA8dGF9Olo4KfRRUgl8AiAWssjALEeBv5vdBF9ugknf0lqHBuAeJ8m3T/fVJ+JLkCS1D0bgHi/BG6ILqJHS4BvRxchSeqeDUA9fCm6gB59mTyebSBJreNFgPUwCDxIWia4KTYBM0nXMUht5UWAai2PANTDJuDK6CK69G2c/CWpsTwCUB9zgN/QnPfkNOD66CKkko0D/ifpx9K2RbumAHsDUzvZJaY0aURrgBWdPA481fnnq4AtTZlscvFj4LjoIkbh98CBeP5fAtgLmNXJQcBhwPzOnxPCqlIu1gF3k5Ziv4d0cfbSTp4c7j8cLLkwdecqmtEAXI2Tv7TNyk5+PuSfDwIvIi2UdUznzznVlqYWupe09sq2NVjuJS3H3jWPANTLdNKv67HRhYzgKODW6CKkBpoOnAK8EXgd7XgWiMr1NPD/gO8A1wEPxZajMv2AtDBQXfMgNo5SEcYCJwNfIZ2Tjf5sm/rkCdJ+cTrNXypeXbiA+J1vuFxW3kuXsjUROAv4HulwbvTn3FSfTcC1wBl47Ui2plPvL4Cjy3vpkkgXEn6cdNV29OfdlJ9HgUuAA5CAO4jfKXeUldT/+gSpLSYA55Gu7I7+7Jvi82vgQtJiU9K/+yjxO+eO0vQnF0pNNAY4G/gV8d8Bpv8sBN6M11JpJ44hfifdUc4r80VLGtZY0mfwfuK/C0z3WUxq5FyBV8MaS1q5KXqH3T5baNazCqS2Gkc6dPwk8d8LZuSsBP4Kr+ZXF75B/I67fRaW+3IldWkG8I+k5jz6+8E8P5uBy0nLRUtdeR/xO/D2ubzclyupR8fh9QF1y6+BVw/znknDehXxO/H2OafclyupD5OAS0n3kkd/V+ScjaRb+jzcr76MIy0BGb1Db8usUl+tpCIcCdxH/PdFjllCuoBbKsSPiN+pt5KeTyCpGaaQbtmN/t7IKf8A7DqaN0carUuJ37G3At8s+4VKKtz5wAbivz/anHXAe0b7htSN9yPW26LoAjq8A0Bqni+RDkk/GF1ISz0EnED69S8Vbh7xHe5W4A/KfqGSSrMvsID475E25WZgWjdvgtStcdTjEN6csl+opFLtAnyb+O+SNuSfcf1+VWQhsTv7GjxVVHdR+4aaZSxwBfETaJPzGVzDXxX6KrE7/G3lv0T1KWrfUPMMAJ8ifiJtYi7tYXvXmr/s6u+B4PGXBI8vqThbgYuBD0QX0jAfooXbzAag/qIbgKXB40sq3ieBj0QX0RAfID2iXarcScQe9rqg/JeoPkXtG2q+uqw1Utd8uPdNK/XvIGI/AKeU/xLVp6h9Q803AHyB+Im2jvlUH9tVKsQ4Yh/wcXD5L1F9ito31A5jgGuIn3DrlKvwFLlq4jHiPghTKnh96o8NgPo1CbiV+Im3DvkJMLG/zdkMdjjNsCJo3GeAp4LGllSddaQVP38XXUiw+4EzgPXRhVTBBqAZlgeNuwJ/6Um5eAR4G2n10RytA84i7gdX5WwAmiFqh8zmgyAJSAt/XRRdRJD3Aj+PLqJKNgDNEHUEIGpcSXGuAK6MLqJilwP/FF1E1WwAmiHqPPzqoHElxfpT4DfRRVTkV6TVEbNjA9AMG4PGzfVcoJS7NcA5pAuB22wD8A5gbXQhEWwAmiFqIo5qPCTF+xktfADOEB8GfhFdRBQbgGbwCICkCB8D7okuoiQLgc9GFxHJBqAZPAIgKcJG4N3AluhCCraJ9LrafopjWIPRBWhUfkp6elfEuJLydivwJeBPogsp0OeABdFFRBuILkBS36IWa/L7Ix97Ab8GpkYXUoBlwAuBVdGFRPMUgCRpJCuBj0YXUZC/xslfUkv4MCBVYRzpnvnoh/X0k5/jD19JLWIDoKqcRfwk3k9eX/wmkaQ4NgCqygBwJ/ETeS+5uYTtIUmhbABUpTcRP5n3khPL2BiSFMkGQFX7BfETeje5vZzN0GxeDCFJ6tbnogvo0mXRBUhSGTwCoKqNAx4i/pf9aLIEGFvOZmg2jwBIkrr1DHBFdBGj9PfA5ugi6siVvKTmi/o17vdH3mYAD5KOBtTVBuAA4PHoQurIIwCSpF48ClwXXcQIvoGTvyRJhXsj8ef4h8urS3vlkiRlbBB4jPiJfkd5CE9TDctTAJKkXm0CvhVdxE5cjXerSJJUmpOI/7W/o7yyzBctSVLuxpIutIue8LfPg3j4f0SeApAk9WMz8L3oIoa4Dg//j8gGQJLUr7rdDli3eiRJaqVppCMB0Yf+twIbgSnlvtx28AiAJKlfy4FfRhfRcTuwKrqIJrABkCQV4aboAjpuji6gKWwAJElFqMvEe0t0AZIk5WQW8ef/twL7lPw6JUnSEMuJnfwfKv8ltoenACRJRYm+EHBh8PiNYgMgSSrKouDx7woev1FsACRJRYk+AnB38PiNYgMgSSrKA8HjLwkev1FsACRJRYluAJYGj98oPi1JklSU8cA6Yn5crgcm40OARs0jAJKkomwEHg0a+3c4+XfFBkCSVKQVQeMuDxq3sWwAJElFipqIbQC6ZAMgSSpS1BGAqHEbywZAklSkqEfxPhU0bmPZAEiSirQxaNwNQeM2lg2AJKlIURNxVOPRWDYAkqQi2QA0hAsBSZKKtBewR8C4K4EnA8aVJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmVG4guQAo2A3hTwLiPAf8SMK4kSQJeA2wNyG1VvDhJ2pkx0QVIwSZkNq4kATAYXUCXtgaN66mS9oqaiMcHjStJgEcApImZjStJgA2ANDVo3L2CxpUkwAZAimoApuBpAEmBbACUu6gGAGDPwLElZc4GQLmbFjj2PoFjS8qcDYByNztw7JmBY0vKnA2AchfZAMwKHFtS5mwAlLOJpKWAo8wKHFtS5mwAlLM5xC7yNDdwbEmZswFQzg4PHn9+8PiSMmYDoJzNCx5/JrBHcA2SMmUDoJxF/wIfAF4cXIOkTNkAKGdHRBcAvDy6AEl5sgFQruYSewfANsdEFyApTzYAytWx0QV01KUOSZmxAVCu6vLLewZwUHQRkvJjA6BcnRxdwHZeG12ApPzYAChHh1GvdfhPiy5ApdoaFGlYNgDKUd0m3JOBCdFFSMqLDYBy9IboAobYBTghughJebEBUG5mAMdFF7EDZ0UXICkvNgDKzZnA2OgiduAtwPjoIiTlwwZAuanrL+09qdedCZJazgZAOTmI+tz/vyPvii5AUj5sAJST80kP4KmrM4B9oouQlAcbAOViEDgvuogRjAfOjS5CUh5sAJSLM4B9o4sYhQvwcympAn7RKBfvjy5glOYCp0cXIUl145Ka6sVxxO07veTH5WwGBfF7S5KCfIv4Sb3bvKqULaEINgCSFGAesJn4Cb3bXFvGxlAIGwBJCvAd4ifzXlPHJYvVPRsASarYy4EtxE/kveb7xW8SBbABkKSK/Yj4Sbzf1O3RxeqeDYAkVegs4ifvIvIrYFzB20bVsgGQpIpMAh4gfvIuKhcWu3lUMRsASarIR4iftIvMSmBGoVtIVbIBkKQKHAKsJ37SLjpXF7mRVCkbAEkq2RjgJuIn67JyRnGbShWyAZCkkl1E/CRdZn4H7FXY1lJVbAAkqUSHAWuJn6TLzjeL2mCqjA2AJJVkArCQ+Mm5qvzHYjabKmIDIEkl+QLxk3KVWU262FHNYAMgSSV4J/ETckTuBaYUsP1UPhsASSrY4cDTxE/GUfkWMND3VlTZbAAkqUDTaddqf73mg/1uSJXOBkCSCjIJ+Cnxk28dsgU4t7/NqZLZAEhSAcaQboWLnnjrlA3Aif1sVEmS6mwAuIL4CbeOeRJ4We+bVpKk+rqM+Im2znkcOLTnrStJUg39DfETbBPye+AFPW5jSZJqpW2P9y07jwLzetrSkiTVwADwOeIn1CZmJfDK7je5JEmxJgBfJX4ibXKewLsDJEkNsifwI+In0DbkGeD8rra+JEkB5gKLiZ8425QtpOsoXDZYklRLbyCdu46eMNuaa0lHVyRJqoWxpNv8thA/SbY9v8Y7BCRJNXAAnu+vOuuAC/GUgCQpyFuBFcRPiLnmu8C+I75LkiQVZDrwFeInQJMaMO8SkCSV7kzSmvXRE595bv4NmDnM+yZJUk9eCtxI/ERndp6ngUuASTt+CyVJGr3pwJeBzcRPcGZ0eQB4G14kKEnqwV6kX5OriJ/QTG9ZSDplI0nSiPYm3dPvxN+e3AScgkcEJEk7cBDwedJ55OgJy5STe0nrB0xEkpS1ccBbSFeQe44/nzwMfAKYgyQpK0cAlwGPED8ZmbhsAb4PnAdMQVKjeE5PozGGdBvfGcDZpCf2SdvbAFwPfL3z54rYciSNxAZAO7M/cAJwKukCsH1iy1GDbAZ+BlxHOkKwgNQgSKoRGwAB7EF6QtzhwJHAsbgqnIqzHrgDuJnUDNwF3EdqFCQFsQFov0Fg6nbZF5i9XQ4BDgyrTrlaB9wD3E9aeOgB4EHSMtHLSacQVodVJ2XABqB9vga8rvPXuwDjA2uR+vUU6UjBRtL1JzfGliO1x2B0ASrcdGDP6CKkguy+3V9PDqtCaqEx0QVIkqTq2QBIkpQhGwBJkjJkAyBJUoZsACRJypANgCRJGbIBkCQpQzYAkiRlyAZAkqQM2QBIkpQhGwBJkjJkAyBJUoZsACRJypANgCRJGbIBkCQpQzYAkiRlyAZAkqQM2QBIkpQhGwBJkjI0GF2AJEk7sDVo3IGgcSvnEQBJkjJkAyBJUoZsACRJypANgCRJGbIBkCQpQzYAkiRlyAZAkqQM2QBIkpShbBY8yMijD7n3AAAFhUlEQVR+wERgN9JCT5OBqZ1MA/YFZgGzO3/uHlGkBGwGfg8s3S4rhmQLsAZ4BngUWFt9mQriQkAly+aFaqf2B+YBhwPzgaNIzYFUpHXAHZ0sAu4C7gbWRxalWrMBKFk2L1Rd2Rc4BjgeOBWYG1uOGmgdcCNwA3ALsID0K14aLRuAkmXzQtWXOcBpwBnAq4GxodWorh4BvglcC/yI1ARIvbIBKFk2L1SFmQ68FfhD4Fjch3K3ErgKuBr4MemcvVQEGwCpxuYClwKPkT6sJp/cAZxPushUKkPUvi2pC+OBdwJ3Ej8xmfKyFrgCOASpfFH7uaQenQx8j/jJyhSXFcCHgb2RqhO1v0vq01HA94mfvEzvWU06xbMHUvWi9ntJBTkZWEj8ZGZGnw3AZ0iLR0lRovZ/SQUaA5xHWsktenIzw+cG4LAdv41SpaI+A5JKsAfwRdKtYtETnXlulgKv3+k7J1Uv6rMgqUTHAvcQP+mZ1Ix9kfTsCKlObACklpoIfBaPBkRmCWnJZ6mObACkljsJ+B3xk2FuuRrYcxTvjxTFBkDKwDTgOuInxRyyBjhndG+LFMoGQMrEAPBXpGfER0+Sbc1vSI9+lprABkDKzOnAU8RPlm3Ltbigj5rFBkDK0IuB3xI/abYlXwYGu3oHpHg2AFKm9gMWED95NjlbgEu63O5SXdgASBnbFfgB8RNpE7MJeFf3m1yqDRsAKXOTge8SP6E2KRuAt/aysSVJqpMJwL8SP7E2IetxSV9JUouMB/6N+Am2ztkEnNnrBpYkqa4mAzcSP9HWMZuAd/S+aSVJqrcpwCLiJ9y65YJ+NqokSU2wP/AQ8ZNuXXJpf5tTkqTmOAJYTfzkG52rgTF9bktJkhrlzeT9OOFfkK6LkKSujY0uQOrDvaQJMMdn2j9BepTysuhCJEmKMJb8VgvcDJxaxMaTJKnJ9gEeJX5irip/W8xmkySp+U4jj+sBFpAWRZIkSR2XEz9Bl5mngUMK21qSJLXEZOB+4ifqsvK+4jaVJEntcirxE3UZuR3v2pEkaVhXEj9hF5lngJcWuoUkSWqhfYAniZ+4i8qni908kuQhRbXT06Sn470uupACPE56xO/66EIkSWqC8aSVAqN/vfeb84veMJIktd1biJ/A+8k9eJROkqSuDZCuno+eyHvNmcVvEkmS8vBG4ifyXnIXPuZXkqS+3Eb8hN5tzihlS0iSlJG3ET+hd5N78de/JEl9GwvcR/zEPtpcUM5mkCQpP39O/MQ+mjwOTCppG0iSlJ1dgdXET/Aj5ZNlbQBJknL1j8RP8MNlC/DC0l69JEmZOor4SX64/LC8ly5JUt7uIX6i31nOLfF1S9JzeKuRcnNVdAE7sR74l+giJElqq4OJ/6W/o3yjzBctSUN5BEC5uZe0zG7dfD26AEl5sQFQjr4dXcAQm4DroouQlBcbAOWobpPtzcCq6CIk5cUGQDm6DVgRXcR26taQSMqADYBytBn4QXQR2/ludAGS8mMDoFz9JLqAjqeARdFFSMqPDYBydXN0AR23kI5ISFKlbACUq7uox4V3dWlEJGXGBkC52gz8PLoI4PboAiTlyQZAOavDgkALowuQlCcbAOUs+uK7x4HHgmuQlCkbAOUs+gjAL4LHl5QxGwDlbHHw+PcGjy8pYzYAytlqYGXg+EsDx5aUORsA5e6BwLGXBo4tKXM2AMqdDYCkLNkAKHePBo79SODYkjJnA6DcRT4VMPL6A0mZswFQ7qIagDXA+qCxJckGQNmLagD89S8plA2Acrcus3ElCbABkDZkNq4kATYAUtREvDFoXEkCYDC6ACnYg8CXAsZdEjCmJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSJEmSpJL8fyNEPbKQxQNDAAAAAElFTkSuQmCC"/>
                </defs>
              </svg>
            </template>
          </oferta-element>

        </div>
        </div>

        <!---------O FIRMIE---->
      <div id="firma" class="relative flex bg-[#1B5B31] min-h-[500px]">

        <div class="w-[47%] relative">
          <img
              src="/Photo_o_firmie.png"
              class="absolute top-0 right-0 w-full h-full object-cover"
          >
        </div>

          <div id="firma-right" class = "flex h-auto w-[50%] py-20 pl-24 pr-10">
            <div id="firma-text" class="h-[60%] w-[100%] flex flex-col">

              <div class="text-white text-sm pb-2">
                <p>O firmie</p> </div>


              <div class="text-white pb-10">
                <h1>Tworzymy z pasją</h1> </div>

              <div class="text-white w-[100%] pb-9">
                <h4>Każdy projekt to nowe wyzwanie. Dlatego nasz zespół tworzą wykwalifikowani projektanci oraz architekci, których zadaniem jest rozpoznanie i realizacja potrzeb każdego Klienta. Nasza specjalizacja to przestrzenie nowoczesne, które charakteryzuje minimalizm, geometria i elegancka prostota. Tworzymy ogrody małoobsługowe, dostosowane do współczesnego trybu życia.</h4>
              </div>

              <div id="buttons-row" class="flex flex-row items-center justify-start gap-6 text-sm">
                <div id="button" class="border-[1px] rounded-3xl pt-3 px-6 pb-[14px] flex flex-row gap-2 justify-center items-center text-white">
                  <p>Poznaj nas bliżej</p>
                  <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M7.99528 -1.20755e-06L7.09959 0.895696L13.5769 7.36358L-7.5502e-07 7.36358L-6.43745e-07 8.63642L13.5675 8.63642L7.09959 15.1043L7.99529 16L16 7.99529L7.99528 -1.20755e-06Z" fill="#F5F0EC"/>
                  </svg>

                </div>

              </div>

            </div>
          </div>

          </div>


      <!-----REALIZACJE-->

      <div id="realizacje" class="relative bg-[#DCC1AB] w-full ">

        <div id="realizacje-text" class="flex flex-col items-start px-12 pt-[120px] pb-[96px] sm:px-[160px] gap-4">

          <div class="text-[14px] text-[#1B5B31]">
            <p>Realizacje</p>
          </div>

          <div class="text-black text-xl">
            <h1>Nasze <i>projekty</i></h1>
          </div>
        </div>

        <div
            class="relative overflow-hidden transition-all duration-500"
            :style="{
    height: expanded ? gridHeight + 'px' : '120vh'
  }"
        >
          <div ref="grid">
            <div
                v-for="image in images"
                :key="image.id"
                class="grid-item p-2"
            >
              <img
                  @click="photoId = image.id"
                  :src="image.url"
                  class="w-full"
              />
            </div>
          </div>

          <button @click = "expandGrid"
              class="absolute flex flex-row items-center gap-2 bottom-[10px] border-[1px] border-[black] left-1/2 -translate-y-1/1 -translate-x-1/2 bg-transprent pt-[12px] px-[22px] pb-[14px] rounded-3xl z-1"
          >
            {{ expanded ? 'Zwiń' : 'Rozwiń'}}
            <svg :class="expanded ? 'rotate-180' : 'rotate-0'" width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M16 7.99529L15.1043 7.09959L8.63642 13.5769L8.63642 1.02988e-07L7.36358 8.78099e-08L7.36358 13.5675L0.895699 7.09959L9.54553e-08 7.99529L8.00471 16L16 7.99529Z" fill="#111111"/>
            </svg>

          </button>
          </div>

        <div
            v-if="!expanded"
            class="absolute inset-0 bg-[linear-gradient(360deg,#DCC1AB_0%,rgba(214,183,158,0)_100%)]"
        ></div>

      </div>

      <!----------INSTAGRAM------------>
      <div id="insta" class="w-[100%] h-[auto] flex items-center justify-center px-10 py-12 bg-white">
        <div class="lg:w-[80%] h-[auto] bg-[#1B5B31] flex flex-col lg:flex-row lg:px-24 px-4 py-14 text-white text-xl text-center lg:text-left justify-between">
          <div id="text-area" class="flex flex-col text-xxl lg:py-26 py-16">
            <h1>Zostańmy w kontakcie!</h1>
            <h1>Znajdziesz nas na <b><i>Instagramie.</i></b></h1>
          </div>
          <div id="text-area-2" class=" gap-4 flex flex-col text-white lg:items-start items-center justify-center">
            <p>Śledź nasze najnowsze realizacje!</p>
            <button class="bg-white rounded-3xl text-center lg:self-start self-center text-black pt-[12px] px-[22px] pb-[14px]">Instagram</button>
          </div>
        </div>
      </div>

      <!------FOOTER------------>
      <div id="footer" class="flex flex-col items-center justify-center bg-black text-white  lg:px-36">
        <div id="footer-top" class=" w-full flex flex-col lg:flex-row justify-between items-center py-20 gap-4">
          <img src="/giarddesign_white.png" class="w-[114.37px] h-[19px]">
            <div class="flex flex-col lg:flex-row gap-4 items-center justify-center">
              <p>Daj znać, co możemy dla ciebie zrobić!</p>
              <button class="bg-[#1B5B31] rounded-3xl px-4 text-white pt-[12px] px-[22px] pb-[14px]">Skontaktuj się z nami</button>
            </div>
        </div>
        <div class="h-[1px] bg-[#F5F0EC] w-[80%] lg:w-full mx-10"></div>

        <div id="socials" class="flex flex-col lg:flex-row w-full items-center justify-between py-16 pb-[200px] gap-6">
      <div class="gap-6 flex flex-col text-center lg:text-start lg:flex-row">
        <p>Kontakt</p>
        <p>Instagram</p>
        <p>Facebook</p>
        <p>Linkedin</p>
      </div>


        <div class="gap-6 flex lg:text-start text-center flex-col lg:flex-row">
          <p>000-000-000</p>
          <p>giarddesign@kontakt.pl</p>
        </div>


      </div>

        <div id="footer-bottom" class="flex flex-col lg:flex-row w-full items-center lg:text-start text-center justify-between py-10">
          <div class="gap-6 flex flex-col lg:flex-row">
            <p>Prawa zastrzeżone © 2022</p>
          </div>


          <div class="gap-6 flex flex-row">
            <p>Made by</p>
            <img src="/logo-full-light.png">
          </div>


        </div>
      </div>






    </div>
  </template>

<style scoped>
.grid-item {
  width: 50%;
}

@media (min-width: 768px) {
  .grid-item {
    width: 33.333%;
  }
}

.dropdown-enter-active,
.dropdown-leave-active {
  transition: all 0.2s ease;
}

.dropdown-enter-from,
.dropdown-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

.dropdown-enter-to,
.dropdown-leave-from {
  opacity: 1;
  transform: translateY(0);
}

.search-enter-active,
.search-leave-active {
  transition: all 0.25s ease;
}

.search-enter-from,
.search-leave-to {
  opacity: 0;
  width: 0;
  transform: translateX(20px);
}

.search-enter-to,
.search-leave-from {
  opacity: 1;
  width: 220px;
  transform: translateX(0);
}
</style>

