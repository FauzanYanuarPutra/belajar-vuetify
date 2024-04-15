<template>
  <div class="date w-50">
    {{ formattedDate }}

    <v-skeleton-loader v-if="!show" class="custom-skeleton" type="date-picker"></v-skeleton-loader>

    <v-date-picker v-else show-adjacent-months v-model="date" class="w-auto"></v-date-picker>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const date = ref(new Date());
const show = ref(false);


const formattedDate = computed(() => {
  const options = { year: 'numeric', month: 'long', day: 'numeric' };
  return date.value.toLocaleDateString('id-ID', options); 
});

setTimeout(() => {
  show.value = true;
}, 500)
</script>
