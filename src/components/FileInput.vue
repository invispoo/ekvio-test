<template>
  <div class="file-input">
    <h4 role="heading">
      Label
    </h4>
    <div class="file-input__form">
      <div>
        <FileInputButton
            :button-text="fileButtonText"
            @file-selected="onFileSelect($event)"
            @cancel="isCancelled = true"
            @click="processClickFunc"
        />
      </div>
      <div class="file-input__file-info">
        <LoadingSpinner :loading="loading"/>
        <p :class="fileName ? 'file_input__file-name_loaded' : 'file_input__file-name'">
          {{ fileName ?? 'Файл не выбран' }}
        </p>
      </div>
    </div>
    <p
        id="hint"
        :class="isCancelled ? 'file-input__hint_cancelled' : 'file-input__hint'"
    >
      {{ isCancelled ? 'Error message' : 'Hint text' }}
    </p>
  </div>
</template>

<script setup lang="ts">
import FileInputButton from "./FileInputButton.vue";
import LoadingSpinner from "./LoadingSpinner.vue";
import { ref, watch } from "vue";

const timer = ref<number | null>(null);

const loading = ref<boolean>(false);

const processClickFunc = ref<(e: Event) => void | undefined>();

const fileName = ref<string | null>(null);

const fileButtonText = ref<string>('Выбрать файл');

const fileInputRef = ref();

const isCancelled = ref<boolean>(false);

watch([loading, fileName], () => {
  if (!loading.value && !fileName.value) {
    processClickFunc.value = undefined;
    fileButtonText.value = 'Выбрать файл';
  }
  else if (loading.value) {
    processClickFunc.value = onLoadCancel;
    fileButtonText.value = 'Отменить';
  }
  else {
    processClickFunc.value = onFileDelete;
    fileButtonText.value = 'Удалить';
  }
  isCancelled.value = false;
});

const onFileSelect = (inputRef: any) => {
  if (inputRef?.files[0]) {
    fileName.value = inputRef.files[0].name;
  }
  if (fileName.value) {
    loading.value = true;
    timer.value = setTimeout(() => {
      loading.value = false;
      fileInputRef.value = inputRef;
    }, 1000)
  }
};

const onFileDelete = (e: Event) => {
  e.preventDefault();
  fileInputRef.value.value = '';
  fileName.value = null;
};

const onLoadCancel = (e: Event) => {
  clearTimeout(timer.value as number);
  e.preventDefault();
  fileName.value = null;
  loading.value = false;
};
</script>

<style scoped>
.file-input {
  margin: 1em;
}

.file-input__form {
  display: flex;
  column-gap: 1.2em;
  margin: -0.5em 0;
}

.file-input__file-info {
  display: flex;
  align-items: center;
  column-gap: 0.5em;
}

.file-input__hint {
  font-weight: normal;
  color: #6B7280;
}

.file-input__hint_cancelled {
  font-weight: normal;
  color: #EF4848;
}

.file_input__file-name_loaded {
  color: #6B7280;
}

.file_input__file-name {
  color: #9BA2AF;
}
</style>