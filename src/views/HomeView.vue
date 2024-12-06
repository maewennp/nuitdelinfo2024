<script setup lang="ts">
import InfoModale from '@/components/InfoModale.vue'
import Gauge from '../components/Gauge.vue'
import SliderTIckDetails from '@/components/SliderTIckDetails.vue'
// import Event from '@/components/Event.vue'
import Event from '@/components/Event.vue'
</script>

<script lang="ts">
import { ref } from 'vue';

const Temperature = ref(0);
const CO2 = ref(5);
const Health = ref(0);

let State1 = {
  background: 'assets/background1.png', // ocean
  image: '', // profile image,
  filter: 'red',
  TemperatureUpdates: +1,
  CO2Updates: +1,
  HealthUpdates: +1,
};
let State2 = {
  background: 'assets/background1.png', // ocean
  image: '', // profile image
  filter: "filter: sepia(1) saturate(10) hue-rotate(-30deg);",
  TemperatureUpdates: -2,
  CO2Updates: +1,
  HealthUpdates: +1,
};
let State3 = {
  background: 'assets/background1.png', // ocean
  image: '', // profile image
  filter: '',
  TemperatureUpdates: +3,
  CO2Updates: +1,
  HealthUpdates: +1,
};
let State4 = {
  background: 'assets/background1.png', // ocean
  image: '', // profile image
  filter: "filter: grayscale(100%)",
  TemperatureUpdates: +4,
  CO2Updates: +1,
  HealthUpdates: +1,
};
let State5 = {
  background: 'assets/background1.png', // ocean
  image: '', // profile image
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
function UpdateSliders(TempUpdate: number, CO2Update: number, HealthUpdate: number) {
  Temperature.value = Temperature.value + TempUpdate;
  CO2.value = CO2.value + CO2Update;
  Health.value = Health.value + HealthUpdate;
}
let TrafficStatus = 10;
let HealthStatus = 10;
let PollutionStatus = 0;

function UpdateState() {
  activeState++;
  console.log(TrafficStatus % 2);
  console.log(HealthStatus);
  console.log(PollutionStatus);
  console.log("Temperature" + Temperature.value + " CO2" + CO2.value + " Health " + Health.value);
}
const trafficButtonMessage = ref<string>("Traffic maritime : OFF");
// let trafficButtonMessage = 'Traffic maritime : ON';
function ToggleTraffic() {
  TrafficStatus++;
  // console.log(TrafficStatus%2);

  if (activeButtonTemperature != 0)
    document.getElementById('TrafficButton')?.classList.remove('activeButton');
  if (TrafficStatus % 2 == 0) {
    document.getElementById('TrafficButton')?.classList.remove('activeButton');
    document.getElementById("ocean")!.classList.remove('redClass');
    Temperature.value += 10;
    //mer en rouge
    // tete en rouge
    // surbrillance de la tete
    trafficButtonMessage.value = "Traffic maritime : OFF";
    document.getElementById("Tête")!.style.visibility = "hidden";
    document.getElementById("Sang")!.style.visibility = "hidden";
  }
  else {
    document.getElementById('TrafficButton')?.classList.add('activeButton');
    Temperature.value -= 10;
    document.getElementById("ocean")!.classList.add('redClass');
    //mer plus en rouge
    // tete plus en rouge
    // tete plus en surbrillance
    trafficButtonMessage.value = "Traffic maritime : ON";
    document.getElementById("Tête")!.style.visibility = "visible";
    document.getElementById("Sang")!.style.visibility = "visible";
  }
  UpdateState();
}
function ToggleHealth(Id: number) {
  // 1 : marre noire, 2 : quota peche, 3 : filet plastique, 4 : micro plastique
  if (activeButtonHealth != 0)
    document.getElementById('Health'+activeButtonHealth)?.classList.remove('activeButton');
  if (HealthStatus == Id) {
    document.getElementById('Health'+activeButtonHealth)?.classList.remove('activeButton');
    if (Id == 1) document.getElementById("ocean")!.classList.remove('grayClass');
    document.getElementById("Estomac")!.style.visibility = "hidden";
    document.getElementById("Peau")!.style.visibility = "hidden";
    document.getElementById("Rein")!.style.visibility = "hidden";
    
    HealthStatus = 0;
    // reset la vue
    if (Id == 1 || Id == 4) Health.value = 0;
    else Health.value = 0;
  }
  else {
    if(activeButtonHealth == 1) document.getElementById("ocean")!.classList.remove('grayClass');
    activeButtonHealth = Id;
    document.getElementById('Health'+activeButtonHealth)?.classList.add('activeButton');
    if (Id == 1) document.getElementById("ocean")!.classList.add('grayClass');
    
    document.getElementById("Estomac")!.style.visibility = "visible";
    document.getElementById("Peau")!.style.visibility = "visible";
    document.getElementById("Rein")!.style.visibility = "visible";
    
    // if (Health>=0) {
      if (Id == 1 || Id == 4) Health.value = -10;
    // }
    // if (Health<0) {
      if (Id == 2 || Id == 3) Health.value = 10;
    // }
    HealthStatus = Id;
  }
  UpdateState();
}
function TogglePollution(Id: number) {
  if (activeButtonPollution != 0)
    document.getElementById('Pollution'+activeButtonPollution)?.classList.remove('activeButton');
  if (PollutionStatus == Id) {
    document.getElementById("Poumons")!.style.visibility = "hidden";
    // document.getElementById('Pollution'+activeButtonPollution)?.classList.remove('activeButton');
    CO2.value = 5;
    PollutionStatus = 0;
  }
  else {
    activeButtonPollution = Id;
    document.getElementById('Pollution'+activeButtonPollution)?.classList.add('activeButton');
    document.getElementById("Poumons")!.style.visibility = "visible";
    if (CO2.value>=0) {
      if(Id == 2)
        CO2.value = 10;
      else CO2.value = 0;
    }
    PollutionStatus = Id;
  }
  UpdateState();
}

let valueTest = 1
let activeButtonHealth = 0;
let activeButtonTemperature = 0;
let activeButtonPollution = 0;

</script>
<template>
  <main id="main">
    <InfoModale></InfoModale>
    <div class="container">
      <div class="block-slider">
        <h2  class="title-information">Informations</h2>
        <SliderTIckDetails :value-slider="-Temperature" :value-content="'Temperature'" />
        <SliderTIckDetails :value-slider="CO2" :value-content="'Santé'"/>
        <SliderTIckDetails :value-slider="(-Health + 10 / 2)" :value-content="'Pollution'"/>
      </div>

      <div id="sky">
        <div class="cloud"></div>
        <div class="cloud"></div>
      </div>

      <div id="ocean">

        <div id="boat-container">

          <div id="boat">
            <div id="shadow-right"></div>
            <div id="rim-left"></div>
            <div id="rim-right"></div>
            <div id="luggage-left"></div>
            <div id="luggage-left-shadow"></div>
          </div>

          <div id="sailor"></div>
          <div id="sailor-arm-left"></div>
          <div id="sailor-arm-right"></div>
          <span class="sailor-eye"></span>
          <span class="sailor-eye"></span>
          <div id="rim"></div>

        </div>

        <svg class="waves" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
          viewBox="0 24 150 28" preserveAspectRatio="none" shape-rendering="auto">
          <defs>
            <path id="gentle-wave" d="M-160 44c30 0 58-18 88-18s 58 18 88 18 58-18 88-18 58 18 88 18 v44h-352z" />
          </defs>
          <g class="parallax">
            <use xlink:href="#gentle-wave" x="48" y="0" fill="rgba(155, 220, 251, 0.7)" />
            <use xlink:href="#gentle-wave" x="48" y="3" fill="rgba(129, 204, 250,0.5)" />
            <use xlink:href="#gentle-wave" x="48" y="5" fill="rgba(255,255,255,0.3)" />
            <use xlink:href="#gentle-wave" x="48" y="7" fill="rgba(184, 236, 253, 1)" />
          </g>
        </svg>
      </div>
    </div>

    <div class="ocean" id="ocean">
      <div class="wave"></div>
      <div class="wave"></div>
      <div class="wave"></div>
    </div>

    <div class="coucou">

      <!-- <img id="background" src=""> -->
      <div class="block-event">

        <img id="background" src="">
          <p class="title-event">Event temperature</p>
          <v-btn id="TrafficButton" variant="outlined" @click="ToggleTraffic()">
            {{ trafficButtonMessage }}
          </v-btn>
      </div>

      <div class="block-event-central">
        <p class="title-event">Event santés</p>
        <div class="little-block">
          <v-btn class="width-button-event" id = "Health1" variant="outlined" @click="ToggleHealth(1)">
            Marrée noire
          </v-btn>
          <v-btn class="width-button-event" id = "Health3" variant="outlined" @click="ToggleHealth(3)">
            Filets recup plastique
          </v-btn>
        </div>

        <div class="little-block">
          <v-btn class="width-button-event" id = "Health2" variant="outlined" @click="ToggleHealth(2)">
            Quota de peche
          </v-btn>
          <v-btn class="width-button-event" id = "Health4" variant="outlined" @click="ToggleHealth(4)">
            Polution micro-plastique
          </v-btn>
        </div>
      </div>

      <div class="block-event">
        <p class="title-event">Event pollution</p>
        <v-btn class="width-button-event" id = "Pollution1" variant="outlined" @click="TogglePollution(1)">
          Energies renouvelables
        </v-btn>
        <v-btn class="width-button-event" id = "Pollution2" variant="outlined" @click="TogglePollution(2)">
          Déforestation
        </v-btn>
      </div>
    </div>

  </main>
</template>

<style scoped>
.activeButton {
  background-color: green;
}
body {
  margin: 0;
  background-color: rgb(184, 236, 253);
}

.coucou {
    background-color: #083c7c;
    display: flex;
    justify-content: space-between;
    padding: 1vh 1vh 1vh 1vh;
    position: absolute;
    bottom: 0;
    width: 100%;
    z-index: 10;
    color: white;
}


.block-event {
    width: 20%;
    display: flex;
    flex-direction: column;
    gap: 6px;
    align-items: center;
}

.block-event-central {
    width: 40%;
    display: flex;
    flex-direction: column;
    gap: 6px;
}

.little-block {
    display: flex;
    flex-direction: row;
    gap: 4px;
}

.width-button-event {
    width: 35vh;
}

.title-event{
  text-align: center;
  font-weight: bold;
}

.container {
  position: relative;
  background-image: linear-gradient(to right top, rgb(106, 184, 249) 65%, rgb(249, 242, 106));
}

#sky {
  height: 62.5vh;
  width: 100%;
  margin: 0;
  padding: 0;
}

