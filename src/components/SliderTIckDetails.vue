<script setup lang="ts">
import { computed } from 'vue'
import type { ColorI } from '@/types/color.ts'

const colors: ColorI[] = [
  { id: 0, value: "green" },
  { id: 5, value: "yellow" },
  { id: 10, value: "red" },
  { id: 15, value: "red" },
];

const props = defineProps<{
  valueSlider: number
  valueContent: string
}>()

const colorActive = computed(() => {
  console.log('here' +props.valueSlider );
  const matchingColor = colors.find((color) => color.id === props.valueSlider);
  return matchingColor ? matchingColor.value : "green"; // Valeur par défaut
});

console.log(colorActive.value);

</script>

<template>
  <div id="titleSlider">
    <div id="slider">
      <h3>- {{ props.valueContent }}</h3>
      <v-slider
        :color="colorActive.valueOf()"
        :model-value="props.valueSlider"
        min="0"
        max="10"
        step="5"
        show-ticks="always"
        >
      </v-slider>
    </div>
  </div>
</template>

<style scoped>


</style>
