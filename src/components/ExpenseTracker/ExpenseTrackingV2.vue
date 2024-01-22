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
            <v-btn dark>
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

// Todo 2: set color and prepend icon prop for Add expense button
// Todo 2: bind addExpenseDisabled to the button

const data = reactive({
  totalIncome: 1000,
  totalExpense: 0,
  totalLeft: 0,
  addExpenseDisabled: false,
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
