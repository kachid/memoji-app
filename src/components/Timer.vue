<template>
    <div id="timer">
        <h2 >{{msg}}</h2>
        <button @click="some">check</button>
    </div>

</template>

<script>
    export default {
        name: 'Timer',
        props: {
          msg: String
        },
        methods: {
            some() {
                alert(1);
            }
        }
    }
</script>

<style scoped>
    h2 {
        margin: 30px auto;
        text-align: center;

        font-family: Arial, sans-serif;
        font-size: 32px;
        line-height: 36px;
        color: #434344;
    }
</style>
