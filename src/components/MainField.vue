<template>
    <figure class="flip"

            >
        <div class="card"
             @click="setActiveClass"
             v-bind:class="{ is_flipped: isActive }"
             >
            <div class="card_back"></div>
            <span class="card_face">{{msg}}</span>
        </div>
    </figure>
</template>

<script>
export default {
  name: 'MainField',
  data: function () {
      return {
          isActive: false
      }
  },
  props: {
    msg: String
  },
  methods: {
      setActiveClass() {
          this.$emit('clickCard', this);
          this.isActive = !this.isActive;
      },
  },
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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


</style>
