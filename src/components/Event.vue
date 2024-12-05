<script setup lang="ts">
    let Temperature = 0;
    let CO2 = 0;
    let PolutionPlastique = 0;
    let Surpeche = 0;

    let State1 = {
        background : 'assets/background1.png', // ocean
        image : '', // profile image,
        filter: 'red',
        TemperatureUpdates: +1,
        CO2Updates: +1,
        PolutionUpdates: +1,
        FishingUpdates: +1,
    };
    let State2 = {
        background : 'assets/background1.png', // ocean
        image : '', // profile image
        filter: "filter: sepia(1) saturate(10) hue-rotate(-30deg);",
        TemperatureUpdates: -2,
        CO2Updates: +1,
        PolutionUpdates: +1,
        FishingUpdates: +1,
    };
    let State3 = {
        background : 'assets/background1.png', // ocean
        image : '', // profile image
        filter: '',
        TemperatureUpdates: +3,
        CO2Updates: +1,
        PolutionUpdates: +1,
        FishingUpdates: +1,
    };
    let State4 = {
        background : 'assets/background1.png', // ocean
        image : '', // profile image
        filter:  "filter: grayscale(100%)",
        TemperatureUpdates: +4,
        CO2Updates: +1,
        PolutionUpdates: +1,
        FishingUpdates: +1,
    };
    let State5 = {
        background : 'assets/background1.png', // ocean
        image : '', // profile image
        filter: "filter: sepia(100) saturate(5) hue-rotate(-90deg);",
        TemperatureUpdates: +5,
        CO2Updates: +1,
        PolutionUpdates: +1,
        FishingUpdates: +1,
    };
    let states = [State1, State2, State3, State4, State5];
    console.log(State1);
    console.log(states);
    console.log(states[0]);
    let activeState = 0;
    function UpdateSliders(TempUpdate: number, CO2Update : number, PolutionUpdate : number, FishingUpdate: number){
        Temperature = Temperature + TempUpdate;
        CO2 = CO2 + CO2Update;
        PolutionPlastique = PolutionPlastique + PolutionUpdate;
        Surpeche = Surpeche + FishingUpdate;
        
    }
    function ChangeState(){
        // console.log(++activeState % 5);
        activeState++;
        // console.log(states[activeState % 5]);
        UpdateSliders(states[activeState % 5].TemperatureUpdates, states[activeState % 5].CO2Updates, states[activeState % 5].PolutionUpdates, states[activeState % 5].FishingUpdates);
        // console.log(Temperature);
        document.getElementById("background").src = states[activeState % 5].background;
        // if (states[activeState % 5].filter != '') 
            document.getElementById("background").style = states[activeState % 5].filter;
        console.log(activeState % 5);
    }
</script>
<template>
    <img id="background" src="">
    <v-btn variant="outlined" @click="ChangeState()">
        Button
    </v-btn>
</template>