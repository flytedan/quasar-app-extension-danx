<template>
  <div>
    <div
        v-if="label"
        class="font-bold text-xs mb-2"
    >
      {{ label }}
    </div>
    <div class="flex items-center cursor-pointer">
      <DateIcon class="w-5 text-blue-base" />
      <div class="font-bold ml-3 hover:text-blue-base">
        <template v-if="date">
          {{ formattedDate }}
        </template>
        <template v-else>
          -&nbsp;-
        </template>
      </div>
    </div>
    <q-popup-proxy>
      <q-date
          v-model="date"
          @update:model-value="onSave"
      />
    </q-popup-proxy>
  </div>
</template>

<script setup>
import { CalendarIcon as DateIcon } from '@heroicons/vue/outline';
import { computed, ref, watch } from 'vue';
import { fDate, parseQDate } from '../../../../helpers';

const emit = defineEmits(['update:model-value']);
const props = defineProps({
  modelValue: {
    type: [String, Object],
    default: null
  },
  label: {
    type: String,
    default: null
  }
});

const formattedDate = computed(() => {
  if (props.modelValue) {
    return fDate(parseQDate(props.modelValue || '0000-00-00'));
  }
  return null;
});

const date = ref(props.modelValue);
watch(() => props.modelValue, val => date.value = val);

function onSave() {
  emit('update:model-value', date.value);
}
</script>
