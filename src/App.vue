<script setup>
import { ref } from "vue";
import Intro from "./components/Intro.vue";
import New from "./components/New.vue";

const show_intro = ref(true);
const show_new = ref(false);

function mask_intro() {
  show_intro.value = false;
}

function start_new() {
  show_new.value = true;
}
</script>

<template>
  <div class="page-wrapper">
    <Intro v-if="show_intro" @finish_tl="start_new" @finish_animation="mask_intro"></Intro>
    <New v-if="show_new"></New>
  </div>
</template>

<style scoped>
.page-wrapper {
  width: 100vw;
  height: 100svh;
  overflow: hidden;
  position: relative;
}
</style>
