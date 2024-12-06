<script setup lang="ts">
import { ref } from 'vue'

const titleClass = ref('title')
</script>

<template>
  <h1 :class="titleClass">Credits</h1>
  <img src="../assets/coline.jpg"/>
</template>

<style>
.title {
  text-align: center;
}
</style>