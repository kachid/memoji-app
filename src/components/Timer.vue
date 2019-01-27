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
          isOpenOne: Boolean
        },
        methods: {
            runTimer () {
                 setInterval(() => this.timeNow--, 1000);
            }
        },
        computed: {
            timeShow () {
                /*let i = 59,
                    iStr = '';

                let timerId = setTimeout(function tick() {
                    if (i === 0) {
                      popupWindow('Lose', 'Try again');
                    } else if (rightPairs === 6) {
                      popupWindow('Win', 'Play again');
                    } else {
                      timerId = setTimeout(tick, 1000);
                    }

                    if (i < 10) {
                      iStr = '0' + i;
                    } else {
                      iStr = '' + i;
                    }

                    timer.innerHTML = '00:' + iStr;

                    i--;

                }, 1000);*/

                let timeStr = String(this.timeNow);

                if (this.isOpenOne) {
                    this.runTimer ();
                }

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
