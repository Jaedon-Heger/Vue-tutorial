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
                label="Expense Name"
                hide-details="auto"
                class="expense-input"
            />
          </v-col>
          <v-col cols="12" md="5">
            <v-text-field
                label="Amount"
                hide-details="auto"
                class="expense-input"
                type="number"
            />
          </v-col>
          <v-col>
            <v-btn
                dark
                color="secondary"
                :disabled="addExpenseDisabled"
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
    <v-row class="noData" align-content="center">No Expenses</v-row>
    <v-row
        class="noData"
        align-content="center"
    >
      <v-col cols="2">{{  data.expenses[0].description }}</v-col>
      <v-col cols="2">{{  data.expenses[0].value }}</v-col>
      <v-col cols="2">
        <v-hover>
          <template v-slot:default="{ isHovering, props }">
            <v-icon
                v-bind="props"
                :color="isHovering ? 'red-accent-2' : 'default'"
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

// TODO 4: display row headers if there are expenses
// TODO 4: create a v-row if expenses length is greater and populate it with the first expense data

import {computed, reactive} from 'vue';

const data = reactive({
  totalIncome: 1000,
  addExpenseDisabled: false,
  expenseNameInput: null,
  expenseAmountInput: null,
  expenses: [
    {
      id: 1,
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

</script>

<style scoped>
.headers{
  font-size: 1.2rem;
  border-bottom: 2px solid white;
  padding-bottom: 0;
  margin-bottom: 10px;
  margin-top: 200px;
}

</style>
