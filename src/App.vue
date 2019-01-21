<template>
<div id="wrap">
    <section>
        <MainField
            v-for="(card, i) in shuffled"
            :key="i + 1"
            :msg="card"
            @hui="handler"
        >
        </MainField>
    </section>
     <Timer></Timer>
</div>
</template>

<script>
import MainField from './components/MainField.vue'
import Timer from './components/Timer.vue'

export default {
  id: 'wrap',
  name: 'wrap',
  components: {
    MainField,
    Timer
  },
  data () {
      return {
          cards: elArr,
          isOpenOne: false,
          isOpenTwo: false,
          firstCard: '',
          secondCard: ''
      }
  },
  methods: {
      handler () {
          alert(1);
          if (!this.isOpenOne/* && inverter("is_open1")*/) { // <---------open first card
              // add condition if the cards were opened incorrectly
              if (this.firstCard/* && !compareCards()*/) {
                  //firstCard.parentNode.classList.remove("is_flipped");
                  //firstCard.classList.remove("is_open1", "is_wrong");
                  //secondCard.parentNode.classList.remove("is_flipped");
                  //secondCard.classList.remove("is_open2", "is_wrong");
                  this.secondCard = undefined;
              }

              this.isOpenOne = !this.isOpenOne;

              /*firstCard = form.querySelector(".is_open1");

          } else if (!isOpenTwo && inverter("is_open2")) { // <--open second card
              isOpenTwo = !isOpenTwo;

              secondCard = form.querySelector(".is_open2");

              if (compareCards()) {
                  firstCard.classList.add("is_right");
                  secondCard.classList.add("is_right");
                  firstCard.classList.remove("is_open1");
                  secondCard.classList.remove("is_open2");

                  isOpenOne = !isOpenOne;
                  isOpenTwo = !isOpenTwo;
                  firstCard = undefined;

                  rightPairs++;

              } else {
                  firstCard.classList.add("is_wrong");
                  secondCard.classList.add("is_wrong");

                  isOpenOne = !isOpenOne;
                  isOpenTwo = !isOpenTwo;
              }*/
          }
      }
  },
  computed: {
      shuffled () {
          let shuffledCards = [...this.cards].sort(() => Math.random() - 0.5);

          return shuffledCards;
      }
  },
  watch: {
      //logic of cards
  }
}

let elArr = [
    '🐻', '🐼', '🐨', '🐯', '🦁', '🐻', '🐼', '🐨', '🐯', '🦁', '🐹', '🐹'
];
</script>

<style>
* {
    margin: 0;
    padding: 0;
}

body {
    background-color: #CFD0CF;
}

header h1 {
    margin: 40px auto;
    text-align: center;

    font-family: Arial, sans-serif;
    font-size: 42px;
    line-height: 47px;
    color: #434344;
}



section {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-gap: 25px;

    margin: 0 auto;
    width: 595px;
}

.is_wrong {
    background-color: #F44336;
}
.is_right {
    background-color: #5AD66F;
}

.substrate {
    position: fixed;

    left: 0;
    top: 0;
    width: 100%;
    height: 100%;

    background-color: rgba(255, 255, 255, 0.5);
}

.popup {
    position: relative;

    width: 350px;
    height: auto;

    margin: 0 auto;
    margin-top: 50vh;
    transform: translateY(-50%);
    padding-top: 30px;
    padding-bottom: 30px;

    background-color: white;

    font-family: Arial, sans-serif;
    font-size: 48px;
    font-weight: bold;
    text-align: center;
}

.popup span {
    display: inline-block;

    animation-name: stretch;
    animation-duration: .6s;
    animation-timing-function: ease;
    animation-iteration-count: infinite;
    animation-direction: alternate;
}

.popup span:first-child {
    animation-delay: .01s;
}

.popup span:nth-child(3n+1) {
    animation-delay: .2s;
}

.popup span:nth-child(3n+2) {
    animation-delay: .4s;
}

.btn {
    display: block;

    margin: 40px auto 0;
    padding: 0 30px;

    width: auto;
    height: 40px;
    box-sizing: border-box;

    font-size: 20px;
    font-weight: bold;
    border-radius: 10px;
    box-shadow: 1px 1px 1px rgba(0, 0, 0, 0.5);
    border: 0;
    background: linear-gradient(to right, #19668D, #22AB93);
    color: white;
}

.btn_pressed {
    box-shadow: 2px 1px 8px rgba(0, 0, 0, 0.5) inset;
    outline: none;
}

@keyframes stretch {
    to {
        transform: scaleY(2) translateY(-10px);
    }
}
</style>
