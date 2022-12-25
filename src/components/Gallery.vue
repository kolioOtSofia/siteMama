<template>
  <!-- <script src="../../node_modules/tw-elements/dist/js/index.min.js"></script> -->

  <section class="overflow-hidden text-white">
    <div class="container py-2 mx-auto lg:pt-12 ">
      <div class="flex flex-wrap -m-1 md:-m-2">
        <div
          v-for="project in refs.projects.value"
          class="flex relative flex-wrap w-1/3"
        >
          <div class="w-full parent">
            <img
              @mouseover="show"
              @mouseleave="isHidden = true"
              alt="gallery"
              class="child object-cover object-center w-full h-full lg relative hover:grayscale"
              :src="project.imagesrc"
            />
          </div>
          <div
            v-if="!isHidden"
            class="absolute grid grid-rows-2 grid-flow-col line-up gap-2 flex w-full my-16 justify-center"
          >
            <div class="flex w-full justify-center text-white-700">{{ project.title }}</div>
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
    -webkit-transition: all .5s;
    -moz-transition: all .5s;
    -o-transition: all .5s;
    transition: all .5s;
}

.parent:hover .child, .parent:focus .child {
    -ms-transform: scale(1.2);
    -moz-transform: scale(1.2);
    -webkit-transform: scale(1.2);
    -o-transform: scale(1.2);
    transform: scale(1.2);
}

.parent:hover .child:before, .parent:focus .child:before {
    display: block;
}

.parent:hover a, .parent:focus a {
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
    background-color: rgba(52,73,94,0.75);
}

</style>
