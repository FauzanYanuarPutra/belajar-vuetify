<template>
  <div class="date">
    <v-date-picker show-adjacent-months v-model="date"></v-date-picker>
    {{ date }}
  </div>
</template>

<script setup>
import { ref } from 'vue';

const date = ref(new Date());
</script>
