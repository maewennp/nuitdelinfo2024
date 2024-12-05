<script setup lang="ts">
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
        // console.log(++activeState % 5);
        activeState++;
        // console.log(states[activeState % 5]);
        // UpdateSliders(states[activeState % 5].TemperatureUpdates, states[activeState % 5].CO2Updates, states[activeState % 5].PolutionUpdates, states[activeState % 5].FishingUpdates);
        // console.log(Temperature);
        (document.getElementById("background")as HTMLImageElement).src = states[activeState % 5].background;
        // if (states[activeState % 5].filter != '') 
        document.getElementById("background")!.style = states[activeState % 5].filter;

        // console.log(activeState % 5);
        console.log(TrafficStatus%2);
        console.log(HealthStatus);
        console.log(PollutionStatus);
        console.log("Temperature" + Temperature + " CO2" + CO2 + " Health " + Health);
        
        // if Traffic % 2 = 0 : pas de traffic, else du traffic
        // if 
    }
    const trafficButtonMessage = ref<string>("Traffic maritime : ON");
    // let trafficButtonMessage = 'Traffic maritime : ON';
    function ToggleTraffic(){
        TrafficStatus++;
        // console.log(TrafficStatus%2);
        if(TrafficStatus%2 == 0) {
            Temperature+=10;
            trafficButtonMessage.value = "Traffic maritime : OFF";
        }
        else {
            Temperature-=10;
            trafficButtonMessage.value = "Traffic maritime : ON";
        }
        UpdateState();
    }
    function ToggleHealth(Id: number) {
        if(HealthStatus == Id) HealthStatus = 0;
        else HealthStatus = Id;
        UpdateState();
    }
    function TogglePollution(Id: number) {
        if(PollutionStatus == Id) PollutionStatus = 0;
        else PollutionStatus = Id;
        UpdateState();
    }
</script>
<template>
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
</template>