<template>
  <label class="box">
    <span class="label">{{ label }}</span>
    <input class="input" :placeholder="placeholder" />
  </label>
</template>

<script setup>
import { defineProps } from "vue";
defineProps(["label", "placeholder"]);
</script>

<style scoped>
.box {
  display: flex;
  flex-direction: column;
  gap: 6px;
  margin: 8px 0;
}
.label {
  font-size: 14px;
  color: #374151;
}
.input {
  padding: 10px 12px;
  border: 1px solid #d1d5db;
  border-radius: 8px;
  outline: none;
}
.input:focus {
  border-color: #111827;
  box-shadow: 0 0 0 3px rgba(17, 24, 39, 0.1);
}
</style>
