<template>
  <div id="free-cell">
    <Start
      v-if="nowPage === 'start'"
      v-on:click-start="changePage"/>
    <Game v-if="nowPage === 'game'"/>
  </div>
</template>

<script>
import Start from './components/Start'
import Game from './components/Game'

export default {
  name: 'FreeCell',
  components: {
    Start,
    Game
  },
  data () {
    return {
      nowPage: 'start'
    }
  },
  methods: {
    changePage(){
      this.nowPage = 'game'
    }
  }
}
</script>
<style lang="sass" scoped>
#free-cell
  height: 100vh
  overflow: hidden
</style>
