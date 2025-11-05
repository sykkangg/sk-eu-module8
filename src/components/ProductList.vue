<template>
  <div class="card">
    <h2>상품 목록</h2>
    <ul class="list">
      <li v-for="product in products" :key="product">{{ product }}</li>
    </ul>
  </div>
</template>

<script setup>
import { reactive } from "vue";
const products = reactive(["책", "키보드", "마우스", "모니터"]);
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
.list {
  margin: 0;
  padding-left: 18px;
}
.list li {
  line-height: 1.8;
}
</style>
