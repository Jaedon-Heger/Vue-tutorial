<template>
  <v-card rounded class="pa-4">
    <v-card-title>
      <v-container>
        <v-row justify="start" align="start">
          <v-col cols="1">
            <h1>Expense Tracker</h1>
          </v-col>
          <v-spacer/>
<!--          <v-col v-if="data.version>10" cols="1">-->
<!--            <v-progress-circular-->
<!--                class="progress"-->
<!--                :color="getProgressLeftColor()"-->
<!--                :model-value="data.totalPercentageLeft"-->
<!--                :size="43"-->
<!--                :width="7"-->
<!--            />-->
<!--          </v-col>-->
        </v-row>
      </v-container>
    </v-card-title>
    <v-card-text>
<!--      <ExpenseTrackingV1 v-if="data.version == 1"/>-->
<!--      <ExpenseTrackingV2 v-if="data.version == 2"/>-->
<!--      <ExpenseTrackingV3 v-if="data.version == 3"/>-->
<!--      <ExpenseTrackingV4 v-if="data.version == 4"/>-->
<!--      <ExpenseTrackingV5 v-if="data.version == 5"/>-->
<!--      <ExpenseTrackingV6 v-if="data.version == 6"/>-->
<!--      <ExpenseTrackingV7 v-if="data.version == 7"/>-->
<!--      <ExpenseTrackingV8 v-if="data.version == 8"/>-->
<!--      <ExpenseTrackingV9 v-if="data.version == 9"/>-->
<!--      <ExpenseTrackingV10 v-if="data.version == 10"/>-->
<!--      <ExpenseTrackingV11 v-if="data.version == 11" v-model="data.totalPercentageLeft"/>-->
<!--      <ExpenseTrackingV12 v-if="data.version == 12" v-model="data.totalPercentageLeft"/>-->
    </v-card-text>
  </v-card>
</template>

<script setup lang="ts">
// import ExpenseTrackingV1 from '@/components/ExpenseTracker/ExpenseTrackingV1.vue';
//
// import ExpenseTrackingV2 from '@/components/ExpenseTracker/ExpenseTrackingV2.vue';
// import ExpenseTrackingV3 from "@/components/ExpenseTracker/ExpenseTrackingV3.vue";
// import ExpenseTrackingV4 from "@/components/ExpenseTracker/ExpenseTrackingV4.vue";
// import ExpenseTrackingV5 from "@/components/ExpenseTracker/ExpenseTrackingV5.vue";
// import ExpenseTrackingV6 from "@/components/ExpenseTracker/ExpenseTrackingV6.vue";
// import ExpenseTrackingV7 from "@/components/ExpenseTracker/ExpenseTrackingV7.vue";
// import ExpenseTrackingV8 from "@/components/ExpenseTracker/ExpenseTrackingV8.vue";
// import ExpenseTrackingV9 from "@/components/ExpenseTracker/ExpenseTrackingV9.vue";
// import ExpenseTrackingV10 from "@/components/ExpenseTracker/ExpenseTrackingV10.vue";
// import ExpenseTrackingV11 from "@/components/ExpenseTracker/ExpenseTrackingV11.vue";
// import ExpenseTrackingV12 from "@/components/ExpenseTracker/ExpenseTrackingV12.vue";


// Todo 1: Create a reactive property for the version and totalPercentageLeft.
//  Note if you decide to use ref then you must remove data.version and replace it with version
// Todo 1: Create a sub header for the version using the prop
// Todo 1: uncomment the template code and corresponding imports
//
// const getProgressLeftColor = () => {
//   if(data.totalPercentageLeft > 50) return 'green'
//   if(data.totalPercentageLeft > 25) return 'orange'
//   return 'red'
// }

</script>

<style scoped>
</style>
