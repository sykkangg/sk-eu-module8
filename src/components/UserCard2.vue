<template>
  <article class="card" :class="size">
    <div class="row">
      <img v-if="avatarUrl" :src="avatarUrl" alt="" class="avatar" />
      <div>
        <h3 class="title">{{ title }}</h3>
        <p class="sub">게시물 {{ count }}</p>
      </div>
      <span v-if="isActive" class="badge">ACTIVE</span>
    </div>
  </article>
</template>

<script setup>
import { defineProps } from "vue";
defineProps({
  title: { type: String, required: true },
  count: { type: Number, default: 0 },
  isActive: { type: Boolean, default: false },
  size: {
    type: String,
    default: "md",
    validator: (v) => ["sm", "md", "lg"].includes(v),
  },
});
</script>

<style scoped>
.card {
  padding: 12px;
  border: 1px solid #e5e7eb;
  border-radius: 10px;
}
.row {
  display: flex;
  align-items: center;
  gap: 12px;
  position: relative;
}
.avatar {
  width: 40px;
  height: 40px;
  border-radius: 999px;
  object-fit: cover;
  border: 1px solid #e5e7eb;
}
.title {
  margin: 0;
  font-size: 16px;
}
.sub {
  margin: 4px 0 0;
  color: #6b7280;
  font-size: 13px;
}
.badge {
  position: absolute;
  right: 0;
  top: 0;
  transform: translateY(-25%);
  font-size: 11px;
  padding: 2px 6px;
  border: 1px solid #9ca3af;
  border-radius: 999px;
}
.sm {
  font-size: 12px;
}
.md {
  font-size: 14px;
}
.lg {
  font-size: 16px;
}
</style>
