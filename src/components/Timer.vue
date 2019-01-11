<template>
    <h2 id="timer">{{msg}}</h2>
</template>

<script>
    export default {
        name: 'Timer',
        props: {
          msg: String
        }
    }
</script>

<style scoped>
    #timer {
        margin: 30px auto;
        text-align: center;

        font-family: Arial, sans-serif;
        font-size: 32px;
        line-height: 36px;
        color: #434344;
    }
</style>
