<template>
    <div class="step-3">
        <div>
            <p>You picked</p>
            <div class="selected" :class="userChoice">
                <div></div>
            </div>
        </div>
        <div>
            <span class="message">
                {{ generateMessage }}
            </span>
            <button class="button" data-style="primary" @click="handleButton">Play again</button>
        </div>
        <div>
            <p>The house picked</p>
            <div class="selected" :class="randomChoice">
                <div></div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ["userChoice", "randomChoice", "winner"],

    methods: {
        handleButton() {
            this.$emit("playAgain")
        }
    },
    computed: {
        generateMessage(){
            if(this.winner === "user"){
                return "You win"
            } else if(this.winner === "notUser"){
                return "You lose"
            } else if(this.winner === "draw") {
                return "It's a draw"
            }
        }
    },
}
</script>