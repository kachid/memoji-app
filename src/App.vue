<template>
<div id="wrap">
    <section>
        <MainField v-for="n in 12" :key="n"></MainField>
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

}
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
