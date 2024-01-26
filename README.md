# Frontend Mentor - Rock, Paper, Scissors solution

- This is my solution to the [Rock, Paper, Scissors challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/rock-paper-scissors-game-pTgwgvgH).
- After I finished Multi-step form challenge I wanted immediately to do another challenge to keep practicing and learning Vue.js.

## The challenge

Users should be able to:

- View the optimal layout for mobile and desktop screen.
- Play Rock, Paper, Scissors against the computer

## Built with

- [Vue.js](https://vuejs.org/) - JS framework
- [SCSS](https://sass-lang.com/) - CSS preprocessor

### What I learned

- I learned about **Teleport** option in Vue 3. I created a button for opening a modal inside Modal.vue component, because it belongs to it logically, but I used Teleport to display the button in the footer of the page, to better match the design.

- I learned basics of **Watchers** in Vue and I gained a better understading of **Lifecycle Hooks**. For example, I learned that at the point when created() is called that data, methods, computed and watchers have alredy been set up, so at one point I called some function for updating data inside of created() hook and then realized using computed properties is a better solution. Another example, in my App.vue component, I needed to compare userChoice and randomChoice every time I get these values back from Step1 component, so first I tried writing the necessary code inside the beforeUpdate() hook but then I realized this is a bad solution because this hook is called every time any reactive data is changed. Searching for a better solution I learned about watch option and used it instead.

- I've been using Sass in my projects but have not used the 'placeholder' selectors. In this project, I created few placeholders that I used for my buttons (the ones in Step1 for selecting the option) as well as for elements that display the selected options in the next steps of the app. Using these placeholders I made my css code a bit less repetetive and a bit more readable:

```scss
.button-pick {
  // button-pick is a div, inside this div is a <button>
  @extend %choice-wrapper;
  width: 13rem;
  height: 13rem;
  @include mq(small) {
    width: 18rem;
    height: 18rem;
  }

  button {
    // common styles for all pick buttons
    @extend %choice-inner;
    cursor: pointer;
    height: 10rem;
    width: 10rem;
    @include mq(small) {
      width: 13rem;
      height: 13rem;
    }
  }
}

.selected {
  @extend %choice-wrapper;
  width: 13rem;
  height: 13rem;
  @include mq(small) {
    width: 20rem;
    height: 20rem;
  }

  & > :first-child {
    @extend %choice-inner;
    width: 10rem;
    height: 10rem;
    @include mq(small) {
      width: 15rem;
      height: 15rem;
    }
  }
}

.button-pick,
.selected {
  &.scissors {
    background-image: $radial-yellow;
    & > * {
      background-image: $bg-image-scissors;
    }
  }

  &.paper {
    background-image: $radial-blue;
    & > * {
      background-image: $bg-image-paper;
    }
  }

  &.rock {
    background-image: $radial-red;
    & > * {
      background-image: $bg-image-rock;
    }
  }
}
```

## Continued development

- To read about Vue Transition and to try implementing it in this project to make smoother transitions and better user experience.

## Useful resources

- https://stackoverflow.com/questions/53730900/more-efficient-choice-comparison-for-rock-paper-scissors
- https://stackoverflow.com/questions/42133894/vue-js-how-to-properly-watch-for-nested-data
- https://stackoverflow.com/questions/44983349/what-is-the-difference-between-updated-hook-and-watchers-in-vuejs
