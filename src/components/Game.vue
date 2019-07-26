<template>
  <div class="game">
		<HowToPlay
			v-if="isHowToPlayShow"
			v-on:close-aleart="isHowToPlayShow = false"/>
		<Pause
			v-if="isPauseShow"
			v-on:pause-continue="continueTime"
			v-on:pause-restart="reStart"/>
		<Replay
			v-if="isReplayShow"
			v-on:replay-continue="continueTime"
			v-on:replay-restart="reStart"/>
		<div class="game__header">
			<div class="game__header__logo">
				<img src="../assets/logo.svg">
			</div>
			<div class="game__header__menu">
				<div class="item"
					@click="pauseTime('replay')">
					<div class="item__image">
						<img src="../assets/icon_11972.svg">
					</div>
					<p class="item__text">重玩</p>
				</div>
				<div class="item">
					<div class="item__image">
						<img src="../assets/Path_198.svg">
					</div>
					<p class="item__text">上一步</p>
				</div>
				<div
					class="item"
					@click="pauseTime('pause')">
					<div class="item__image">
						<img src="../assets/icon_15460.svg">
					</div>
					<p class="item__text">暫停</p>
				</div>
			</div>
		</div>
		<div class="game__wrap">
			<div class="game__wrap__top">
				<div class="column">
					<div class="column__card left-card"></div>
					<div class="column__card left-card"></div>
					<div class="column__card left-card"></div>
					<div class="column__card left-card"></div>
				</div>
				<div class="column">
					<div class="column__card right-card">
						<img src="../assets/icon_13999-73_white.svg">
					</div>
					<div class="column__card right-card">
						<img src="../assets/Group_117-10_white.svg">
					</div>
					<div class="column__card right-card">
						<img src="../assets/icon_14017-64_white.svg">
					</div>
					<div class="column__card right-card">
						<img src="../assets/icon_14002-70_white.svg">
					</div>
				</div>
			</div>
			<div class="game__wrap__down">
				<div class="game__wrap__down__wrap">
					<div
						v-for="(row, rowKey, rowIndex) in belowLeft"
						:key="`left-row-${rowIndex}`"
						@drop="drop($event, rowKey)"
						@dragover="allowDrop($event)"
						class="row left-row">
            <div
              v-for="(card, cardKey, cardIndex) in row"
							:key="`${rowIndex}-${cardKey}-${card.suit}`"
							:class="[`suit-${card.suit}`, `num-${cardIndex}`]"
							@dragstart="dragStart($event, card)"
							:draggable="Object.keys(row).length === cardIndex+1 ? true : false"
							class="row__card">
							<div class="row__card__text left-txt">
								<p v-text="card.txt"></p>
								<img
									v-if="card.suit === 'S'"
									src="../assets/suit-S.svg"
									class="small-suit">
								<img
									v-if="card.suit === 'H'"
									src="../assets/suit-H.svg"
									class="small-suit">
								<img
									v-if="card.suit === 'C'"
									src="../assets/suit-C.svg"
									class="small-suit">
								<img
									v-if="card.suit === 'D'"
									src="../assets/suit-D.svg"
									class="small-suit">
							</div>
							<div class="row__card__suits">
								<div
									v-for="i in card.num+1"
									v-if="card.num < 10"
									:key="i"
									:class="{
										'card-middle': card.num % 2 === 0 && i === 3 ,
										'card-full': card.num < 3
									}"
									class="row__card__suits__suit">
									<img
										v-if="card.num <= 9 && card.suit === 'S'"
										src="../assets/suit-S.svg"
										class="normal-suit">
									<img
										v-if="card.num <= 9 && card.suit === 'H'"
										src="../assets/suit-H.svg"
										class="normal-suit">
									<img
										v-if="card.num <= 9 && card.suit === 'C'"
										src="../assets/suit-C.svg"
										class="normal-suit">
									<img
										v-if="card.num <= 9 && card.suit === 'D'"
										src="../assets/suit-D.svg"
										class="normal-suit">
								</div>
								<div
									v-for="i in 2"
									v-if="card.num >= 10"
									:key="i"
									:class="{'upsite-down': i === 2}"
									class="row__card__suits__special">
									<img
										v-if="card.num === 10"
										src="../assets/pic-elf.svg"
										class="special-suit">
									<img
										v-if="card.num === 11"
										src="../assets/pic-knight.svg"
										class="special-suit">
									<img
										v-if="card.num === 12"
										src="../assets/pic-king.svg"
										class="special-suit">
								</div>
								
							</div>
              <div class="row__card__text right-txt">
								<p v-text="card.txt"></p>
								<img
									v-if="card.suit === 'S'"
									src="../assets/suit-S.svg"
									class="small-suit">
								<img
									v-if="card.suit === 'H'"
									src="../assets/suit-H.svg"
									class="small-suit">
								<img
									v-if="card.suit === 'C'"
									src="../assets/suit-C.svg"
									class="small-suit">
								<img
									v-if="card.suit === 'D'"
									src="../assets/suit-D.svg"
									class="small-suit">
							</div>
						</div>
					</div>
				</div>
				<div class="game__wrap__down__wrap">
					<div
						v-for="(row, rowKey, rowIndex) in belowRight"
						:key="`right-${rowKey}-${rowIndex}`"
						@drop="drop($event, rowKey)"
						@dragover="allowDrop($event)"
						class="row right-row">
            <div
              v-for="(card, cardKey, cardIndex) in row"
							:key="`${rowIndex}-${cardKey}-${card.suit}`"
							:class="[`suit-${card.suit}`, `num-${cardIndex}`]"
							@dragstart="dragStart($event, card)"
							:draggable="Object.keys(row).length === cardIndex+1 ? true : false"
							class="row__card">
							<div class="row__card__text left-txt">
								<p v-text="card.txt"></p>
								<img
									v-if="card.suit === 'S'"
									src="../assets/suit-S.svg"
									class="small-suit">
								<img
									v-if="card.suit === 'H'"
									src="../assets/suit-H.svg"
									class="small-suit">
								<img
									v-if="card.suit === 'C'"
									src="../assets/suit-C.svg"
									class="small-suit">
								<img
									v-if="card.suit === 'D'"
									src="../assets/suit-D.svg"
									class="small-suit">
							</div>
							<div class="row__card__suits">
								<div
									v-for="i in card.num+1"
									v-if="card.num < 10"
									:key="i"
									:class="{
										'card-middle': card.num % 2 === 0 && i === 3 ,
										'card-full': card.num < 3
									}"
									class="row__card__suits__suit">
									<img
										v-if="card.num <= 9 && card.suit === 'S'"
										src="../assets/suit-S.svg"
										class="normal-suit">
									<img
										v-if="card.num <= 9 && card.suit === 'H'"
										src="../assets/suit-H.svg"
										class="normal-suit">
									<img
										v-if="card.num <= 9 && card.suit === 'C'"
										src="../assets/suit-C.svg"
										class="normal-suit">
									<img
										v-if="card.num <= 9 && card.suit === 'D'"
										src="../assets/suit-D.svg"
										class="normal-suit">
								</div>
								<div
									v-for="i in 2"
									v-if="card.num >= 10"
									:key="i"
									:class="{'upsite-down': i === 2}"
									class="row__card__suits__special">
									<img
										v-if="card.num === 10"
										src="../assets/pic-elf.svg"
										class="special-suit">
									<img
										v-if="card.num === 11"
										src="../assets/pic-knight.svg"
										class="special-suit">
									<img
										v-if="card.num === 12"
										src="../assets/pic-king.svg"
										class="special-suit">
								</div>
								
							</div>
              <div class="row__card__text right-txt">
								<p v-text="card.txt"></p>
								<img
									v-if="card.suit === 'S'"
									src="../assets/suit-S.svg"
									class="small-suit">
								<img
									v-if="card.suit === 'H'"
									src="../assets/suit-H.svg"
									class="small-suit">
								<img
									v-if="card.suit === 'C'"
									src="../assets/suit-C.svg"
									class="small-suit">
								<img
									v-if="card.suit === 'D'"
									src="../assets/suit-D.svg"
									class="small-suit">
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
		<div class="game__footer">
			<div class="game__footer__hinit">
				<div class="game__footer__hinit__logo">
					<img src="../assets/Group_213.svg">
				</div>
				<p class="game__footer__hinit__text">提示</p>
			</div>
			<p
				class="game__footer__time"
				v-text="showNowTime"></p>
			<p class="game__footer__score">Score: 02</p>
		</div>
  </div>
