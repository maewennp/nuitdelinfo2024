<script setup lang="ts">
import TheWelcome from '../components/TheWelcome.vue'
import InfoModale from '@/components/InfoModale.vue'
import Gauge from '../components/Gauge.vue'
// import Event from '@/components/Event.vue'
</script>
<script lang="ts">
import { ref } from 'vue';

    let Temperature = 0;
    let CO2 = 0;
    let Health = 0;

    let State1 = {
        background : 'assets/background1.png', // ocean
        image : '', // profile image,
        filter: 'red',
        TemperatureUpdates: +1,
        CO2Updates: +1,
        HealthUpdates: +1,
    };
    let State2 = {
        background : 'assets/background1.png', // ocean
        image : '', // profile image
        filter: "filter: sepia(1) saturate(10) hue-rotate(-30deg);",
        TemperatureUpdates: -2,
        CO2Updates: +1,
        HealthUpdates: +1,
    };
    let State3 = {
        background : 'assets/background1.png', // ocean
        image : '', // profile image
        filter: '',
        TemperatureUpdates: +3,
        CO2Updates: +1,
        HealthUpdates: +1,
    };
    let State4 = {
        background : 'assets/background1.png', // ocean
        image : '', // profile image
        filter:  "filter: grayscale(100%)",
        TemperatureUpdates: +4,
        CO2Updates: +1,
        HealthUpdates: +1,
    };
    let State5 = {
        background : 'assets/background1.png', // ocean
        image : '', // profile image
        filter: "filter: sepia(100) saturate(5) hue-rotate(-90deg);",
        TemperatureUpdates: +5,
        CO2Updates: +1,
        HealthUpdates: +1,
    };
    let states = [State1, State2, State3, State4, State5];
    console.log(State1);
    console.log(states);
    console.log(states[0]);
    let activeState = 0;
    function UpdateSliders(TempUpdate: number, CO2Update : number, HealthUpdate : number){
        Temperature = Temperature + TempUpdate;
        CO2 = CO2 + CO2Update;
        Health = Health + HealthUpdate;
    }
    let TrafficStatus = 0;
    let HealthStatus = 0;
    let PollutionStatus = 0;

    function UpdateState(){
        activeState++;
        console.log(TrafficStatus%2);
        console.log(HealthStatus);
        console.log(PollutionStatus);
        console.log("Temperature" + Temperature + " CO2" + CO2 + " Health " + Health);
    }
    const trafficButtonMessage = ref<string>("Traffic maritime : ON");
    // let trafficButtonMessage = 'Traffic maritime : ON';
    function ToggleTraffic(){
        TrafficStatus++;
        // console.log(TrafficStatus%2);
        if(TrafficStatus%2 == 0) {
          document.getElementById("ocean")!.classList.remove('redClass');
          Temperature += 10;
          //mer en rouge
          // tete en rouge
          // surbrillance de la tete
          trafficButtonMessage.value = "Traffic maritime : OFF";
        }
        else {
          Temperature-=10;
          document.getElementById("ocean")!.classList.add('redClass');
          //mer plus en rouge
          // tete plus en rouge
          // tete plus en surbrillance
          trafficButtonMessage.value = "Traffic maritime : ON";
        }
        UpdateState();
    }
    function ToggleHealth(Id: number) {
      // 1 : marre noire, 2 : quota peche, 3 : filet plastique, 4 : micro plastique
        if(HealthStatus == Id){
          if (Id == 1) document.getElementById("ocean")!.classList.add('defaultClass');
          HealthStatus = 0;
          // reset la vue
          Health += 10;
        }
        else {
          if (Id == 1) document.getElementById("ocean")!.classList.add('grayClass');
          Health -= 10;
          HealthStatus = Id;
        } 
        UpdateState();
    }
    function TogglePollution(Id: number) {
        if(PollutionStatus == Id) {
          CO2 += 10;
          PollutionStatus = 0;
        }
        else {
          CO2 -= 10;
          PollutionStatus = Id;
        }
        UpdateState();
    }
</script>
<template>
  <main id="main">
    <InfoModale />
    <div>
        <img id="background" src="">
        <div>
            <p>Event temperature</p>
            <v-btn id = "TrafficButton" variant="outlined" @click="ToggleTraffic()">
                {{trafficButtonMessage}}
            </v-btn>
    
        </div>
        <div>
            <p>Event santés</p>
            <v-btn variant="outlined" @click="ToggleHealth(1)">
                Marrée noire
            </v-btn>
            <v-btn variant="outlined" @click="ToggleHealth(2)">
                Mise en place d'un quota de peche
            </v-btn>
            <v-btn variant="outlined" @click="ToggleHealth(3)">
                Ajouter des filets de recuperation du plastique dans les rivieres
            </v-btn>
            <v-btn variant="outlined" @click="ToggleHealth(4)">
                Augmenter la polution micro-plastique
            </v-btn>
        </div>
        <p>Event pollution</p>
        <v-btn variant="outlined" @click="TogglePollution(1)">
            Passage aux energies renouvelables
        </v-btn>
        <v-btn variant="outlined" @click="TogglePollution(2)">
            Que se passe t'il si il y a deforestation
        </v-btn>
    </div>
    <div class="ocean" id="ocean">
    <div class="wave"></div>
    <div class="wave"></div>
    <div class="wave"></div>
  </div>
  </main>
</template>

<style scoped>
  .redClass{
    filter: sepia(1) saturate(10) hue-rotate(-30deg);
  }
  .grayClass{
    filter: grayscale(100%)
  }
  .defaultClass{
    filter: none;
  }
.ocean {
  height: 280px;
  width: 100%;
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  overflow-x: hidden;
}

.wave {
  background: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 800 88.7'%3E%3Cpath d='M800 56.9c-155.5 0-204.9-50-405.5-49.9-200 0-250 49.9-394.5 49.9v31.8h800v-.2-31.6z' fill='%23003F7C'/%3E%3C/svg%3E");
  position: absolute;
  width: 200%;
  height: 100%;
  animation: wave 10s -3s linear infinite;
  transform: translate3d(0, 0, 0);
  opacity: 0.8;
}

.wave:nth-of-type(2) {
  bottom: 0;
  animation: wave 18s linear reverse infinite;
  opacity: 0.5;
}

.wave:nth-of-type(3) {
  bottom: 0;
  animation: wave 20s -1s linear infinite;
  opacity: 0.5;
}

@keyframes wave {
    0% {transform: translateX(0);}
    50% {transform: translateX(-25%);}
    100% {transform: translateX(-50%);}
}
</style>
