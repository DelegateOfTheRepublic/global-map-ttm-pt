<script setup lang="ts">
import TCell from './components/TCell.vue';
import { ref } from 'vue';
import { CellPlacement } from './types';

const selectedCellId = ref<keyof CellPlacement>();
</script>

<template>
  <div class="container">
    <t-cell
      v-for="placement in Object.keys(CellPlacement)"
      :key="placement"
      :size="200"
      :placement="CellPlacement[placement]"
      :is-selected="selectedCellId === placement"
      @click="selectedCellId = placement"
      @esc="() => (selectedCellId = undefined)"
    />
  </div>
</template>

<style scoped>
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 8px;
}
</style>
