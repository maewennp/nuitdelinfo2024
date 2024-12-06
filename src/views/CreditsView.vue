<script setup lang="ts">
import { ref } from 'vue'

const titleClass = ref('title')
</script>

<template>
  <h1 :class="titleClass">Credits</h1>
  <div class="imgbox">
		<div class="column">
			<img src="../assets/coline.jpg"/>
			<img src="../assets/jerome.jpg"/>
			<img src="../assets/justine.jpg"/>
			<img src="../assets/ilan.jpg"/>
			<img src="../assets/maewenn.jpg"/>
			
		</div>
		<div class="column">
			
			<img src="../assets/johan.jpg"/>
			<img src="../assets/david.jpg"/>
			<img src="../assets/marie.jpg"/>
			<img src="../assets/enzo.jpg"/>
		</div>
	</div>



</template>

<style>
.title {
  text-align: center;
  font-family: sans-serif;
  font-size: xxx-large;
  padding-bottom: 10px;
  color: black;
}
.imgbox {
	display : flex ;
    flex-direction: column ;
}
.column {
	display : flex ;
    flex-direction: row ;
	justify-content: center;
	width: 100%;
}
img {

    border: 10px solid transparent;
	width: 20%;
}
* {
	background-color: rgb(13, 162, 207);
}
</style>