.cloud {
  margin: auto;
  position: absolute;
  bottom: 0;
  left: 0;
  top: 0;
  right: 0;
  right: 750px;
  bottom: 150px;
  height: 125px;
  width: 125px;
  border-radius: 50%;
  background-color: white;
  opacity: 0.6;
}

.cloud:nth-of-type(2) {
  bottom: 250px;
  left: 1150px;
}

.cloud::before {
  content: "";
  position: absolute;
  left: 80px;
  top: 40px;
  height: 85px;
  width: 85px;
  border-radius: 50%;
  background-color: white;
}

.cloud::after {
  content: "";
  position: absolute;
  left: -40px;
  top: 35px;
  height: 85px;
  width: 85px;
  border-radius: 50%;
  background-color: white;
}

#ocean #boat-container {
  animation: boatsway 3s ease-in-out infinite alternate;
}

@keyframes boatsway {
  from {
    transform: rotate(-5.5deg);
  }

  to {
    transform: rotate(5.5deg);
  }
}

#boat {
  margin: auto;
  position: absolute;
  bottom: 0;
  left: 0;
  top: 0;
  right: 0;
  top: 30px;
  width: 400px;
  height: 100px;
  background-color: rgb(34, 92, 238);
  border-bottom-right-radius: 5rem;
  border-bottom-left-radius: 5rem;
  z-index: 3;
  transform-style: preserve-3d;
}

