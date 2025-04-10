<template>
  <div class="w-full">
    <label for="pan_label" class="text-gray-600 text-lg font-normal">PAN</label>
    <InputText
      id="pan_label"
      class="w-full py-2"
      v-model="pan"
      variant="filled"
      @keydown="onKeydown"
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

// Allow only alphanumeric keys (A-Z, 0-9), allow control keys (backspace, arrows, etc.)
const onKeydown = (event) => {
  const key = event.key;

  const isControlKey = [
    'Backspace', 'Delete', 'ArrowLeft', 'ArrowRight', 'Tab', 'Home', 'End'
  ].includes(key);

  const isAlphanumeric = /^[a-zA-Z0-9]$/.test(key);

  if (!isAlphanumeric && !isControlKey) {
    event.preventDefault();
  }

  // Prevent entering more than 10 characters (unless it's a control key)
  if (isAlphanumeric && pan.value.length >= 10) {
    event.preventDefault();
  }
};

// Always sanitize input for mobile compatibility
const onInput = (event) => {
  const value = event.target.value.toUpperCase().replace(/[^A-Z0-9]/g, '').slice(0, 10);
  pan.value = value;
};

watch(pan, (newValue) => {
  emit('update:modelValue', newValue);
});
</script>
