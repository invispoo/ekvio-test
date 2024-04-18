<template>
  <span
      v-if="loading"
      class="loading-spinner"
  />
</template>

<script setup lang="ts">
interface Props {
  loading: boolean;
}

defineProps<Props>();
</script>

<style scoped>
.loading-spinner {
  width: 1.2em;
  height: 1.2em;
  border: 2px solid #00A8A5;
  border-bottom-color: transparent;
  border-radius: 50%;
  display: inline-block;
  box-sizing: border-box;
  animation: rotation 1s linear infinite;
}

@keyframes rotation {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>