<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="addTransaction">
    <div class="form-control">
      <label for="text">Text</label>
      <input
        type="text"
        id="text"
        v-model.trim="text"
        placeholder="Enter text..."
      />
    </div>
    <div class="form-control">
      <label for="amount">Amount</label>
      <span class="small help-text">(negative - expense, positive - income)</span>
      <input
        type="number"
        id="amount"
        v-model.trim="amount"
        placeholder="Enter amount..."
      />
    </div>
    <p v-if="transactionError" class="error">{{ transactionError }}</p>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script setup>
import { ref, defineEmits } from "vue";
const emit = defineEmits("submitTransaction");
const text = ref("");
const amount = ref("");
const transactionError = ref("");

const addTransaction = () => {
  transactionError.value = "";
  if (text.value == "") {
    transactionError.value = "Please enter transaction text";
    return;
  }

  if (amount.value == "") {
    transactionError.value = "Please enter transaction value";
    return;
  }

  emit("submitTransaction", { text: text.value, amount: amount.value });
  text.value = amount.value = "";
};
</script>
