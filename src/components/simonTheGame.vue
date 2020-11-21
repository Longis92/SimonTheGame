<template>
    <div class="container">
        <h1>Simon The Game</h1>
        <div class="simon">
            <div class="buttons">
                <div class="button red" v-on:click="redClick" v-bind:style="buttonStyleRed"></div>
                <div class="button blue" v-on:click="blueClick" v-bind:style="buttonStyleBlue"></div>
                <div class="button yellow" v-on:click="yellowClick" v-bind:style="buttonStyleYellow"></div>
                <div class="button green" v-on:click="greenClick" v-bind:style="buttonStyleGreen"></div>
            </div>
        </div>
        <div class="gameInfo">
            <button v-on:click="startGame">Start</button>
            <p class="gameResult">{{ this.message }}</p>
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
            level: "легкий", 
            timeout: 1500,
            currentPressedButton: 0,
            currentDisplayButton: 0,
            message: "",
            sounds: {
                1: './assets/audio/1.mp3',
                2: './assets/audio/2.mp3',
                3: './assets/audio/3.mp3',
                4: './assets/audio/4.mp3',
            },
        }            
    },
    computed: {
        buttonStyleBlue: function() {
            if (this.currentDisplayButton === 1) {
                return {
                    background: "black"
                }
            } else {
                return {
                    background: "blue"
                }
            }
        },
        buttonStyleRed: function() {
            if (this.currentDisplayButton === 2) {
                return {
                    background: "black"
                }
            } else {
                return {
                    background: "red"
                }
            }
        },
        buttonStyleGreen: function() {
            if (this.currentDisplayButton === 3) {
                return {
                    background: "black"
                }
            } else {
                return {
                    background: "green"
                }
            }
        },
        buttonStyleYellow: function(){
            if (this.currentDisplayButton === 4) {
                return {
                    background: "black"
                }
            } else {
                return {
                    'background': "yellow"
                }
            }
        },
    },
    methods: {
        startGame() {
            // задаем level в соответствии с указанным:
            // level =
            // задаем timeout в соответствии с level:
            switch (this.level) {
                case "легкий":
                    this.timeout = 1500
                    break;
                case "средний":
                    this.timeout = 1000
                    break;
                case "сложный":
                    this.timeout = 400
                    break;
            }
            this.simonSteps=[]
            this.playerSteps=[]
            this.addStep()
            this.displaySteps(this.simonSteps)
            this.resetPressedButton()
            this.getUserActions(this.simonSteps.length)
            console.log(this.playerSteps) 
            if (this.getGameResult(this.simonSteps, this.playerSteps)) {
                console.log("You win!")
                //this.message = "You win!"
            } else {
                console.log("You lose!")
                //this.message = "You lose!"
            }
        },
        addStep() { 
            this.simonSteps.push(Math.floor((Math.random() * 4) + 1))
        },
        resetDisplayButton() {
            this.currentDisplayButton = 0
        },
        displaySteps(simonSteps) {
            for (let index = 0; index < simonSteps.length; index++) {
                this.currentDisplayButton = simonSteps[index]
                setTimeout(this.resetDisplayButton, 200)
            }
        },
        getCurrentPressedButton() {
            this.playerSteps.push(this.currentPressedButton)
            this.currentPressedButton = 0
        },
        getUserActions(count) {
            for (let index = 0; index < count; index++) {
                setTimeout(this.getCurrentPressedButton, this.timeout)
            }
        },
        blueClick() {
            this.currentPressedButton = 1
        },
        redClick() {
            this.currentPressedButton = 2
        },
        greenClick() {
            this.currentPressedButton = 3
        },
        yellowClick() {
            this.currentPressedButton = 4
        },
        getGameResult(simonSteps, playerSteps) {
            for (let index = 0; index < simonSteps.length; index++) {
                if (simonSteps.indexOf(index) !== playerSteps.indexOf(index)) {
                    return false
                }
            }
            return true
        },
    }
}
</script>