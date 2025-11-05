<script setup>
  import { defineProps } from 'vue';
  import EnrollItem from '../components/EnrollItem.vue'


  const props = defineProps({ items: { type: Array, required: true }});
  const emit = defineEmits(['remove'])
  console.log(props.items)
</script>

<template>

  <ul>
    <li v-for="it in items" :key="it.id" :item="it" @remove="$emit('remove', it.id)">
      {{ it.name }}
      {{ it.email }}
      {{ it.phoneNumber }}
      {{ it.age }}

    </li>
  </ul>

</template>