<template>
    <div class="step-1" aria-label="pick rock, paper or scissors">
        <div class="button-pick paper">
            <button aria-label="paper" @click="handleButtonClick('paper')"></button>
        </div>
        <div class="button-pick scissors">
            <button aria-label="scissors" @click="handleButtonClick('scissors')"></button>
        </div>
        <div class="button-pick rock">
            <button aria-label="rock" @click="handleButtonClick('rock')"></button>
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
        handleButtonClick(choice) {
            // update local userChoice & randomChoice
            this.choices.userChoice = choice
            this.updateRandomChoice()

            // send local choices object to App
            this.$emit("choices", this.choices)

            // step1 is done, go to next step
            this.$emit("nextStep")
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