</template>

<script>
import Pause from './Pause'
import Replay from './Replay'
import HowToPlay from './HowToPlay'
Array.prototype.shuffle = function(){
  var pivot = this.length
  while(pivot--){
    var ri = Math.floor(Math.random()*pivot)
    var temp = this[ri];this[ri]=this[pivot];this[pivot]=temp
  }
  return this
}
let dom = null
export default { 
	name: 'Game',
	components: {
		Pause,
		Replay,
		HowToPlay
  },
	data () {
    return {
			cards: ['A','2','3','4','5','6','7','8','9','10','J','Q','K']
      .flatMap(x=>['S','H','C','D'].map(y=>x+y))
      .reduce((acc,cur,i)=>{
        acc[cur]={suit:cur[cur.length-1],txt:cur.substr(0,cur.length-1),num:Math.floor(i/4)};
        return acc},{}), 
			cardSet:	['A','2','3','4','5','6','7','8','9','10','J','Q','K']
				.flatMap(x=>['S','H','C','D'].map(y=>x+y)),
				//英文小教室---suit花色: spades黑桃, hearts紅桃, clubs梅花, diamonds方塊
			below: {b0:{},b1:{},b2:{},b3:{},b4:{},b5:{},b6:{},b7:{}},
			second: 0,
			isPause: false,
			isReplayShow: false,
			isPauseShow: false,
			isHowToPlayShow: true,
			moveCard: {}
    }
	},
	mounted() {
		this.shuffleCard()
		this.timmer()
	},
	computed:{
		belowLeft() {
			const left = {
				b0: this.below.b0,
				b1: this.below.b1,
				b2: this.below.b2,
				b3: this.below.b3
			}
			return left
		},
		belowRight() {
			const right = {
				b4: this.below.b4,
				b5: this.below.b5,
				b6: this.below.b6,
				b7: this.below.b7
			}
			return right
		},
		nowMin() {
      let min = Math.floor(Math.floor(this.second % 3600) / 60)
      let splitMin = min.toString().split("")
      if(splitMin.length <= 1) {
        splitMin.unshift('0')
      }
      let nowMin = splitMin.toString().replace(',', '')
      return nowMin
    },
    nowSec() {
      let sec = this.second % 60
      let splitSec = sec.toString().split("")
      if(splitSec.length <= 1) {
        splitSec.unshift('0')
      }
      let nowSec = splitSec.toString().replace(',', '')
      return nowSec
    },
    showNowTime() {
      return `Time：${this.nowMin}：${this.nowSec}`
		}
	},
  methods:{
		shuffleCard(){
			//組成8個二維陣列，存放不同牌
			this.below = {b0:{},b1:{},b2:{},b3:{},b4:{},b5:{},b6:{},b7:{}}
      let cardArr = [7,6,7,6,7,6,7,6].shuffle().reduce((acc,cur)=>({
        cum: acc.cum+cur,
        arr: [...acc.arr,acc.res.slice(acc.cum,acc.cum+cur)],
        res: acc.res
      }),{cum:0,arr:[],res:this.cardSet.slice().shuffle()}).arr
      //轉成雙層物件，方便索引
      cardArr.map((slot,i)=>{
        let slotRef = 'b'+i
        slot.map(cardRef=>{
          this.cards[cardRef].slot = slotRef; 
          this.below[slotRef][cardRef] = this.cards[cardRef]
        })
      })
		},
		timmer() {
      let clock = window.setInterval(() => {
				if(!this.isPauseShow && !this.isReplayShow) {
					this.second++
				} else {
					window.clearInterval(clock)
				}
      },1000)
		},
		pauseTime(showAleart) {
			if(showAleart === 'pause'){
				this.isPauseShow = true
			} else if (showAleart === 'replay'){
				this.isReplayShow = true
			}
		},
		continueTime() {
			this.isPauseShow = false
			this.isReplayShow = false
			this.timmer()
		},
		reStart() {
			this.isPauseShow = false
			this.isReplayShow = false
			this.shuffleCard()
			this.second = 0
			this.timmer()
		},
		dragStart(event, card){
			dom = event.currentTarget
			this.moveCard = card
		},
		allowDrop(event) {
			event.preventDefault()
		},
		drop(event, rowKey) {
			event.preventDefault()
			event.target.appendChild(dom)
			const cardKey = this.moveCard.txt + this.moveCard.suit
			delete this.below[this.moveCard.slot][cardKey]
			this.below[rowKey][cardKey] = this.moveCard
		},
		cancelDefault (e) {
			e.preventDefault()
			e.stopPropagation()
			return false
		}
  }
}
</script>

