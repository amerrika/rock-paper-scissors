<template>
  <Header :score="dynamic.totalScore" />
  <main class="container-narrow">
    <Step1 v-if="dynamic.currentStep === 1" :possible-choices="possibleChoices" @choices="updateChoices"
      @nextStep="goToNextStep" />
    <Step2 v-if="dynamic.currentStep === 2" v-bind="dynamic.choices" @nextStep="goToNextStep" />
    <Step3 v-if="dynamic.currentStep === 3" v-bind="dynamic.choices" :winner="dynamic.winner"
      @playAgain="goToInitialStep" />
  </main>
  <Footer />
  <Modal />
</template>

<script>
// import sass
import "./sass/main.scss";
// import vue components
import Header from "./components/Header.vue"
import Footer from "./components/Footer.vue"
import Modal from "./components/Modal.vue"
import Step1 from "./components/Step1.vue"
import Step2 from "./components/Step2.vue"
import Step3 from "./components/Step3.vue"

export default {
  name: "App",
  components: {
    Header,
    Footer,
    Modal,
    Step1,
    Step2,
    Step3
  },
  data() {
    return {
      // dynamic - data shared between App.vue and its children
      dynamic: {
        totalScore: 0,
        currentStep: 1,
        winner: undefined,
        choices: {
          userChoice: undefined,
          randomChoice: undefined,
        }
      },
      // static - data should not be changed
      possibleChoices: ["paper", "scissors", "rock"]
    };
  },
  methods: {
    goToNextStep() {
      this.dynamic.currentStep++
    },
    goToInitialStep() {
      this.dynamic.currentStep = 1
    },
    updateChoices(obj) {
      this.dynamic.choices.userChoice = obj.userChoice
      this.dynamic.choices.randomChoice = obj.randomChoice
    },
    increaseTotalScore() {
      this.dynamic.totalScore++
    },
    decreaseTotalScore() {
      // Only if totalScore is > 0
      if (this.dynamic.totalScore > 0) {
        this.dynamic.totalScore
      }
    },
  },
  computed: {
    userChoice() {
      // to be watched
      return this.dynamic.choices.userChoice
    },
  },
  watch: {
    // After receiving userChoice & randomChoice from Step1, we want to compare them
    userChoice() {
      const { choices } = this.dynamic

      const userIndex = this.possibleChoices.indexOf(choices.userChoice)
      const randomIndex = this.possibleChoices.indexOf(choices.randomChoice)

      // if it's not a tie
      if (userIndex !== randomIndex) {
        // user is a winner
        if (userIndex === (randomIndex + 1) % 3) {
          this.increaseTotalScore()
          this.dynamic.winner = "user"
          // user is NOT a winner
        } else {
          this.decreaseTotalScore()
          this.dynamic.winner = "notUser"
        }
        // if it's a tie
      } else {
        this.dynamic.winner = "draw"
      }

    }
  },
};
</script>
