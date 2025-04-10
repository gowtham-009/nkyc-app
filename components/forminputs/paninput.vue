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
      maxlength="10"
      inputmode="text"
      @keypress="allowAlphaNumeric"
      @input="enforceMaxLength"
    />
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';

const props = defineProps(['modelValue']);
const emit = defineEmits(['update:modelValue']);

const pan = ref(props.modelValue || '');

// Sync with parent
watch(pan, (newVal) => {
  emit('update:modelValue', newVal);
});

// Allow only alphanumeric characters
function allowAlphaNumeric(event) {
  const key = event.key;
  if (!/^[a-zA-Z0-9]$/.test(key)) {
    event.preventDefault();
  }
}

// Enforce max length manually for edge cases (like pasting)
function enforceMaxLength(event) {
  const value = event.target.value;
  if (value.length > 10) {
    pan.value = value.slice(0, 10);
  }
}
</script>