<style lang="sass" scoped>
$wrapWidth: calc(100% - 120px)

p
	margin: 0

img
	display: block

.game
	width: 100%
	height: 100%
	position: relative
	background-image: url(../assets/bg-img.svg)
	background-repeat: no-repeat
	background-size: 180%
	background-position-y: bottom
	background-position-x: calc(50% - 80px)

	&__header
		width: calc(100% - 48px)
		height: 70px
		display: flex
		justify-content: space-between
		padding: 30px 24px

		&__logo
			width: 170px

		&__menu
			display: flex

			.item
				display: flex
				flex-direction: column
				align-items: center
				margin-left: 16px
				cursor: pointer

				&__image
					width: 25px
					height: 25px
					margin-bottom: 5px

				&__text
					color: #58554F
					font-size: 15px

	&__wrap
		width: $wrapWidth
		height: calc(100% - 130px)
		padding: 0 60px

		&__top
			width: 100%
			height: 140px
			display: flex
			justify-content: space-between
			margin-bottom: 30px
			
			.column
				width: 45%
				height: 100%
				display: flex

				&__card
					width: 100px
					height: 100%
					display: flex
					justify-content: center
					align-items: center

					img
						width: 30px

				.left-card
					background-color: #F7F6F5
					border: 1px solid #AFAFAF
					border-radius: 5px
					margin-right: 30px

				.right-card
					background-color: #F7F6F5
					border-radius: 5px
					margin-left: 30px
					box-shadow: 0 4px 14px rgba(24,24,24,0.29)

		&__down
			width: 100%
			height: calc(100% - 170px)
			display: flex
			justify-content: space-between
	
			&__wrap
				width: 45%
				height: 100%
				display: flex

				.row
					position: relative
					width: 100px
					height: 100%

					&__card
						height: 130px
						position: relative
						background-color: #F7F6F5
						border-radius: 5px
						padding: 1px 5px
						border: 1px solid #D9D9D9
						display: flex
						flex-direction: column
						justify-content: space-between
						
						&__suits
							display: flex
							flex-wrap: wrap
							position: absolute
							top: 50%
							left: 50%
							transform: translate(-50%, -50%)

							&__suit
								width: 50%
								margin: 2px 0

								.normal-suit
									width: 15px
									margin: 0 auto

							&__special
								width: 100%

								.special-suit
									width: 30px
									margin: 0 auto

							.upsite-down
								transform: rotate(180deg)

							.card-full, .card-middle
								width: 100%

						&__text
							font-size: 14px
							font-weight: bold

							.small-suit
								width: 8px

						.right-txt
							transform: rotate(180deg)

					@for $i from 1 through 20
						.num-#{$i}
    					top: -110px * $i

				.left-row
					margin-right: 30px
					
				.right-row
					margin-left: 30px

	&__footer
		width: 100%
		height: 170px
		display: flex
		flex-direction: column
		justify-content: flex-end
		align-items: center
		position: absolute
		bottom: 0
		padding: 30px 0

		&__hinit
			display: flex
			flex-direction: column
			align-items: center
			cursor: pointer

			&__logo
				width: 25px
			
			&__text
				color: #fff
				font-size: 15px
		
		&__time
			color: #fff
			font-size: 42px
		
		&__score
			color: #fff
			font-size: 26px
			text-decoration: bold
</style>