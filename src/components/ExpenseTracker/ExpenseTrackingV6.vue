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
    <v-row
        v-else
        class="noData"
        align-content="center"
    >
      <v-col cols="2">{{ data.expenses[0].description }}</v-col>
      <v-col cols="2">{{ data.expenses[0].value }}</v-col>
      <v-col cols="2">
        <v-hover>
          <template v-slot:default="{ isHovering, props }">
            <v-icon
                v-bind="props"
                :color="isHovering ? 'red-accent-2' : 'default'"
                @click="deleteExpense(data.expenses[0].id)"
            >
              mdi-delete
            </v-icon>
          </template>
        </v-hover>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup lang="ts">

// TODO 6: using v-for display all expenses in the expenses array

import {computed, reactive} from 'vue';

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
