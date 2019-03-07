<template>
    <div class="user-wrapper">
        <header>
            <slot name="welcome"></slot>
            <h3>Game results:</h3>
            <span v-if="msgTime > 0">Вы прошли игру за {{msgTime}} секунды</span>
        </header>
    </div>
</template>

<script>
export default {
  name: 'UserInfo',
  data () {
      return {

      }
  },
  props: {
      msgTime: Number
  },
  methods: {

  },
  watch: {

  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.user-wrapper {
    position: fixed;
    bottom: 100px;
    left: 100px;
}
</style>
