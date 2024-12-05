<template>
  <div class="JaugePlate">
    <div class="barre-container">
      <div class="barre" :style="{ width: niveau + '%', backgroundColor: couleurBarre }"></div>
    </div>
    <button @click="augmenter">Augmenter</button>
    <button @click="diminuer">Diminuer</button>
  </div>
</template>

<script lang="ts">
import { ref, computed } from 'vue'

export default {
  setup() {
    const niveau = ref(34) // Niveau d'essence initial

    const augmenter = () => {
      if (niveau.value < 100) {
        niveau.value += 34
      }
    }

    const diminuer = () => {
      if (niveau.value > 0) {
        niveau.value -= 34
      }
    }

    const couleurBarre = computed(() => {
      if (niveau.value > 68) {
        return 'green' // Vert pour plus de 66%
      } else if (niveau.value > 34) {
        return 'yellow' // Jaune pour entre 33% et 66%
      } else {
        return 'red' // Rouge pour 33% et moins
      }
    })

    return {
      niveau,
      augmenter,
      diminuer,
      couleurBarre,
    }
  },
}
</script>

<style scoped>
.JaugePlate {
  text-align: center;
}

.barre-container {
  width: 100%;
  background-color: #e0e0e0;
  border-radius: 10px;
  overflow: hidden;
}

.barre {
  height: 20px;
  text-align: center;
  line-height: 20px; /* Centrer le texte verticalement */
  color: white; /* Couleur du texte */
}
</style>
