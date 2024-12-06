<script setup lang="ts">
import { computed } from 'vue'
import type { ColorI } from '@/types/color.ts'

const colors: ColorI[] = [
  { id: 0, value: "green" },
  { id: 1, value: "yellow" },
  { id: 2, value: "red" },
];

const props = defineProps<{
  valueSlider: number
}>()

const colorActive = computed(() => {
  const matchingColor = colors.find((color) => color.id === props.valueSlider);
  return matchingColor ? matchingColor.value : "green"; // Valeur par défaut
});

</script>

<template>
  <div>
    <v-slider
      :color="colorActive.valueOf()"
      :model-value="props.valueSlider"
      min="0"
      max="2"
      step="1"
      show-ticks="always"
      disabled
    />
  </div>
</template>

<style scoped></style>
