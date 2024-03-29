<template>
  <div
      class="max-w-full relative overflow-auto"
      :class="{'p-4 border rounded border-gray-medium': !readonly}"
      @dragover.prevent
      @drop.prevent="onDrop"
  >
    <FieldLabel
        :field="field"
        :show-name="showName"
        class="text-sm font-semibold"
    />
    <div
        v-if="!disable && !readonly"
        class="text-sm my-2"
    >
      <a
          class="text-blue-base"
          @click="$refs.file.click()"
      >Upload</a>
      <a
          v-if="uploadedFiles.length > 0"
          class="ml-3 text-red-dark"
          @click="onClear"
      >Clear</a>
      <input
          ref="file"
          class="hidden"
          type="file"
          multiple
          @change="onFilesSelected"
      />
    </div>

    <div class="max-w-[50em] flex items-stretch justify-start">
      <ImagePreview
          v-for="file in uploadedFiles"
          :key="'file-upload-' + file.id"
          class="w-32 m-2 cursor-pointer bg-neutral-plus-5"
          :class="{'border border-dashed border-blue-base': !uploadedFiles.length}"
          :image="file"
          :related-files="uploadedFiles"
          downloadable
          :removable="!readonly && !disable"
          @remove="onRemove(file)"
      />
      <ImagePreview
          v-if="!disable && !readonly"
          class="w-32 m-2 cursor-pointer border border-dashed border-blue-base"
          disabled
          @click="$refs.file.click()"
      />
      <div
          v-if="readonly && uploadedFiles.length === 0"
          class="p-1"
      >
        --
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted } from 'vue';
import { useMultiFileUpload } from '../../../../helpers';
import { ImagePreview } from '../../../Utility';
import FieldLabel from './FieldLabel';

const emit = defineEmits(['update:model-value']);
const props = defineProps({
  modelValue: {
    type: [Object, String],
    default: null
  },
  field: {
    type: Object,
    required: true
  },
  showName: Boolean,
  disable: Boolean,
  readonly: Boolean
});

const { onComplete, onDrop, onFilesSelected, uploadedFiles, onClear, onRemove } = useMultiFileUpload();
onMounted(() => {
  if (props.modelValue) {
    uploadedFiles.value = props.modelValue;
  }
});
onComplete(() => emit('update:model-value', uploadedFiles.value));
</script>
