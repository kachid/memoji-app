<template>
    <v-app>
    <div id="wrap">
        <header>
            <UserInfo :msgTime="complitedTime">
                <h3 slot="welcome">Hi, {{userID}}!</h3>
                <h4 slot="results"
                    v-for="(result, i) in this.complitedGames"
                    :key="i"
                    >
                    {{i}}: - {{result}} seconds
                </h4>
            </UserInfo>
            <h1>Memoji</h1>
            <div class="wrapper-button">
                <v-btn>Log in</v-btn>
            </div>
        </header>
        <v-container grid-list-md>
            <v-layout row wrap>
                <v-flex v-for="(card, i) in cards" xs3>
                    <MainField

                        :key="i + 1"
                        :msg="card"
                        :flipCard="reset"
                        @clickCard="handler"
                    >
                    </MainField>
                </v-flex>
            </v-layout>
        </v-container>
         <Timer
             v-show="showT"
             @showTimer="showT = true"
             @stopTimer="startTimer = false"
             @showWindow="popupWindow"
             @playTime="setPlayTime"
             :runTimer="startTimer"
             :rightPairs="rightPairs"
             >
         </Timer>

         <Modal v-if="showModal"
                @close="closeWindow"
                :message="msgBtn"
         >
            <h3 slot="header">You {{headerPopup}}!</h3>
            <h3 slot="body">{{userID}}, you completed this game in {{complitedTime}} seconds</h3>
        </Modal>
    </div>
    </v-app>
</template>

<script>
import MainField from './components/MainField.vue'
import Timer from './components/Timer.vue'
import Modal from './components/Modal.vue'
import UserInfo from './components/UserInfo.vue'

export default {
  id: 'wrap',
  name: 'wrap',
  components: {
    MainField,
    Timer,
    Modal,
    UserInfo
  },
  data () {
      return {
          cards: elArr,
          isOpenOne: false,
          isOpenTwo: false,
          firstCard: '',
          secondCard: '',
          rightPairs: 0,
          startTimer: false,
          showT: false,
          showModal: false,
          headerPopup: '',
          msgBtn: '',
          reset: false,
          complitedTime: 0,
          complitedGames: [],
          userID: "Unknow user"
      }
  },
  created: function () {
      this.cards = this.shuffledThisCards(this.cards);
  },
  methods: {
      startGame () {
        this.startTimer = true;
      },
      handler (cardEl) {
          this.startGame();
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
          this.reload();
      },
      shuffledThisCards (cardsDeck) {
          return [...cardsDeck].sort(() => Math.random() - 0.5);
      },
      reload () {
          // перемешиваем колоду
          this.cards = this.shuffledThisCards(this.cards);

          //обнуляем логику
          this.isOpenOne = false;
          this.isOpenTwo = false;
          this.firstCard = '';
          this.secondCard = '';
          this.rightPairs = 0;

          //обнуляем таймер
          this.startTimer = false;
          this.showT = false;

          //переворачиваем карты рубашкой вверх
          this.reset = !this.reset;
      },
      setPlayTime (time) {
          this.complitedTime = 60 - time;
          this.complitedGames.push(this.complitedTime);
      }
  },
  computed: {
      compareCards () {
          return this.firstCard.msg === this.secondCard.msg;
      }
  },
  watch: {

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

header {
    display: flex;
    justify-content: space-around;
    align-content: center;
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
