<template>
	<div class="notice">
		<div class="notice__mask"></div>
		<div class="notice__wrap">
			<div class="notice__wrap__image">
				<img src="../assets/pic-castle.svg">
			</div>
			<p class="notice__wrap__title">重玩</p>
			<p class="notice__wrap__text">將會遺失現在的進度，確定重玩嗎？</p>
			<div class="notice__wrap__buttons">
				<div
					class="button"
					@click="restart">重新此關</div>
				<div
					class="button"
					@click="continueGame">返回繼續玩</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
  name: 'Replay',
  methods:{
		continueGame() {
			this.$emit('replay-continue')
		},
		restart() {
			this.$emit('replay-restart')
		}
  }
}
</script>

<style lang="sass" scoped>
img
	display: block

p
	margin: 0

.notice
	width: 100%
	height: 100%
	position: absolute
	display: flex
	justify-content: center
	align-items: center
	z-index: 999

	&__mask
		position: absolute
		width: 100%
		height: 100%
		background-color: #404040
		opacity: 0.4

	&__wrap
		position: relative
		width: 420px
		height: 220px
		background-color: #F7F6F5
		border: 5px solid #82D5E8
		border-radius: 15px
		z-index: 9999
		display: flex
		flex-direction: column
		align-items: center
		
		&__image
			position: absolute
			top: -30%

		&__title
			font-size: 26px
			color: #82D5E8
			margin-top: 45px
			margin-bottom: 5px

		&__text
			font-size: 15px
			color: #58554F
			margin-bottom: 26px

		&__buttons
			display: flex

			.button
				width: 116px
				height: 50px
				background-color: #FFFFFF
				border-radius: 10px
				color: #58554F
				display: flex
				align-items: center
				justify-content: center
				cursor: pointer

				&:not(:last-of-type)
					margin-right: 36px

				&:hover
					background-color: #82D5E8
					color: #FFFFFF

</style>
