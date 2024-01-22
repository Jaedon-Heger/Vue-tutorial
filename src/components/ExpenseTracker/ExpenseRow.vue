<template>
  <v-row
      class="expenseRow"
      align-content="center"
  >
    <v-col>{{ expense.description }}</v-col>
    <v-col>{{ expense.value }}</v-col>
    <v-col>
      <v-hover>
        <template v-slot:default="{ isHovering, props }">
          <v-icon
              v-bind="props"
              :color="isHovering ? 'red-accent-2' : 'default'"
              @click="deleteExpense"
          >
            mdi-delete
          </v-icon>
        </template>
      </v-hover>
    </v-col>
  </v-row>
</template>
<script setup lang="ts">
import type ExpenseData from "@/models/ExpenseData";
import {onMounted} from "vue";

const props = defineProps<{
  expense: ExpenseData
}>()
const emit = defineEmits(['delete'])

const deleteExpense = () => {
  emit('delete', props.expense.id)
}


onMounted(()=>{
  console.log("Mounted")
});
</script>

<style scoped>
.expenseRow {
  border-bottom: 1px solid var(--color-border-hover);
}

</style>
