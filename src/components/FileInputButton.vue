<template>
  <label for="file-upload" class="input-button">
    {{ buttonText }}
  </label>
  <input
      type="file"
      id="file-upload"
      @change="emit('fileSelected', $event)"
      @cancel="emit('cancel')"
  />
</template>

<script setup lang="ts">

interface Props {
  buttonText: string;
}

defineProps<Props>();

const emit = defineEmits(['fileSelected', 'cancel']);
</script>

<style scoped>
input[type="file"] {
  display: none;
}

.input-button {
  padding: 0.8em 0.9em;
  background-color: white;
  color: #384252;
  border-radius: 0.8em;
  border: 1px solid #e5e7eb;
  cursor: pointer;
  box-shadow: 0 2px 7px -6px rgba(0,0,0,0.75);
  transition: background-color 0.4s;
}

.input-button:hover {
  background-color: #F3F4F6;
}

.input-button:active {
  background-color: #D0D5DC;
  box-shadow: none;
}
</style>
