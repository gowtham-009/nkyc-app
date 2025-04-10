<template>
  <div class="w-full">
    <label for="pan_label" class="text-gray-600 text-lg font-normal">PAN</label>
    <InputText
      id="pan_label"
      class="w-full py-2"
      v-model="pan"
      variant="filled"
      size="large"
      placeholder="AGMLS6667Z"
      @keypress="handleKeyPress"
      @input="handleInput"
    />
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';

const props = defineProps(['modelValue']);
const emit = defineEmits(['update:modelValue']);

const pan = ref(props.modelValue || '');

// Restrict keypress to alphanumeric and max 10 characters
const handleKeyPress = (event) => {
  const char = event.key.toUpperCase();
  const isAlphanumeric = /^[A-Z0-9]$/.test(char);

  if (!isAlphanumeric || pan.value.length >= 10) {
    event.preventDefault(); // Block invalid character or length overflow
  }
};

// Convert input to uppercase (if pasted or autofill)
const handleInput = (event) => {
  let value = event.target.value.toUpperCase().replace(/[^A-Z0-9]/g, '');
  if (value.length > 10) value = value.slice(0, 10);
  pan.value = value;
};

// Sync with parent
watch(pan, (newVal) => {
  emit('update:modelValue', newVal);
});
</script>
