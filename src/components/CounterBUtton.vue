<template>
  <button class="btn" @click="addOne">+1 증가</button>
</template>

<script setup>
import { defineEmits } from "vue";
const emit = defineEmits(["add"]); // 부모에게 'add' 이벤트 알림

function addOne() {
  emit("add", 1); // 페이로드로 1 전달
}
</script>

<style scoped>
.btn {
  padding: 8px 14px;
  border: none;
  border-radius: 8px;
  background: #4f8cff;
  color: white;
  cursor: pointer;
  font-weight: 600;
}
.btn:hover {
  opacity: 0.9;
}
</style>
