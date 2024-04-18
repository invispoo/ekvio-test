<template>
  <div class="file-input">
    <h4 class="file-input__label">
      {{ labelText }}
    </h4>
    <div class="file-input__form">
      <div>
        <FileInputButton
            :button-text="buttonText"
            @file-selected="onFileSelect($event)"
            @cancel="onCancel"
        />
      </div>
      <div class="file-input__file-info">
        <LoadingSpinner :loading="loading"/>
        <span :class="fileName ? 'file_input__file-name_loaded' : 'file_input__file-name_init'">
          {{ fileName ?? 'Файл не выбран' }}
        </span>
      </div>
    </div>
    <h4 class="file-input__hint">
      {{ hintText }}
    </h4>
  </div>
</template>

<script setup lang="ts">
import FileInputButton from "./FileInputButton.vue";
import LoadingSpinner from "./LoadingSpinner.vue";
import {computed, ref} from "vue";

const fileName = ref<string | null>(null);

const loading = ref<boolean>(false);

const labelText = ref('Label');
const hintText = ref('Hint text');

const buttonText = computed(() => {
  if (loading.value) {
    return 'Отменить';
  }
  else if (!loading.value && fileName.value) {
    return 'Удалить';
  }
  else {
    return 'Выбрать файл';
  }
});

const onFileSelect = (e: Event) => {
  loading.value = true;
  setTimeout(() => {
    loading.value = false;
    fileName.value = (e.target as HTMLInputElement)!.files![0].name;
  }, 1000)
};

const onCancel = () => {

};
</script>

<style scoped>
.file-input {
  margin: 1em;
}

.file-input__form {
  display: flex;
  column-gap: 1.2em;
  margin: 1.5em 0;
}

.file-input__file-info {
  display: flex;
  align-content: center;
  column-gap: 0.5em;
}

.file-input__hint {
  font-weight: normal;
  color: #6B7280;
}

.file_input__file-name_loaded {
  color: #6B7280;
}

.file_input__file-name_init {
  color: #9BA2AF;
}
</style>