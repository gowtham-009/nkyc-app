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
      @input="onInput"
      maxlength="10"
    />
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';

const props = defineProps(['modelValue']);
const emit = defineEmits(['update:modelValue']);

const pan = ref(props.modelValue || '');

// Emit changes to parent
watch(pan, (newVal) => {
  emit('update:modelValue', newVal);
});

// Handle input to restrict to alphanumeric and 10 characters
const onInput = (event) => {
  const value = event.target.value.toUpperCase().replace(/[^A-Z0-9]/g, '').slice(0, 10);
  pan.value = value;
};
</script>
