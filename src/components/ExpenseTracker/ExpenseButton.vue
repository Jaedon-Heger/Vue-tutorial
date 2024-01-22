<template>
  <v-btn
      dark
      color="deep-purple accent-1"
      :disabled="disabled"
      @click="clickedButton"
  >
    <slot/>
  </v-btn>
</template>
<script setup lang="ts">


const emit = defineEmits(['click']);
const disabled = defineProps('disabled');

const clickedButton = () => {
  emit('click');
};
</script>
