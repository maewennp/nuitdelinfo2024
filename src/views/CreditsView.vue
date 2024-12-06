<script setup lang="ts">
import { ref } from 'vue'

const titleClass = ref('title')


</script>

<template>
  <h1 :class="titleClass">Credits</h1>
  <div class="imgbox">
   
		<div class="column">

			<img src="../assets/maewenn.jpg" alt="Maeween - 'Vous voulez pas participer à la nuit de l'info de l'an prochain ?'"title="MaeWenn"/>
			<img src="../assets/johan.jpg" alt="Johan - dev aguerri et émérite. Producteur notoire de cette page"/>    
			<img src="../assets/marie.jpg" alt="Marie - L'autre artisane de cette page. Présentatrice de talent et reine du power point"/>
			<img src="../assets/david.jpg" alt="David - Dénicheur d'assets qui ne serviront finalement pas"/>
			<img src="../assets/enzo.jpg" alt="Enzo - Architecte du slider"/>			
		</div>
		<div class="column">
			<img src="../assets/coline.jpg" alt="Coline #Godefroy energy"/>
			<img src="../assets/jerome.jpg" alt="Jérôme testeur s'il en est"/>
			<img src="../assets/justine.jpg"alt="Justine la reine des vagues"/>
			<img src="../assets/ilan.jpg" alt="Ilan dit 'Nan mais vous verrez, c'est beginner friendly le vuejs'"/>

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

img:hover{
	opacity: 0.3;
}
* {
	background-color: rgb(13, 162, 207);
}
img:hover .text {
    opacity: 1;
}

.text {
  background-color: #04AA6D;
  color: white;
  font-size: 24px;
  padding: 16px 32px;
}


</style>