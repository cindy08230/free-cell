<template>
  <div class="start">
      <div class="start__content">
        <div class="start__content__king">
          <img src="../assets/pic-king.svg">
        </div>
        <div class="start__content__logo">
          <img src="../assets/logo.svg">
        </div>
        <div
          class="start__content__button"
          @click="clickStart">
          <p class="start__content__button__text">開始遊戲</p>
        </div>
      </div>
      <div class="start__background">
        <img src="../assets/bg-img.svg">
      </div>
    </div>
</template>

<script>
export default {
  name: 'Start',
  methods:{
    clickStart(){
      this.$emit('click-start')
    }
  }
}
</script>

<style lang="sass" scoped>
p
  margin: 0

img
  display: block

.start
  width: 100%
  height: 100%
  position: relative
  display: flex
  justify-content: center

  &__content
    margin-top: 160px
    display: flex
    flex-direction: column
    align-items: center

    &__king
      width: 78px
      margin-bottom: 20px

    &__logo
      width: 265px

    &__button
      width: 185px
      height: 55px
      border: 3px solid #82D5E8
      border-radius: 50px
      display: flex
      align-items: center
      justify-content: center
      margin-top: 45px
      cursor: pointer

      &__text
        color: #82D5E8
        font-size: 26px

  &__background
    width: 100%
    position: absolute
    bottom: -10%
</style>
