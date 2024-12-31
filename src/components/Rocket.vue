<script setup>
import { ref } from "vue";
const main = ref();

defineExpose({
  main,
});
</script>

<template>
  <div class="rocket" ref="main">
    <img src="/rocket.png" alt="" />
  </div>
</template>

<style scoped>
.rocket {
  width: 200px;
  height: 200px;
}

.rocket img {
  object-fit: contain;
  height: inherit;
  width: inherit;
}
</style>
