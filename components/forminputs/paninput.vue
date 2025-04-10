<template>
  <div class="w-full">
    <label for="pan_label" class="text-gray-600 text-lg font-normal">PAN</label>
    <InputText
      id="pan_label"
      class="w-full py-2"
      v-model="localPan"
      variant="filled"
      size="large"
      placeholder="AGMLS6667Z"
      :counter="16"
    />
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';

const props = defineProps({
  modelValue: String
});
const emit = defineEmits(['update:modelValue']);

const localPan = ref(props.modelValue || '');

// Format input and sync with parent
watch(localPan, (newVal) => {
  const formatted = newVal.toUpperCase().replace(/[^A-Z0-9]/g, '').slice(0, 16);
  if (formatted !== newVal) {
    localPan.value = formatted;
  }
  emit('update:modelValue', formatted);
});

// Watch for changes from parent and update local state
watch(() => props.modelValue, (newVal) => {
  if (newVal !== localPan.value) {
    localPan.value = newVal || '';
  }
});
</script>
