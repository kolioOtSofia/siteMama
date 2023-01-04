<template>
  <!-- <script src="../../node_modules/tw-elements/dist/js/index.min.js"></script> -->

  <section class="overflow-hidden text-white">
    <div class="container py-2 mx-auto lg:pt-12">
      <div class="flex flex-wrap -m-1 md:-m-2" @mouseleave="hideEverything">
        <div
          v-for="(project, index) in refs.projects.value"
          class="flex relative flex-wrap w-1/3"
        >
          <div class="w-full parent" @mouseover="show(index)">
            <img
              alt="gallery"
              class="child object-cover object-center w-full h-full lg relative hover:grayscale"
              :src="project.imagesrc"
            />
          </div>
          <div
            class="absolute grid grid-rows-2 grid-flow-col line-up gap-2 w-full my-16 justify-center"
            :class="{ hide: isHiddenArray[index] }"
          >
            <p class="flex w-full justify-center text-white-700">
              {{ project.title }}
            </p>
            <p class="flex w-full justify-center">
              {{ project.subtitleText }}
            </p>
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

const isHiddenArray = ref(
  Array.from(Array(refs.projects.value.length), () => true)
);

type Project = {
  imagesrc: string;
  title: string;
  subtitleText: string;
};

function show(index: number) {
  const currentlyVisible = isHiddenArray.value.findIndex(
    (bool) => bool === false
  );
  if (currentlyVisible >= 0) isHiddenArray.value[currentlyVisible] = true;
  if (isHiddenArray.value[index] === true) isHiddenArray.value[index] = false;
}

function hideEverything() {
  for (let i = 0; i < isHiddenArray.value.length; i++) {
    isHiddenArray.value[i] = true;
  }
}
</script>

<style>
.hide {
  display: none;
}

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

.parent {
  overflow: hidden;
  position: relative;
  display: inline-block;
  cursor: pointer;
}

.child {
  height: 100%;
  width: 100%;
  background-size: cover;
  background-repeat: no-repeat;
  -webkit-transition: all 0.5s;
  -moz-transition: all 0.5s;
  -o-transition: all 0.5s;
  transition: all 0.5s;
}

.parent:hover .child,
.parent:focus .child {
  -ms-transform: scale(1.2);
  -moz-transform: scale(1.2);
  -webkit-transform: scale(1.2);
  -o-transform: scale(1.2);
  transform: scale(1.2);
}

.parent:hover .child:before,
.parent:focus .child:before {
  display: block;
}

.parent:hover a,
.parent:focus a {
  display: block;
}

.child:before {
  content: "";
  display: none;
  height: 100%;
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  background-color: rgba(52, 73, 94, 0.75);
}
</style>
