<template>
    <label
        for="file-upload"
        class="file-input-button"
    >
      <input
          type="file"
          id="file-upload"
          ref="inputRef"
          @change="emit('fileSelected', inputRef)"
          @cancel="emit('cancel')"
          @click="emit('click', $event)"
      >
      <span
          role="button"

      >{{ buttonText }}</span>
    </label>

</template>

<script setup lang="ts">
import { ref } from "vue";

interface Props {
  buttonText: string;
}

defineProps<Props>();

const emit = defineEmits(['fileSelected', 'cancel', 'click']);

const inputRef = ref();
</script>

<style scoped>
.file-input-button input[type="file"] {
  position: absolute;
  z-index: -1;
  opacity: 0;
  display: block;
  width: 0;
  height: 0;
}

.file-input-button span{
  position: relative;
  display: inline-block;
  padding: 0.8em 0.9em;
  background-color: white;
  color: #384252;
  border-radius: 0.8em;
  border: 1px solid #e5e7eb;
  cursor: pointer;
  box-shadow: 0 2px 7px -6px rgba(0,0,0,0.75);
  transition: background-color 0.4s;
}

.file-input-button span:hover {
  background-color: #F3F4F6;
}

.file-input-button span:active {
  background-color: #D0D5DC;
  box-shadow: none;
}

.file-input-button input[type=file]:focus + span {
  outline: 2px solid #F0F1F2 !important;
}

.file-input-button input[type=file]:disabled + span {
  border-color: #E9EBED;
  color: #BCC0C9;
}
</style>
