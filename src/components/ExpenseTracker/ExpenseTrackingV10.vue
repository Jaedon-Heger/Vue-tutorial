<template>
  <v-container>
    <v-row class="gradiantBorderBottom gradiantBorderBottomFullWidth pa-2">
      <v-container>
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
            <ExpenseButton :disabled="addExpenseDisabled" @click="addExpense">
              Add Expense
            </ExpenseButton>
          </v-col>
        </v-row>
      </v-container>
    </v-row>

    <v-row align="center" class="gradiantBorderBottom gradiantBorderBottomFullWidth pa-2">
      <v-container class="expenseTable">
        <v-row class="headers">
          <v-col>Description</v-col>
          <v-col>Amount</v-col>
          <v-col>Actions</v-col>
        </v-row>
        <v-row
            v-if="data.expenses.length==0"
            class="noData mb-10"
            align-content="center"
        >
          No Expenses
        </v-row>

        <div class="mb-10" v-else>
          <ExpenseRow
              v-for="expense in data.expenses"
              :key="expense.id"
              :expense="expense"
              @delete="deleteExpense"
          />
        </div>

      </v-container>
    </v-row>

    <v-row class="mt-10">
      <ExpenseButton :disabled="data.expenses.length < 1" @click="submit">
        Submit Expenses
      </ExpenseButton>
    </v-row>
  </v-container>
</template>

<script setup lang="ts">
// Todo 10: create your own 2 way binding for totalSpentPercentage and bind it in expense tracker to a v-progress-circular
// Hint: look into defineModel and use watches to alter its value.


import {computed, reactive, watch} from 'vue';
import ExpenseRow from "@/components/ExpenseTracker/ExpenseRow.vue";
import ExpenseButton from "@/components/ExpenseTracker/ExpenseButton.vue";
import type { ExpenseData } from '@/models/ExpenseData'

const MAX_DESCRIPTION_LENGTH = 30;
const MAX_DESCRIPTION_MESSAGE = `You can only input ${MAX_DESCRIPTION_LENGTH} characters`;
const MAX_AMOUNT_EXCEEDED_MESSAGE = `Spending on this expense will put you in the red`;


const data = reactive({
  totalIncome: 1000,
  addExpenseDisabled: false,
  expenseNameInput: '',
  expenseAmountInput: null,
  expenses: [] as ExpenseData[]
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

const submit = () => {
  alert('Expenses Submitted')
}

watch(() => data.expenseAmountInput, (newVal) => {
  if (newVal && newVal > totalLeft.value) {
    alert(MAX_AMOUNT_EXCEEDED_MESSAGE)
  }
})

watch(() => (data.expenseNameInput as String | null)?.length, (newVal) => {
  if (newVal && newVal > MAX_DESCRIPTION_LENGTH) {
    alert(MAX_DESCRIPTION_MESSAGE)
    data.expenseNameInput = data.expenseNameInput.slice(0, MAX_DESCRIPTION_LENGTH)
  }
})
</script>

<style scoped>
.headers {
  font-size: 1.2rem;
  border-bottom: 2px solid white;
  padding-bottom: 0px;
  margin-bottom: 10px;
}

.expenseTable {
  width: 80%;
}

</style>
