<script setup>
import { ref, computed } from 'vue';
const userName = ref('');
const quantity = ref(0);

const total = computed(()=>Number(quantity.value)*1000);
</script>

<template>
  <h2>v-model 수식자 실습</h2>
  <div>
    <h3>trim</h3>
    <label for="">이름</label>
    <input type="text" v-model.trim="userName"/>
    <p>{{ userName }}</p>
    
    <h3>number</h3>
    <label for="">수량</label>
    <input type="number" v-model.number="quantity" placeholder="숫자로 변환">
    <p>숫자로 변환 {{ quantity }} / 타입: {{ typeof quantity }}</p>
    <p>총계: {{ total.toLocaleString() }}</p>
  </div>
</template>