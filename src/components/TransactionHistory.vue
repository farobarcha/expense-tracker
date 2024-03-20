<template>
  <h3>Transactions</h3>
  <ul id="list" class="list" v-if="transactions.length">
    <li
      v-for="transaction in transactions"
      :key="transaction.id"
      :class="transaction.amount < 0 ? 'minus' : 'plus'"
    >
      {{ transaction.text }} <span>${{ transaction.amount }}</span>
      <button class="delete-btn" @click="$emit('removeTransaction', transaction.id)">x</button>
    </li>
  </ul>
  <p class="help-text" v-else>No transactions found</p>
</template>

<script setup>
defineProps({
  transactions: {
    type: Array,
    required: true,
    default: [],
  },
});
</script>
