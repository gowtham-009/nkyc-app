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

// ✅ Clean input: Uppercase, Alphanumeric only, max 10 chars
const onInput = (event) => {
  const raw = event.target.value;
  const cleaned = raw.toUpperCase().replace(/[^A-Z0-9]/g, '').slice(0, 10);
  pan.value = cleaned;
};

// Sync with parent
watch(pan, (newVal) => {
  emit('update:modelValue', newVal);
});
</script>
