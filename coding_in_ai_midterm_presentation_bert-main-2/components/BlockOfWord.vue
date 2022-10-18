<script setup lang="ts">
const final = {
  x: 0,
  y: 0,
  opacity: 1,
  transition: {
    type: 'spring',
    damping: 10,
    stiffness: 20,
    mass: 2
  }
}
</script>

<template>
  <span
    class="block-of-word"
    v-motion
    :initial="{y: 50, opacity: 0}"
    :enter="final"
  >
    <slot />
  </span>
</template>

<style scoped>
.block-of-word{
  display: inline-block;
  border: #222 2px solid;
  margin-right: 5px;
  padding: 2px;
}
</style>