<template>
  <v-container>
    <v-row>
      <v-container class="gradiantBorderBottom gradiantBorderBottomFullWidth">
        <v-row>
          <h3 class="ml-3">Total Income: {{ data.totalIncome }}</h3>
        </v-row>
        <v-row>
          <h3 class="ml-3">Total Expense: {{ totalExpense }}</h3>
        </v-row>
        <v-row>
          <h3 class="ml-3">Total Left: {{ totalLeft }}</h3>
        </v-row>
        <v-row class="mb-1 mt-4" align="center">
          <v-col cols="12" md="5">
            <v-text-field
                v-model="data.expenseNameInput"
                density="comfortable"
                label="Expense Name"
                hide-details="auto"
                class="expense-input"
            />
          </v-col>
          <v-col cols="12" md="5">
            <v-text-field
                v-model="data.expenseAmountInput"
                density="comfortable"
                label="Amount"
                hide-details="auto"
                class="expense-input"
                type="number"
                @keydown.enter="addExpense"
            />
          </v-col>
          <v-col>
            <v-btn
                dark
                color="deep-purple accent-1"
                :disabled="addExpenseDisabled"
                @click="addExpense"
            >
              Add expense
            </v-btn>
          </v-col>
        </v-row>
      </v-container>
    </v-row>
    <v-row class="headers">
      <v-col cols="2">Description</v-col>
      <v-col cols="2">Amount</v-col>
      <v-col cols="2">Actions</v-col>
    </v-row>
    <v-row
        v-if="data.expenses.length==0"
        class="noData"
        align-content="center"
    >
      No Expenses
    </v-row>

    <div v-else>
      <ExpenseRow
          v-for="expense in data.expenses"
          :key="expense.id"
          :expense="expense"
          @delete="deleteExpense"
      />
    </div>
  </v-container>
</template>

<script setup lang="ts">

// TODO 8: Add watchers to the expenseNameInput to alert when the length is above a certain amount of characters
// TODO 8: Add watchers to the expenseAmount to alert when the amount is larger than the total left
// TODO 8: If total left goes into negative display it as red

import {computed, reactive} from 'vue';
import ExpenseRow from "@/components/ExpenseTracker/ExpenseRow.vue";

const data = reactive({
  totalIncome: 1000,
  addExpenseDisabled: false,
  expenseNameInput: null,
  expenseAmountInput: null,
  expenses: [
    {
      id: 0,
      description: 'Rent',
      value: '1000'
    }
  ]
});

const totalExpense = computed(() => {
  return data.expenses.reduce((total, expense) => {
    return total + parseInt(expense.value);
  }, 0);
});

const totalLeft = computed(() => {
  return data.totalIncome - totalExpense.value;
});

const addExpenseDisabled = computed(() => {
  return !data.expenseNameInput || !data.expenseAmountInput;
});

const addExpense = () => {
  data.expenses.push({
    id: data.expenses.length,
    description: data.expenseNameInput,
    value: data.expenseAmountInput
  });
  data.expenseNameInput = null;
  data.expenseAmountInput = null;
}

const deleteExpense = (id) => {
  data.expenses = data.expenses.filter(expense => expense.id !== id);
}
</script>

<style scoped>
.headers{
  font-size: 1.2rem;
  border-bottom: 2px solid white;
  padding-bottom: 0px;
  margin-bottom: 10px;
}
</style>