#boat::before {
  content: "";
  position: absolute;
  height: 125px;
  width: 125px;
  left: 225px;
  bottom: 0px;
  border-top-left-radius: 4rem;
  border-bottom-right-radius: 5rem;
  background-color: rgb(34, 92, 238);
  z-index: 3;
}

#boat::after {
  content: "";
  position: absolute;
  height: 100px;
  width: 100px;
  left: 222.5px;
  bottom: 45px;
  border-radius: 4rem;
  background-color: rgb(250, 221, 95);
  transform: translateZ(-1px);
}

#shadow-right {
  margin: auto;
  position: absolute;
  bottom: 0;
  left: 0;
  top: 0;
  right: 0;
  left: 275px;
  bottom: 25px;
  height: 125px;
  width: 125px;
  border-top-left-radius: 4rem;
  border-bottom-right-radius: 5rem;
  background-color: rgb(6, 58, 212);
  z-index: 2;
}

#rim-left {
  margin: auto;
  position: absolute;
  bottom: 0;
  left: 0;
  top: 0;
  right: 0;
  width: 260px;
  height: 22.5px;
  background-color: rgb(250, 221, 95);
  border-radius: 5rem;
  left: -180px;
  top: -115px;
  z-index: 3;
}

#rim-right {
  margin: auto;
  position: absolute;
  bottom: 0;
  left: 0;
  top: 0;
  right: 0;
  width: 155px;
  height: 20px;
  background-color: rgb(250, 221, 95);
  border-radius: 5rem;
  right: -290px;
  top: -170px;
  z-index: 5;
}

