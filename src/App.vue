<template>
  <h2 class="main-heading">Expense Tracker</h2>
  <div class="container">
    <IncomePeriod
      :currentYear="currentYear"
      :currentMonth="currentMonth"
      @loadCurrentPeriod="handleLoadCurrentPeriod"
    />
    <Balance :totalBalance="totalBalance" />
    <IncomeExpense :income="income" :expenses="expenses" />
    <TransactionHistory
      :transactions="transactions[currentTimeStamp]"
      @removeTransaction="handleRemoveTransaction"
    />
    <TransactionForm @submitTransaction="handleSumbit" />
  </div>
</template>

<script setup>
import { ref, computed, onBeforeMount, watch } from "vue";
import { uid } from "uid";

import Balance from "./components/Balance.vue";
import IncomeExpense from "./components/IncomeExpense.vue";
import TransactionHistory from "./components/TransactionHistory.vue";
import TransactionForm from "./components/TransactionForm.vue";
import IncomePeriod from "./components/IncomePeriod.vue";

const transactions = ref([]);
// Create a new Date object
const currentDate = ref('');

// Get the current year
const currentYear = ref('');

// Get the current month (0-indexed, meaning January is 0)
const currentMonth = ref('');

const currentTimeStamp = ref('');

const setTransaction = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
  localStorage.setItem("currentTimeStamp", JSON.stringify(currentTimeStamp.value));
};

const fetchTransactions = () => {
  let localTransactions = localStorage.getItem("transactions");
  
  if (localTransactions) {
    transactions.value = JSON.parse(localTransactions);
  }
};

const fetchTimeStamp = () => {
  let timeStamp = localStorage.getItem("currentTimeStamp");

  if (timeStamp) {
    currentTimeStamp.value = JSON.parse(timeStamp);
  }

  if (!currentTimeStamp) {
    currentDate.value = new Date(new Date().getFullYear(), new Date().getMonth());
    currentYear.value = currentDate.value.getFullYear();
    currentMonth.value = currentDate.value.getMonth();
    currentTimeStamp = currentDate.value.getTime();
  } else {
    currentDate.value = new Date(currentTimeStamp.value);
    currentYear.value = currentDate.value.getFullYear();
    currentMonth.value = currentDate.value.getMonth();
  }
};

onBeforeMount(() => {
  fetchTimeStamp();
  fetchTransactions();
});

watch(
  [transactions, currentTimeStamp],
  () => {
    setTransaction();
  },
  {
    deep: true,
  }
);

const handleLoadCurrentPeriod = (timestamp) => {
  currentTimeStamp.value = timestamp;
  currentDate.value = new Date(timestamp);
};

const handleSumbit = (formData) => {
  if (transactions.value[currentTimeStamp.value] === undefined) {
    // If the index doesn't exist, initialize it with an empty array
    transactions.value[currentTimeStamp.value] = [];
  }

  // Push the new transaction object into the inner array
  transactions.value[currentTimeStamp.value].push({
    id: uid(),
    ...formData,
  });

  // Ensure reactivity by triggering the change detection
  transactions.value = { ...transactions.value };
};

const handleRemoveTransaction = (id) => {
  if (!transactions.value[currentTimeStamp.value]) {
    return;
  }

  transactions.value[currentTimeStamp.value] = transactions.value[currentTimeStamp.value].filter(
    (transaction) => transaction.id !== id
  );
};

const totalBalance = computed(() => {
  if (!transactions.value[currentTimeStamp.value]) {
    return;
  }

  return transactions.value[currentTimeStamp.value].reduce((accumulator, transaction) => {
    return accumulator + transaction.amount;
  }, 0);
});

const income = computed(() => {
  if (!transactions.value[currentTimeStamp.value]) {
    return;
  }

  return transactions.value[currentTimeStamp.value]
    .filter((transaction) => transaction.amount > 0)
    .reduce((accumulator, transaction) => accumulator + transaction.amount, 0)
    .toFixed(2);
});

const expenses = computed(() => {
  if (!transactions.value[currentTimeStamp.value]) {
    return;
  }

  return transactions.value[currentTimeStamp.value]
    .filter((transaction) => transaction.amount < 0)
    .reduce((accumulator, transaction) => accumulator + transaction.amount, 0)
    .toFixed(2);
});
</script>