<script setup>
const props = defineProps({
  total: {
    type: Number,
    required: true,
  },
})
</script>

<template>
  <h3>结余</h3>
  <h1 id="balance">${{ total }}</h1>
</template>

<style>
</style>