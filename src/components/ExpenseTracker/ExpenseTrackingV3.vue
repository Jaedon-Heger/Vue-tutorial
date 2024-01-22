<template>
  <v-container>
    <v-row>
      <v-container class="gradiantBorderBottom gradiantBorderBottomFullWidth">
        <v-row>
          <h3 class="ml-3">Total Income: {{ data.totalExpense }}</h3>
        </v-row>
        <v-row>
          <h3 class="ml-3">Total Expense: {{ data.totalExpense }}</h3>
        </v-row>
        <v-row>
          <h3 class="ml-3">Total Left: {{ data.totalLeft }}</h3>
        </v-row>
        <v-row class="mb-1 mt-4" align="center">
          <v-col cols="12" md="5">
            <v-text-field
                v-model="data.expenseNameInput"
                label="Expense Name"
                hide-details="auto"
                class="expense-input"
            />
          </v-col>
          <v-col cols="12" md="5">
            <v-text-field
                v-model="data.expenseAmountInput"
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
                :disabled="data.addExpenseDisabled"
            >
              Add expense
            </v-btn>
          </v-col>
        </v-row>
      </v-container>
    </v-row>
  </v-container>
</template>

<script setup lang="ts">
import {reactive} from 'vue';

// Todo 3: migrate total expense to computed property
// Todo 3: migrate total left to computed property
// Todo 3: migrate addExpenseDisabled to computed property

const data = reactive({
  totalIncome: 1000,
  totalExpense: 0,
  totalLeft: 0,
  addExpenseDisabled: false,
  expenseNameInput: null,
  expenseAmountInput: null,
  expenses: [
    {
      name: 'Rent',
      value: '1000'
    }
  ]
});
</script>

<style scoped>
</style>
