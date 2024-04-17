<template>
  <input type="file"/>
</template>

<script setup lang="ts">
interface Props {
  buttonText: string;
}

defineProps<Props>();
const emit = defineEmits(['clicked']);
</script>

<style scoped>

input::file-selector-button {
  background-color: white;
  color: #384252;
  padding: 0.8em 0.9em;
  border-radius: 0.8em;
  border: 1px solid #e5e7eb;
  cursor: pointer;
  box-shadow: 0 2px 7px -6px rgba(0,0,0,0.75);
  font-family: sans-serif;
  transition: background-color 0.4s;
}

.button:hover {
  background-color: #F3F4F6;
}

.button:active {
  background-color: #D0D5DC;
  box-shadow: none;
}

.button:focus {
  outline: 2px solid #F0F1F2 !important;
}
</style>
