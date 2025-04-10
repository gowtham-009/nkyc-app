<template>
  <div class="w-full">
    <label for="pan_label" class="text-gray-600 text-lg font-normal">PAN</label>
    <InputText
      id="pan_label"
      class="w-full py-2"
      v-model="pan"
      variant="filled"
      @keydown="onKeyDown"
      @input="onInput" 
      maxlength="10"
      size="large"
      placeholder="AGMLS6667Z"
    />
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';

const props = defineProps(['modelValue']);
const emit = defineEmits(['update:modelValue']);

const pan = ref(props.modelValue || '');

// ✅ Only allow alphanumeric keys and control keys (Backspace, Delete, Arrows, etc.)
const onKeyDown = (event) => {
  const key = event.key;

  const isAlphanumeric = /^[a-zA-Z0-9]$/.test(key);
  const isControlKey = [
    'Backspace', 'Delete', 'ArrowLeft', 'ArrowRight', 'Tab', 'Home', 'End'
  ].includes(key);

  if (!isAlphanumeric && !isControlKey) {
    event.preventDefault(); // Block special characters
    return;
  }

  // Block input if already 10 characters and not a control key
  if (isAlphanumeric && pan.value.length >= 10) {
    event.preventDefault();
  }
};

// ✅ Fallback cleanup for mobile (ensures input is clean if keydown misses)
const onInput = (event) => {
  const clean = event.target.value.toUpperCase().replace(/[^A-Z0-9]/g, '').slice(0, 10);
  pan.value = clean;
};

// Sync with v-model
watch(pan, (newVal) => {
  emit('update:modelValue', newVal);
});
</script>
