<script setup>
const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
})
const emits = defineEmits(['transactionDeleted'])

const deleteTransaction = (id) => {
  emits('transactionDeleted', id)
}
</script>

<template>
  <h3>消费记录</h3>
  <ul id="list" class="list">
    <li
      v-for="transaction in transactions"
      :key="transaction.id"
      :class="transaction.amount < 0 ? 'minus' : 'plus'"
    >
      {{ transaction.text }} <span>${{ transaction.amount }}</span>
      <button @click="deleteTransaction(transaction.id)">X</button>
    </li>
  </ul>
</template>

<style>
</style>