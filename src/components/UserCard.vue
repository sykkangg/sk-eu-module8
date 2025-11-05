<template>
  <div class="card">
    <h2>사용자 카드</h2>
    <p>
      카운터: <strong>{{ count }}</strong>
    </p>
    <button class="btn" @click="up">+</button>
  </div>
</template>

<script setup>
import { ref } from "vue";
const count = ref(0);

function up() {
  count.value = count.value + 1;
}
</script>

<style scoped>
.card {
  display: grid;
  gap: 8px;
}
h2 {
  font-size: 18px;
  margin: 0;
}
.btn {
  width: 64px;
  padding: 6px 0;
  border: 1px solid #d1d5db;
  border-radius: 8px;
  background: #f3f4f6;
  cursor: pointer;
}
.btn:hover {
  background: #e5e7eb;
}
</style>
