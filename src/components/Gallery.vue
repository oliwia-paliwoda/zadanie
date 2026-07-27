<script setup>
import { computed, ref } from "vue"


const emit = defineEmits([
  "close"
])

const closeGallery = () => {
  emit("close")
}

const props = defineProps({
  photoId: {
    type: Number,
    required: true,
  }
})

const touchStartX = ref(0)

const handleTouchStart = (event) => {
  touchStartX.value = event.touches[0].clientX
}

const handleTouchEnd = (event) => {
  const touchEndX = event.changedTouches[0].clientX

  const difference = touchStartX.value - touchEndX

  if (difference > 50) {
    nextImage()
  }

  if (difference < -50) {
    prevImage()
  }
}

const images = [
  {id: 1, url: "/zadanie/Photo_realizacje (1).png"},
  {id: 2, url: "/zadanie/Photo_realizacje (2).png"},
  {id: 3, url: "/zadanie/Photo_realizacje (3).png"},
  {id: 4, url: "/zadanie/Photo_realizacje (5).png"},
  {id: 5, url: "/zadanie/Photo_realizacje (6).png"},
  {id: 6, url: "/zadanie/Photo_realizacje (7).png"},
  {id: 7, url: "/zadanie/Photo_realizacje (8).png"},
  {id: 8, url: "/zadanie/Photo_realizacje (9).png"},
  {id: 9, url: "/zadanie/Photo_realizacje (10).png"},
  {id: 10, url: "/zadanie/Photo_realizacje (11).png"},
  {id: 11, url: "/zadanie/Photo_realizacje (12).png"},
  {id: 12, url: "/zadanie/Photo_realizacje (13).png"},
  {id: 13, url: "/zadanie/Photo_realizacje (14).png"},
  {id: 14, url: "/zadanie/Photo_realizacje (15).png"},
  {id: 15, url: "/zadanie/Photo_realizacje (16).png"},
  {id: 16, url: "/zadanie/Photo_realizacje (17).png"},
  {id: 17, url: "/zadanie/Photo_realizacje (18).png"},
]


const currentIndex = ref(
    images.findIndex(photo => photo.id === props.photoId)
)

const currentImage = computed(() => {
  return images[currentIndex.value]
})


const nextImage = () => {
  if (currentIndex.value < images.length - 1) {
    currentIndex.value++
  }
}


const prevImage = () => {
  if (currentIndex.value > 0) {
    currentIndex.value--
  }
}
</script>


<template>
  <div class="fixed inset-0 z-50 bg-black/80 flex items-center justify-center"  @touchstart="handleTouchStart"  @touchend="handleTouchEnd">

    <button class="absolute left-5 text-white text-5xl hidden sm:flex"  @click="prevImage">
      ‹
    </button>


    <img :src="currentImage.url" class="max-w-[90vw] max-h-[90vh] object-contain"/>


    <button class="absolute right-5 text-white  text-5xl hiddensm:flex" @click="nextImage">
      ›
    </button>

    <button class="absolute top-5 right-5 text-white text-4xl" @click="closeGallery"
    >
      ×
    </button>

    <div class="absolute bottom-8 left-1/2 -translate-x-1/2 text-white text-sm bg-black/40 flex items-center text-center px-4 py-2 rounded-full sm:hidden">
      Przesuń palcem, aby przewijać zdjęcia →
    </div>

  </div>
</template>