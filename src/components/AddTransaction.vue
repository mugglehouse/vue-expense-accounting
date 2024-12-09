<script setup>
import { ref } from 'vue'

// 两个input的双向绑定
const text = ref('')
const amount = ref('')

// 子传父，触发事件
const emits = defineEmits(['transactionSumitted'])
function onSubmit() {
  emits('transactionSumitted', {
    id: Math.floor(Math.random() * 100000000),
    text: text.value,
    amount: parseFloat(amount.value),
  })
}
</script>

<template>
  <h3>AddTransaction</h3>
  <!-- .prevent 阻止页面跳转 -->
  <form id="form" @submit.prevent="onSubmit">
    <!-- text -->
    <div class="form-control">
      <label for="text">Text</label>
      <input type="text" id="text" placeholder="Enter text..." v-model="text" />
    </div>
    <!-- amount -->
    <div class="form-control">
      <label for="amount"
        >Amount <br />
        (negative - expense, positive - income)</label
      >
      <input type="text" id="amount" placeholder="Enter amount..." v-model="amount" />
    </div>
    <!-- summit -->
    <button class="btn">Add transaction</button>
  </form>
</template>

<style>
</style>