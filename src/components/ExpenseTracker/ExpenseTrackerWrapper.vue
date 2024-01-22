<template>
  <v-card rounded class="pa-4">
    <v-card-title>
      <v-container>
        <v-row justify="start" align="start">
          <v-col cols="1">
            <h1>Expense Tracker</h1>
          </v-col>
          <v-spacer/>
          <v-col v-if="data.version==11" cols="1">
            <v-progress-circular
                class="progress"
                :color="getProgressLeftColor()"
                :model-value="data.totalPercentageLeft"
                :size="43"
                :width="7"
            />
          </v-col>
        </v-row>
      </v-container>
    </v-card-title>
    <v-card-text>
      <ExpenseTrackingV1/>
    </v-card-text>
  </v-card>
</template>

<script setup lang="ts">
import {reactive} from "vue";
import ExpenseTrackingV1 from '@/components/ExpenseTracker/ExpenseTrackingV1.vue';
import ExpenseTrackingV2 from '@/components/ExpenseTracker/ExpenseTrackingV2.vue';
import ExpenseTrackingV3 from "@/components/ExpenseTracker/ExpenseTrackingV3.vue";
import ExpenseTrackingV4 from "@/components/ExpenseTracker/ExpenseTrackingV4.vue";
import ExpenseTrackingV5 from "@/components/ExpenseTracker/ExpenseTrackingV5.vue";
import ExpenseTrackingV6 from "@/components/ExpenseTracker/ExpenseTrackingV6.vue";
import ExpenseTrackingV7 from "@/components/ExpenseTracker/ExpenseTrackingV7.vue";
import ExpenseTrackingV8 from "@/components/ExpenseTracker/ExpenseTrackingV8.vue";
import ExpenseTrackingV9 from "@/components/ExpenseTracker/ExpenseTrackingV9.vue";
import ExpenseTrackingV10 from "@/components/ExpenseTracker/ExpenseTrackingV10.vue";
import ExpenseTrackingV11 from "@/components/ExpenseTracker/ExpenseTrackingV11.vue";

// Todo 1.1: Pass props to wrapper and allow a version to be specified from the parent component
// Todo 1.2: Create a sub header for the version using the prop
// Todo 1.3: Inside v-card text add in expense tracking components and use conditional rendering to show the correct one based on the version
const data = reactive({
  totalPercentageLeft: 100,
  version: 11,
});

const getProgressLeftColor = () =>{
  if(data.totalPercentageLeft > 50) return 'green'
  if(data.totalPercentageLeft > 25) return 'orange'
  return 'red'
}

</script>

<style scoped>
</style>
