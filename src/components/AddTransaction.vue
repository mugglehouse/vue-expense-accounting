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
  <h3>添加消费</h3>
  <!-- .prevent 阻止页面跳转 -->
  <form id="form" @submit.prevent="onSubmit">
    <!-- text -->
    <div class="form-control">
      <label for="text">类型</label>
      <input type="text" id="text" placeholder="输入文本" v-model="text" />
    </div>
    <!-- amount -->
    <div class="form-control">
      <label for="amount">金额（收入正数，支出负数）<br /> </label>
      <input type="text" id="amount" placeholder="输入金额" v-model="amount" />
    </div>
    <!-- summit -->
    <button class="btn">添加</button>
  </form>
</template>

<style>
</style>