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
  <div id="element" class="bg-white rounded-xl aspect-square w-[80vw] sm:w-[60vw] md:w-[40vw] lg:w-[24vw] flex flex-col px-6 py-8 gap-10">
    <div id="icon+text" class="flex flex-col gap-10">
      <slot name="icon"></slot>
      <div id="element-text" class="flex flex-col gap-2">
        <div class="text-xl">
          {{ title }}
        </div>
        <div class="text-xs">
          {{ description }}
        </div>
      </div>
    </div>

    <div class="text-[#1B5B31] text-sm underline flex flex-row items-center justify-start gap-2 mt-auto">
      <p>Dowiedz się więcej</p>
      <svg
          class="shrink-0"
          width="10"
          height="10"
          viewBox="0 0 16 16"
          fill="none"
          xmlns="http://www.w3.org/2000/svg">
        <path d="M7.99528 -1.20755e-06L7.09959 0.895696L13.5769 7.36358L-7.5502e-07 7.36358L-6.43745e-07 8.63642L13.5675 8.63642L7.09959 15.1043L7.99529 16L16 7.99529L7.99528 -1.20755e-06Z" fill="#1B5B31"/>
      </svg>
    </div>

  </div>
</template>

<style scoped>

</style>