#rim-right::before {
  content: "";
  position: absolute;
  width: 55px;
  right: 0px;
  height: 20px;
  background-color: rgb(245, 183, 72);
  border-radius: 5rem;
}

#rim-right::after {
  content: "";
  position: absolute;
  width: 55px;
  right: 40px;
  height: 20px;
  background-color: rgb(250, 221, 95);
  border-radius: 5rem;
}

#luggage-left {
  margin: auto;
  position: absolute;
  bottom: 0;
  left: 0;
  top: 0;
  right: 0;
  left: -380px;
  top: -143px;
  width: 110px;
  height: 70px;
  border-radius: 1rem;
  background-color: rgb(184, 236, 253);
  opacity: 0.7;
  transform: translateZ(-1px);
}

#luggage-left::before {
  content: "";
  position: absolute;
  left: -20px;
  width: 80px;
  height: 57.5px;
  background-color: white;
  border-radius: 1rem;
}

#luggage-left::after {
  content: "";
  position: absolute;
  top: 12.5px;
  left: -2.5px;
  width: 37.5px;
  height: 12.5px;
  background-color: rgb(250, 221, 95);
  border-radius: 1rem;
}

#sailor {
  margin: auto;
  position: absolute;
  bottom: 0;
  left: 0;
  top: -150px;
  right: 0;
  height: 110px;
  width: 97.5px;
  right: 115px;
  border-top-left-radius: 4rem;
  border-top-right-radius: 4rem;
  background-color: rgb(254, 195, 172);
  z-index: 1;
}

#sailor::before {
  content: "";
  position: absolute;
  width: 14.5px;
  height: 8.5px;
  background-color: black;
  border-bottom-left-radius: 1rem;
  border-bottom-right-radius: 1rem;
  top: 70.5px;
  left: 35.5px;
}

#sailor-arm-left {
  margin: auto;
  position: absolute;
  bottom: 0;
  left: -65.5px;
  top: -67.5px;
  right: 0;
  height: 55px;
  width: 30px;
  background-color: rgb(254, 195, 172);
  z-index: 6;
  transform: translateZ(1px);
  border-radius: 4rem;
}

#sailor-arm-right {
  margin: auto;
  position: absolute;
  bottom: 0;
  left: -235.5px;
  top: -135px;
  right: 0;
  height: 30px;
  width: 65px;
  background-color: rgb(254, 195, 172);
  z-index: 6;
  transform: translateZ(1px);
  border-radius: 4rem;
  transform-origin: right center;
  animation: wave 0.85s infinite alternate ease-in-out;
}

@keyframes wave {
  from {
    transform: rotate(-15deg);
  }

  to {
    transform: rotate(15deg);
  }
}

.sailor-eye {
  margin: auto;
  position: absolute;
  bottom: 0;
  left: -162.5px;
  top: -172.5px;
  right: 0;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  background-color: white;
  z-index: 7;
}

.sailor-eye:nth-of-type(2) {
  left: -87.5px;
}

.sailor-eye::before {
  content: "";
  position: absolute;
  width: 10px;
  height: 10px;
  background-color: black;
  border-radius: 50%;
  top: 9px;
  left: 10px;
}

.waves {
  position: relative;
  width: 100%;
  height: 15vh;
  margin-bottom: -7px;
  min-height: 100px;
  max-height: 150px;
  z-index: 10;
}

.parallax>use {
  animation: tide 25s cubic-bezier(0.55, 0.5, 0.45, 0.5) infinite;
}

@keyframes tide {
  from {
    transform: translate3d(-90px, 0, 0);
  }

  to {
    transform: translate3d(85px, 0, 0);
  }
}

.parallax>use:nth-child(1) {
  animation-delay: -2s;
  animation-duration: 7s;
}

.parallax>use:nth-child(2) {
  animation-delay: -3s;
  animation-duration: 10s;
}

.parallax>use:nth-child(3) {
  animation-delay: -4s;
  animation-duration: 13s;
}

.parallax>use:nth-child(4) {
  animation-delay: -5s;
  animation-duration: 20s;
}

.redClass {
  filter: sepia(1) saturate(10) hue-rotate(-30deg);
}

.grayClass {
  filter: grayscale(100%)
}

.defaultClass {
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

.title-information{
  text-align: center;
}

.block-slider{
  display: block;
  width: 20%;
  float: right;
  padding: 10px;
  background: rgba(0, 0, 0, 0.2);
}

@keyframes wave {
  0% {
    transform: translateX(0);
  }

  50% {
    transform: translateX(-25%);
  }

  100% {
    transform: translateX(-50%);
  }
}
</style>
