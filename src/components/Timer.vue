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
                timeNow: 59,
                timer: null
            }
        },
        props: {
          firstClick: Boolean
        },
        methods: {
            startTimer () {
                this.timer = setInterval(() => {
                    this.timeNow--;
                }, 1000);
            },
            stopTimer () {
                clearInterval(this.timer);
            }
        },
        computed: {
            timeShow () {
                let timeStr = '';
                timeStr = String(this.timeNow);

                if (this.timeNow < 1) {
                    this.stopTimer();
                    return `00:00`
                } else if (this.timeNow < 10) {
                    return `00:0${timeStr}`;
                } else {
                    return `00:${timeStr}`;
                }

                /*
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

            },

        },
        watch: {
            firstClick() {
                this.startTimer();
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
