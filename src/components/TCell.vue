<template>
  <div
    :class="[
      'cell',
      { 'move-to-center': props.isSelected, hover: !isSelected },
    ]"
    @click="$emit('click')"
    @keydown.esc="$emit('esc')"
    tabindex="0"
  ></div>
</template>

<script setup lang="ts">
import { defineProps, defineEmits, withDefaults } from 'vue';
import { PlacementCoeff } from './types';

const props = withDefaults(
  defineProps<{
    size: number;
    offset?: number;
    isSelected?: boolean;
    placement: PlacementCoeff;
  }>(),
  {
    size: 100,
    offset: 8,
    isSelected: false,
  }
);

const emits = defineEmits<{ (e: 'click'): void; (e: 'esc'): void }>();

const size = `${props.size}px`;
const coordToCenter = {
  x: `${props.placement.x * (props.size + props.offset)}px`,
  y: `${props.placement.y * (props.size + props.offset)}px`,
};
</script>

<style scoped>
.cell {
  width: v-bind(size);
  height: v-bind(size);
  background-color: white;
  outline: 0px solid grey;
  transform: translate(0, 0) scale(1);
  transition: outline 0.2s ease, transform 0.4s ease;
}
.hover:hover {
  outline: 8px solid grey;
}
.move-to-center {
  transform: translate(v-bind(coordToCenter.x), v-bind(coordToCenter.y))
    scale(3.08);
  z-index: 9999;
}
</style>
