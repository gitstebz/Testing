<template>
    <div class="button-container">
      <label class="button-label">
        <input
          type="checkbox"
          :value="modelValue"
          @input="() => $emit('update:modelValue', !modelValue)"
          class="hidden-checkbox"
        />
        <span class="button-text">{{ modelValue ? 'Completed!' : 'Mark as complete' }}</span>
      </label>
    </div>
  </template>
  
  <script setup>
  defineProps({
    modelValue: {
      type: Boolean,
      default: false,
    },
  });
  defineEmits(['update:modelValue']);
  </script>
  
  <style scoped>
   
  ::selection{
    display: none;
  }
  
  .button-label {
    display: inline-flex;
    align-items: center;
    padding: 10px 20px;
    background-color: #007bff;
    color: white;
    border-radius: 8px;
    cursor: pointer;
    font-family: Arial, sans-serif;
    font-size: 14px;
    transition: background-color 0.3s, transform 0.2s;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }
  
  .button-label:hover {
    background-color: #0056b3;
    transform: scale(1.05);
  }
  
  .button-label:active {
    transform: scale(0.95);
  }
  
  .hidden-checkbox {
    display: none;
  }
  
  .button-text {
    pointer-events: none;
  }
  </style>
  