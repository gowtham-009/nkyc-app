<template>
  <div class="w-full">
    <label for="pan_label" class="text-gray-600 text-lg font-normal">PAN</label>
    <InputText
      id="pan_label"
      class="w-full py-2"
      v-model="pan"
      variant="filled"
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

// Handle input: allow only A-Z, 0-9 and max 10 characters
const onInput = (event) => {
  const rawValue = event.target.value.toUpperCase();
  const cleaned = rawValue.replace(/[^A-Z0-9]/g, '').slice(0, 10);
  pan.value = cleaned;
};

// Sync with v-model
watch(pan, (newVal) => {
  emit('update:modelValue', newVal);
});
</script>
