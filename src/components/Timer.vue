<template>
    <div id="timer">
        <h2 >{{timeShow}}</h2>
    </div>

</template>

<script>
    export default {
        name: 'Timer',
        data () {
            return {
                timeNow: 59
            }
        },
        props: {
          msg: String
      },
      computed: {
          timeShow () {
              let timeStr = String(this.timeNow);

              return `0:${timeStr}`;
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
