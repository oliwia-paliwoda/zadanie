<script setup lang="ts">
defineProps({
  title: {
    type: String,
    required: true
  },
  description: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div
      class=" bg-white rounded-xl shrink-0 aspect-square w-[clamp(280px,24vw,420px)] flex flex-col justify-between p-[clamp(1rem,2vw,2rem)]">

    <div class="flex flex-col gap-[clamp(1rem,2vw,2.5rem)]">

      <slot name="icon"></slot>

      <div class="flex flex-col gap-2">
        <h2>
          {{ title }}
        </h2>

        <h4>
          {{ description }}
        </h4>
      </div>

    </div>


    <div class="group cursor-pointer  text-[#1B5B31] underline flex items-center gap-2 text-[clamp(0.75rem,1vw,0.875rem)] active:text-black">
      <h4 class="transition-all duration-200 group-hover:font-bold">Dowiedz się więcej</h4>

      <svg class="shrink-0 transition-all duration-200 group-hover:scale-110 active:fill-black" width="10" height="10" viewBox="0 0 16 16" fill="none">
        <path
            d="M7.99528 -1.20755e-06L7.09959 0.895696L13.5769 7.36358L-7.5502e-07 7.36358L-6.43745e-07 8.63642L13.5675 8.63642L7.09959 15.1043L7.99529 16L16 7.99529L7.99528 -1.20755e-06Z"
            fill="currentColor"
        />
      </svg>
    </div>

  </div>
</template>

<style scoped>

</style>