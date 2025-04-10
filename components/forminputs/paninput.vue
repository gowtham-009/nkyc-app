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
      :maxlength="10"
      @keypress="onKeyPress"
      @input="onInput"
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

// Sync with parent when localPan changes
watch(localPan, (newVal) => {
  emit('update:modelValue', newVal);
});

// Sync from parent when modelValue changes
watch(() => props.modelValue, (newVal) => {
  if (newVal !== localPan.value) {
    localPan.value = newVal || '';
  }
});

// Allow only A-Z and 0-9 at keypress
const onKeyPress = (e) => {
  const char = e.key.toUpperCase();
  const isValid = /^[A-Z0-9]$/.test(char);
  if (!isValid || localPan.value.length >= 10) {
    e.preventDefault();
  }
};

// Just to ensure formatting on paste or autofill
const onInput = () => {
  localPan.value = localPan.value.toUpperCase().replace(/[^A-Z0-9]/g, '').slice(0, 10);
};
</script>
