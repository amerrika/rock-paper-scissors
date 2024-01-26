<template>
    <div class="step-2">
        <div>
            <p>You picked</p>
            <div :class="userChoiceClass">
                <div></div>
            </div>
        </div>
        <div>
            <p>The house picked</p>
            <div class="placeholder__outer" v-if="counter !== 0">
                <div class="placeholder__inner">
                    <span>
                        {{ counter }}
                    </span>
                </div>
            </div>
            <div :class="randomChoiceClass" v-else>
                <div></div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    props: ["userChoice", "randomChoice"],

    data() {
        return {
            counter: undefined,
        }
    },

    methods: {
        startCountdown(time) {
            let seconds = time

            const interval = setInterval(() => {
                seconds--;
                this.counter = seconds
                if (seconds < 1) {
                    clearInterval(interval)
                }
            }, 600);
        },
    },

    created() {
        // Countdown for placeholder
        this.startCountdown(4)

        setTimeout(() => {
            this.$emit("nextStep")
        }, 3700)
    },

    computed: {
        userChoiceClass() {
            return `selected ${this.userChoice}`
        },
        randomChoiceClass() {
            return `selected ${this.randomChoice}`
        },
    }
}
</script>