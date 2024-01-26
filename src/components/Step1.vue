<template>
    <div class="step-1" aria-label="pick rock, paper or scissors">
        <div class="button-pick paper">
            <button aria-label="paper" @click="handleButtonClick"></button>
        </div>
        <div class="button-pick scissors">
            <button aria-label="scissors" @click="handleButtonClick"></button>
        </div>
        <div class="button-pick rock">
            <button aria-label="rock" @click="handleButtonClick"></button>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            choices: {
                userChoice: undefined,
                randomChoice: undefined,
            },
            possibleChoices: ["paper", "scissors", "rock"],
        }
    },
    methods: {
        handleButtonClick(event) {
            // update local variables
            this.updateUserChoice(event)
            this.updateRandomChoice()

            // send choices object to App
            this.$emit("choices", this.choices)
            
            // step1 is done, go to next step
            this.$emit("nextStep")
        },
        updateUserChoice(event) {
            this.choices.userChoice = event.target.getAttribute("aria-label")
        },
        getRandomInt(max) {
            return Math.floor(Math.random() * max)
        },
        updateRandomChoice() {
            this.choices.randomChoice = this.possibleChoices[this.getRandomInt(3)]
        },
    },
}
</script>