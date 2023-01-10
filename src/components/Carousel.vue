<template>
  <div class="relative w-full aspect-w-16 aspect-h-9" v-if="images.length === 1">
    <img :src="images[0].src" :alt="images[0].alt" class="z-10" />
  </div>
  <div class="relative w-full" v-else>
    <div class="aspect-w-16 aspect-h-9 w-full">
      <img :src="images[previousImageIndex].src" :alt="images[previousImageIndex].alt" class="z-10" />
      <HeadlessTransitionRoot appear :show="i === imageIndex" as="template" v-for="(image, i) in images">
        <HeadlessTransitionChild
          as="template"
          enter="duration-500 ease-out"
          enter-from="opacity-0"
          enter-to="opacity-100"
          leave="duration-500 ease-in"
          leave-from="opacity-100"
          leave-to="opacity-0"
        >
          <img class="absolute inset-0 z-20" :src="image.src" :alt="image.alt" />
        </HeadlessTransitionChild>
      </HeadlessTransitionRoot>
    </div>
    <div
      class="bottom-0 inset-x-0 flex items-end justify-between absolute z-30 bg-gradient-to-b from-[#00000000] via-[#00000020] to-[#00000065] p-2"
    >
      <div class="w-10"></div>
      <div class="flex gap-1">
        <button
          @click="() => manualNext(i - 1)"
          v-for="i in images.length"
          class="w-8 h-2 rounded-full"
          :class="{ 'bg-blue-600/80': i === imageIndex + 1, 'bg-neutral-700/80': i !== imageIndex + 1 }"
        ></button>
      </div>
      <button
        class="w-8 h-8 sm:w-9 sm:h-9 flex items-center justify-center bg-neutral-900/40 hover:bg-neutral-900/80 backdrop-blur rounded-full transition text-lg text-neutral-400 hover:text-white"
        @click="() => manualNext()"
      >
        <Icon name="mdi:arrow-right"></Icon>
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { debounce } from 'lodash'

const props = withDefaults(
  defineProps<{
    images: { src: string; alt: string }[]
    mode: 'manual' | 'auto'
    nextImageDelayMs?: number
  }>(),
  {
    nextImageDelayMs: 3000,
  }
)

const imageIndex = ref(0)
const interval = ref()
const previousImageIndex = computed(() => {
  if (imageIndex.value === 0) {
    return props.images.length - 1
  }
  return imageIndex.value - 1
})
const restartInterval = () => {
  console.log('restarting interval!')
  if (props.mode === 'auto') {
    interval.value = setInterval(() => {
      nextImage()
    }, props.nextImageDelayMs)
  }
}
const debouncedRestartInterval = debounce(restartInterval, 10000)
const nextImage = () => {
  imageIndex.value = (imageIndex.value + 1) % props.images.length
}
const manualNext = (idx?: number) => {
  if (interval.value) {
    clearInterval(interval.value)
  }
  if (idx == null) {
    imageIndex.value = (imageIndex.value + 1) % props.images.length
  } else {
    imageIndex.value = idx
  }
  debouncedRestartInterval()
}

onMounted(() => {
  if (props.mode === 'auto') {
    interval.value = setInterval(() => {
      nextImage()
    }, props.nextImageDelayMs)
  }
})
</script>
