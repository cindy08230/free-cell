<template>
	<div class="notice">
		<div class="notice__mask"></div>
		<div class="notice__wrap">
			<div class="notice__wrap__image">
				<img src="../assets/pic-rule.svg">
			</div>
			<p class="notice__wrap__title">怎麼玩</p>
			<p class="notice__wrap__text">
				新接龍(Freecell)是一款使用52張牌進行的單人卡片遊戲，遊戲目標是將整副牌搬到右上角的四個空欄中。 將一副標準52張撲克牌洗牌，再分別置於8個欄目，其中4個欄目有7張紙牌，其餘4個欄目有6張紙牌，每張撲克牌皆要以翻開顯示。 另外還有右上角四個本位欄框、左上角四個空白欄。 紙牌 A、2 可立即放到本位欄框，而其他同花色的牌則可以由小到大依序疊上去。只要將所有的牌都放到本位欄框中，就成功了。 空白欄框為四個放牌位置。每個欄框都可任意放一張紙牌。 移動紙牌的規則如下： 將紙牌移動到某一欄時的順序必須為由大到小，而且是不同的顏色（即黑、紅兩種顏色）。 將紙牌移至本位欄框時，必須以相同花色，將牌按照從低（A）到高（K）的順序移動。 某欄最底端的紙牌可移到空白欄框、另一欄的最底端或 本位欄框。 空白欄框中的紙牌可移至某一欄的最底端或本位欄框。
			</p>
			<div class="notice__wrap__buttons">
				<div
					class="button"
					@click="closeAleart">關閉</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
  name: 'HowToPlay',
  methods:{
		closeAleart() {
			this.$emit('close-aleart')
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
		width: 444px
		height: 530px
		background-color: #F7F6F5
		border: 5px solid #82D5E8
		border-radius: 15px
		z-index: 9999
		display: flex
		flex-direction: column
		align-items: center
		
		&__image
			position: absolute
			top: -8%

		&__title
			font-size: 26px
			color: #82D5E8
			margin-top: 45px
			margin-bottom: 5px

		&__text
			font-size: 15px
			line-height: 25px
			color: #58554F
			margin-bottom: 26px
			width: 329px
			height: 320px
			overflow: scroll

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
