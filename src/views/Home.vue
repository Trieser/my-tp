<template>
  <Transition name="blackhole-fade" mode="out-in">
    <Preloader v-if="isLoading" @done="onDone" />
    <section
      v-else
      key="main"
      class="min-h-screen bg-black text-white flex flex-col justify-center items-start px-6 md:px-24 font-sans"
    >
      <div class="max-w-3xl space-y-5">
        <p class="text-lg uppercase text-gray-400 tracking-wider">
          Creative Developer
        </p>
        <h1 class="text-4xl md:text-6xl font-bold leading-tight">
          Hello<br />
          <span class="text-indigo-400">Dmitrie</span>.<br />
        </h1>
        <p class="text-md md:text-lg text-gray-400 max-w-lg">
          Dedicated to crafting impactful digital experiences.
        </p>
        <div class="flex gap-4 pt-4">
          <a href="#projects" class="bg-white text-black px-6 py-2 rounded-full hover:bg-gray-200 transition font-medium">
            View Projects
          </a>
          <a href="mailto:kamu@email.com" class="border border-white px-6 py-2 rounded-full hover:bg-white hover:text-black transition font-medium">
            Contact Me
          </a>
        </div>
      </div>
    </section>
  </Transition>
</template>

<script setup>
import { ref } from 'vue'
import Preloader from '../components/Preloader.vue'

const isLoading = ref(true)

const onDone = () => {
  isLoading.value = false
}
</script>

<style scoped>
.blackhole-fade-enter-active,
.blackhole-fade-leave-active {
  transition: all 1s ease;
}
.blackhole-fade-enter-from {
  opacity: 0;
  filter: blur(30px);
  transform: scale(1.1);
}
.blackhole-fade-leave-to {
  opacity: 0;
  filter: blur(20px);
  transform: scale(0.8);
}
</style>
