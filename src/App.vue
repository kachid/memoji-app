<template>
    <div id="wrap">
        <section>
            <MainField
                v-for="(card, i) in shuffled"
                :key="i + 1"
                :msg="card"
                :reload="reload"
                @clickCard="handler"
                @runTimer.once="firstClick = true"
            >
            </MainField>
        </section>
         <Timer
             v-show="showT"
             @showTimer="showT = true"
             @showWindow="popupWindow"
             :firstClick="firstClick"
             :rightPairs="rightPairs"
             >
         </Timer>
         <Modal v-if="showModal"
                @close="closeWindow"
                :message="msgBtn"
         >
            <h3 slot="header">{{headerPopup}}</h3>
        </Modal>
    </div>
</template>

<script>
import MainField from './components/MainField.vue'
import Timer from './components/Timer.vue'
import Modal from './components/Modal.vue'

export default {
  id: 'wrap',
  name: 'wrap',
  components: {
    MainField,
    Timer,
    Modal
  },
  data () {
      return {
          cards: elArr,
          isOpenOne: false,
          isOpenTwo: false,
          firstCard: '',
          secondCard: '',
          rightPairs: 0,
          firstClick: false,
          showModal: false,
          headerPopup: '',
          msgBtn: '',
          reload: false,
          showT: false
      }
  },
  methods: {
      handler (cardEl) {
          if (this.isOpenOne === false && cardEl.is_flipped === false) { // <---------open first card
              // add condition if the cards were opened incorrectly
              if (this.firstCard && !this.compareCards) {
                  this.firstCard.is_flipped = false;
                  this.firstCard.is_wrong = false;
                  this.secondCard.is_flipped = false;
                  this.secondCard.is_wrong = false;
                  this.secondCard = '';
              }

              this.isOpenOne = true;
              this.firstCard = cardEl;

          } else if (this.isOpenTwo === false && cardEl.is_flipped === false) { // <--open second card
              this.isOpenTwo = true;
              this.secondCard = cardEl;

              //both cards are open and now we need to compare them
              if (this.compareCards) {
                  this.firstCard.is_right = true;
                  this.secondCard.is_right = true;
                  //clear first card
                  this.firstCard = '';
                  //increase counter
                  this.rightPairs++;

              } else {
                  this.firstCard.is_wrong = true;
                  this.secondCard.is_wrong = true;
              }

              this.isOpenOne = false;
              this.isOpenTwo = false;
          }
      },
      popupWindow (message) {
          this.showModal = true;
          this.headerPopup = message[0];
          this.msgBtn = message[1];
      },

      closeWindow () {
          this.showModal = false;
          this.reload = true;
      },
      shuffledThisCards (cardsDeck) {
          return [...cardsDeck].sort(() => Math.random() - 0.5)
      }
  },
  computed: {
      shuffled () {
          return this.shuffledThisCards(this.cards);
      },
      compareCards () {
          return this.firstCard.msg === this.secondCard.msg;
      }
  },
  watch: {
      reload () {
          this.shuffledThisCards(this.cards);

          this.isOpenOne = false;
          this.isOpenTwo = false;
          this.FirstClick = false;
          this.firstCard = undefined;
          this.secondCard = undefined;
          this.rightPairs = 0;
          this.showT = false;
      },
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
