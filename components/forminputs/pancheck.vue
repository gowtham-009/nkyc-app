<template>
    <fieldset>
      <legend class="sr-only">Notifications</legend>
      <div class="space-y-5">
        <div class="flex items-center gap-3">
          <div class="flex h-6 shrink-0 items-center">
            <div class="group grid size-6 grid-cols-1">
              <input 
                id="comments" 
                aria-describedby="comments-description" 
                name="comments" 
                type="checkbox" 
                :checked="false" 
                @change="$emit('update:modelValue', $event.target.checked)"
                class="col-start-1 row-start-1 appearance-none rounded border border-gray-300 bg-white checked:border-indigo-600 checked:bg-indigo-600 indeterminate:border-indigo-600 indeterminate:bg-indigo-600 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 disabled:border-gray-300 disabled:bg-gray-100 disabled:checked:bg-gray-100 forced-colors:appearance-auto"
              />
              <svg class="pointer-events-none col-start-1 row-start-1 size-3.5 self-center justify-self-center stroke-white group-has-[:disabled]:stroke-gray-950/25" viewBox="0 0 14 14" fill="none">
                <path class="opacity-0 group-has-[:checked]:opacity-100" d="M3 8L6 11L11 3.5" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                <path class="opacity-0 group-has-[:indeterminate]:opacity-100" d="M3 7H11" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
              </svg>
            </div>
          </div>
          <div class="text-sm/6">
            <label for="comments" class="text-gray-600 leading-4 text-md font-normal text-justify">
              I'm a tax resident of India and not paying taxes to any other jurisdiction(s)
            </label>
          </div>
        </div>
      </div>
    </fieldset>
  </template>
  
  <script setup>
  defineProps({
    modelValue: {
      type: Boolean,
      default: false, // Ensures the checkbox is initially unchecked
    },
  });
  
  defineEmits(['update:modelValue']);
  </script>
  