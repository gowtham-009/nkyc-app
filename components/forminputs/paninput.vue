<template>
  <div class="w-full">
    <label for="pan_label" class="text-gray-600 text-lg font-normal">PAN</label>
    <InputText
      id="pan_label"
      class="w-full py-2"
      v-model="pan"
      variant="filled"
      @input="formatInput"
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

// Format and sanitize input on all input events (works on mobile)
const formatInput = (event) => {
  let value = event.target.value.toUpperCase().replace(/[^A-Z0-9]/g, '').slice(0, 10);
  pan.value = value;
};

// Sync internal model with parent
watch(pan, (newValue) => {
  emit('update:modelValue', newValue);
});
</script>
