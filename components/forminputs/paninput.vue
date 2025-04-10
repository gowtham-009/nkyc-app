<template>
  <div class="w-full">
    <label for="pan_label" class="text-gray-600 text-lg font-normal">PAN</label>
    <InputText 
      v-model="pan" 
      @keypress="handleKeyPress"
      @input="convertToUppercase"
      maxlength="10" 
    />
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';

const props = defineProps(['modelValue']);
const emit = defineEmits(['update:modelValue']);

const pan = ref(props.modelValue || '');

// Convert input to uppercase
const convertToUppercase = () => {
  pan.value = pan.value.toUpperCase();
};

// Only allow alphanumeric characters
const handleKeyPress = (event) => {
  const charCode = event.charCode;
  // Allow only A-Z, a-z, 0-9
  if (!(charCode >= 48 && charCode <= 57) && // 0-9
      !(charCode >= 65 && charCode <= 90) && // A-Z
      !(charCode >= 97 && charCode <= 122)) { // a-z
    event.preventDefault();
  }
};

// Sync with parent
watch(pan, (newVal) => {
  emit('update:modelValue', newVal);
});
</script>