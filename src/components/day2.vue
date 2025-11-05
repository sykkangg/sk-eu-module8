<script setup>
  import { ref, computed } from "vue";
  import UserCard from "../components/UserCard.vue";
  import ProductList from "../components/ProductList.vue";

  const currentName = ref("UserCard");
  const comps = { UserCard, ProductList };
  const currentComp = computed(() => comps[currentName.value]);

  // props
  import InputLabel from "../components/InputLabel.vue";
  import UserCard2 from "../components/UserCard2.vue";

  //emit
  import CounterButton from "../components/CounterButton.vue";

  const count = ref(0);
  function inc(n) {
    count.value += n;
  }

</script>



<template>
  <div class="container">
    <h1>동적 컴포넌트 연습</h1>

    <div class="tab-wrap">
      <button class="tab" :class="{active: currentName === 'UserCard'}"
      @click="currentName = 'UserCard'">UserCard</button>
      <button class="tab" :class="{active: currentName === 'ProductList'}"
      @click="currentName = 'ProductList'">ProductList</button>
    </div>

    <!-- App.vue -->
    <div>
      <!-- 핵심: 동적 컴포넌트 -->
      <keep-alive>
        <component :is="currentComp" class="panel" />
      </keep-alive>
    </div>
  </div>

  <!-- Props-->
  <div class="">
    <h1>defineProps 실습</h1>
    <section class="card">
      <h2>1) InputLabel-배열처리</h2>
      <InputLabel label="이름" placeholder="홍길동" />
      <InputLabel label="이메일" placeholder="user@example.com" />
    </section>

    <section class="card">
      <h2>2) UserCard -옵션처리(런타임 검증 + 기본값 + validator)</h2>
      <UserCard2 title="홍길동" :count="3" :is-active="true" size="md" />
      <UserCard2 title="임꺽정" size="lg" />
    </section>
  </div>

  <!-- emit -->
  <div class="">
    <h1>emit 실습</h1>

    <p class="count">
      현재 값: <strong>{{ count }}</strong>
    </p>

    <!-- 자식이 전달하는 add 이벤트를 듣고, count를 증가 -->
    <CounterButton @add="inc" />
  </div>

  <!-- form binding -->
</template>



<style>
/* 간단 전역 스타일 */
* {
  box-sizing: border-box;
}
body,
#app {
  margin: 0;
  font-family: system-ui, -apple-system, Segoe UI, Roboto, "Noto Sans KR",
    sans-serif;
}
.container {
  max-width: 720px;
  margin: 40px auto;
  padding: 0 16px;
}

h1 {
  font-size: 22px;
  margin: 0 0 16px;
}

.tabs {
  display: flex;
  gap: 8px;
  margin-bottom: 12px;
}
.tab {
  padding: 8px 12px;
  border: 1px solid #d1d5db;
  background: #f9fafb;
  border-radius: 8px;
  cursor: pointer;
}
.tab.active {
  background: #2563eb;
  color: #fff;
  border-color: #2563eb;
}
.tab:active {
  transform: translateY(1px);
}

.panel {
  border: 1px solid #e5e7eb;
  background: #fff;
  border-radius: 12px;
  padding: 16px;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.04);
}

/* Props */
</style>
