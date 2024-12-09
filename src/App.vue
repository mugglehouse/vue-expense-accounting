<script setup>
import Header from './components/Header.vue'
import Balance from './components/Balance.vue'
import IncomeExpenses from './components/IncomeExpenses.vue'
import TransactionList from './components/TransactionList.vue'
import AddTransaction from './components/AddTransaction.vue'

import { ref, computed, onMounted } from 'vue'

// 交易记录表
const transactions = ref([])

// 每次页面加载完成时，从localStorage中获取交易记录表
onMounted(() => {
  const transactionsFromLocalStorage = JSON.parse(localStorage.getItem('transactions')) || []
  transactions.value = transactionsFromLocalStorage
})

// 添加记录
function handlerTransactionSumitted(transaction) {
  transactions.value.push(transaction)
  // 每次交易记录表更新，都更新一次localStorage
  saveTransactionsToLocalStorage()
}
function saveTransactionsToLocalStorage() {
  localStorage.setItem('transactions', JSON.stringify(transactions.value))
}

// 删除记录
function handleTransactionDeleted(id) {
  transactions.value = transactions.value.filter((transaction) => transaction.id !== id)
}

// 计算收入和支出
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
    .toFixed(2) // 保留两位小数
})
const expense = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
    .toFixed(2) // 保留两位小数
})

// 计算总金额
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0)
})
</script>

<template>
  <Header />
  <div class="container">
    <Balance :total="total" />
    <IncomeExpenses :income="income" :expense="expense" />
    <TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted" />
    <AddTransaction @transactionSumitted="handlerTransactionSumitted" />
  </div>
</template>

<style scoped>
</style>
