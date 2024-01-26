<template>
    <header class="header container-narrow">
        <div class="logo">
            <img src="../assets/images/logo.svg" alt="Rock Paper Scissors">
        </div>
        <div class="score">
            <p class="fs-500 txt-neutral-900 fw-500">Score</p>
            <span class="txt-center txt-neutral-800 fw-700" ref="score">
                {{ headerScore }}
            </span>
        </div>
    </header>
</template>

<script>

export default {
    props: ['score'],
    data() {
        return {
            headerScore: 0
        }
    },
    watch: {
        score(newValue, oldValue) {
            setTimeout(() => {
                this.headerScore = newValue
            }, 4000)
        }
    }
}
</script>