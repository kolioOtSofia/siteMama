<template>
  <!-- <script src="../../node_modules/tw-elements/dist/js/index.min.js"></script> -->

  <section class="overflow-hidden text-gray-700">
    <div class="container px-5 py-2 mx-auto lg:pt-12 lg:px-32">
      <div class="flex flex-wrap -m-1 md:-m-2">
        <div
          v-for="project in refs.projects.value"
          class="flex relative flex-wrap w-1/3"
        >
          <div class="w-full p-1 md:p-2">
            <img
              @mouseover="show"
              @mouseleave="isHidden = true"
              alt="gallery"
              class="object-cover object-center w-full h-full rounded-lg relative transition ease-in-out delay-150 duration-500 hover:blur-sm"
              :src="project.imagesrc"
            />
          </div>
          <div
            v-if="!isHidden"
            class="absolute grid grid-rows-2 grid-flow-col line-up gap-2 flex w-full my-16 justify-center"
          >
            <div class="flex w-full justify-center">{{ project.title }}</div>
            <div class="flex w-full justify-center">
              {{ project.subtitleText }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, toRefs } from "vue";

const props = defineProps<{
  projects: Project[];
}>();

const refs = toRefs(props);

type Project = {
  imagesrc: string;
  title: string;
  subtitleText: string;
};

let isHidden = ref(true);
function show() {
  if (isHidden.value === true) isHidden.value = false;
}
</script>

<style>
.line-up {
  animation: 2s anim-line-up ease-out forwards;
}

@keyframes anim-line-up {
  0% {
    opacity: 0;
    transform: translateY(80%);
  }
  20% {
    opacity: 0;
  }
  50% {
    opacity: 1;
    transform: translateY(0%);
  }
  100% {
    opacity: 1;
    transform: translateY(0%);
  }
}
</style>
