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
      <v-col>Description</v-col>
      <v-col>Amount</v-col>
      <v-col>Actions</v-col>
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
// TODO 9: add a button at the bottom of the page to submit expenses
// TODO 9: create a common button component where the text can be altered through a slot and make add expense and submit
// use this component

import {computed, reactive, watch} from 'vue';
import ExpenseRow from "@/components/ExpenseTracker/ExpenseRow.vue";
import type { ExpenseData } from '@/models/ExpenseData'

const MAX_DESCRIPTION_LENGTH = 30;
const MAX_DESCRIPTION_MESSAGE = `You can only input ${MAX_DESCRIPTION_LENGTH} characters`;
const MAX_AMOUNT_EXCEEDED_MESSAGE = `Spending on this expense will put you in the red`;


const data = reactive({
  totalIncome: 1000,
  addExpenseDisabled: false,
  expenseNameInput: '',
  expenseAmountInput: null,
  expenses: [
    {
      id: 0,
      description: 'Rent',
      value: 1000
    }
  ] as ExpenseData[]
});

const totalExpense = computed(() => {
  return data.expenses.reduce((total, expense) => {
    return total + expense.value;
  }, 0);
});

const totalLeft = computed(() => {
  return data.totalIncome - totalExpense.value;
});

const addExpenseDisabled = computed(() => {
  return !data.expenseNameInput || !data.expenseAmountInput;
});

const getMaxId = () => {
  return data.expenses.length > 0 ? Math.max(...data.expenses.map(expense => expense.id)) : 0;
};

const addExpense = () => {
  if (!data.expenseNameInput) {
    return;
  }

  data.expenses.push({
    id: getMaxId() + 1,
    description: data.expenseNameInput,
    value: data.expenseAmountInput ? parseInt(data.expenseAmountInput) : 0
  });
  data.expenseNameInput = '';
  data.expenseAmountInput = null;
}


const deleteExpense = (id: Number) => {
  data.expenses = data.expenses.filter(expense => expense.id !== id);
}


watch(() => data.expenseAmountInput, (newVal) => {
  if (newVal || 0 > totalLeft.value) {
    alert(MAX_AMOUNT_EXCEEDED_MESSAGE)
  }
})

watch(() => (data.expenseNameInput as String | null)?.length, (newVal) => {
  if (newVal || 0 > MAX_DESCRIPTION_LENGTH) {
    alert(MAX_DESCRIPTION_MESSAGE)
    data.expenseNameInput = data.expenseNameInput.slice(0, MAX_DESCRIPTION_LENGTH)
  }
})

</script>

<style scoped>
.headers{
  font-size: 1.2rem;
  border-bottom: 2px solid white;
  padding-bottom: 0px;
  margin-bottom: 10px;
}
</style>
