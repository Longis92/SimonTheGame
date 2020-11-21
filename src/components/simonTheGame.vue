<template>
    <div class="container">
        <h1>Simon The Game</h1>
        <div class="simon">
            <div class="buttons">
                <div class="button red" v-on:click="redClick"></div>
                <div class="button blue" v-on:click="blueClick"></div>
                <div class="button yellow" v-on:click="yellowClick"></div>
                <div class="button green" v-on:click="greenClick"></div>
            </div>
        </div>
        <div class="gameInfo">
            <button v-on:click="startGame">Start</button>
            <span class="stepCounter">{{ stepCounter }}</span>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            simonSteps: [], //массив шагов Саймона
            playerSteps: [], //массив шагов игрока
            stepCounter: 1,
            sounds: {
                1: './assets/audio/1.mp3',
                2: './assets/audio/2.mp3',
                3: './assets/audio/3.mp3',
                4: './assets/audio/4.mp3',
            }
        }            
    },
    watch: {

    },
    methods: {
        startGame() {
            this.simonSteps=[]
            this.playerSteps=[]
            this.addStep()
            //this.displaySteps()
        },
        addStep() { //метод добавляет шаг в массив Саймона
            this.simonSteps.push(Math.floor((Math.random() * 4) + 1))
        },
        blueClick() {
            this.playerSteps.push(1)
        },
        redClick() {
            this.playerSteps.push(2)
        },
        yellowClick() {
            this.playerSteps.push(3)
        },
        greenClick() {
            this.playerSteps.push(4)
        },
        //displaySteps() {
        //},
    }
}
</script>