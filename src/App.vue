<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
    HelloWorld
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
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

footer h2 {
    margin: 30px auto;
    text-align: center;

    font-family: Arial, sans-serif;
    font-size: 32px;
    line-height: 36px;
    color: #434344;
}

section {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-gap: 25px;

    margin: 0 auto;
    width: 595px;
}

.flip {
    perspective: 600px;
}

.card {
    position: relative;

    display: flex;
    justify-content: center;
    align-items: center;

    height: 130px;
    width: 130px;

    font-size: 75px;
    box-sizing: border-box;
    border-radius: 9px;
    box-shadow: 1px 1px 5px rgba(0, 0, 0, 0.5);
    background-color: white;

    transition: transform .3s linear;
    transform-style: preserve-3d;
}

.card_back {
    height: 100%;
    width: 100%;
    box-sizing: border-box;

    position: absolute;
    backface-visibility: hidden;
    background: linear-gradient(to top right, #22AB93, #19668D);
    border: 5px solid white;
    border-radius: 9px;
}

.card_face {
    display: flex;
    justify-content: center;
    align-items: center;

    height: 100%;
    width: 100%;

    background-color: white;
    border-radius: 9px;
}

.is_flipped {
    transform: rotateY(180deg);
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
