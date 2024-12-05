<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
    <header>
      <div class="wrapper">
        <div class="character_sheet">
    
          <div class="title">
            <h2>Personnage</h2>
          </div>

          <div class="content">
            <Gauge>
              <template #icon>
                *
              </template>
              <template #heading>Température</template>
              Contenu
            </Gauge>
            <Gauge>
              <template #icon>
                *
              </template>
              <template #heading>Dioxygène / O²</template>
              Contenu
            </Gauge>
            <Gauge>
              <template #icon>
                *
              </template>
              <template #heading>Pollution</template>
              Contenu
            </Gauge>
            <Gauge>
              <template #icon>
                *
              </template>
              <template #heading>Sur-pêche</template>
              Contenu
            </Gauge>

          </div>
        </div>
      </div>
    </header>

    <RouterView />

</template>

<style scoped>
header {
  width: 100%;
}


</style>
