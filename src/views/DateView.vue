<template>
  <div class="date">
    <v-date-picker show-adjacent-months v-model="date"></v-date-picker>
    {{ formattedDate }}
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const date = ref(new Date());

const formattedDate = computed(() => {
  const options = { year: 'numeric', month: 'long', day: 'numeric' };
  return date.value.toLocaleDateString('id-ID', options); 
});
</script>
