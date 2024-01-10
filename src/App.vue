<template>
	<div id="app">
		<div class="container">
			<div class="header">
				<Header />
			</div>

			<div class="content">
				<div class="backgroundOfTheFight">
					<div class="player">
						<Player 
							:healthPlayer="healthPlayer"
							@messageYouLoss="messageYouLoss"

						/>
					</div>
					<div class="monster">
						<Monster 
							:healthMonster="healthMonster"
							@messageYouWin="messageYouWin"
						/>
					</div>
				</div>

				<div class="gameOver" v-show="overGame" >
					<h1>You Lose!</h1>
				</div>

				<div class="gameWin" v-show="winGame" >
					<h1>You Win!</h1>
				</div>

				<div class="Menu">
					<Menu
						:healthPlayer="healthPlayer"
						:healthMonster="healthMonster"
						:winGame="winGame"
						:overGame="overGame"
						@playerLostLife="playerLostLife"
						@monsterLostLife="monsterLostLife"
						@resetHealth="resetHealth"
						@monsterReceivesSpecialAttack="specialAttack"
						@healingPlayer="playerReceivesLife"
						@resetGame="resetGame"
					/>
				</div>
				</div>
			</div>
	</div>
</template>

<script>
import Header from './components/Header.vue'
import Player from './components/Player.vue'
import Monster from './components/Monster.vue'
import Menu from './components/Menu.vue'

export default ({
	name: 'App',
	components: {
		Header,
		Player,
		Monster,
		Menu
	},
	data() {
		return {
			healthPlayer: 100,
			healthMonster: 100,
			overGame: false,
			winGame: false,
		}
	},
	methods: {
		resetGame(statusGame) {
			this.overGame = statusGame;
			this.winGame = statusGame
		},
		messageYouLoss(lose) {
			this.overGame = lose;
		},
		messageYouWin(win) {
			this.winGame = win;
		},
		playerLostLife(life) {
			this.healthPlayer = life
		},
		resetHealth(health) {
			this.healthPlayer = health;
			this.healthMonster = health;
		},
		monsterLostLife(healthMonster) {
			this.healthMonster = healthMonster;
		},
		specialAttack(healthMonster) {
			this.healthMonster = healthMonster;
		},
		playerReceivesLife(healthPlayer) {
			this.healthPlayer = healthPlayer;
		}
	}
})
</script>

<style scoped>
	* {
		font-family: 'Raleway', sans-serif;
	}
	.container {
		display: flex;
		flex-direction: column;
		height: 100vh; 
	}

	.header .content {
		margin-bottom: 20px; 
	}

	.backgroundOfTheFight {
		box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.1); 
		width: 100%;
		height: 30vh;
		display: flex;
		flex-direction: row;
		justify-content: space-around;
	}

	.player {
		width: 45%;
		display: flex;
		flex-direction: column;
	}

	.monster {
		width: 45%;
		display: flex;
		flex-direction: column;
	}

	.gameOver, .gameWin {
		box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.1); 
		width: 100%;
		height: auto;
		display: flex;
		justify-content: center;
	 }
</style
</style>