<template>

<div>

	<div class="container">
		<div class="menu">
			<div class="menuStartGame" v-if="menuStartGame">
				<button @click="menuStartGame = !menuStartGame" id="startGameButton">Start Game</button>
			</div>

			<div class="menuInGame" v-else-if="!winGame && !overGame">
				<button @click="attack()" id="attack">Attack</button>
				<button @click="specialAttack()" id="specialAttack">Special Attack</button>
				<button 
					@click="healing()" 
					id="healing"
					:disabled="healingDisable"
				>Healing
				</button>
				<button @click="leaveTheGame()" id="giveUp">Give Up</button>
			</div>
			<div class="restartGame" v-if="winGame || overGame">
				<button id="restartGame" @click="this.restartGame()">Restart</button>
			</div>
		</div>

	</div>
</div>
</template>

<script>
export default {
	name: 'Menu', 
	data() {
		return {
			menuStartGame: true,
		}
	},
	props: {
		healthPlayer: Number,
		healthMonster: Number,
		winGame: Boolean,
		overGame: Boolean,
		logInfos: Array,
	},
	computed: {
		healingDisable() {
			return this.healthPlayer < 100 ? false : true;
		}
	},
	methods: {
		restartGame() {
			this.$emit('resetGame', false);
			this.leaveTheGame();
		},
		leaveTheGame() {
			this.menuStartGame = !this.menuStartGame;
			this.$emit('resetHealth', 100);
		},
		automateActions(people, operation, damageRandom) {
			const randomNumber = Math.floor(Math.random() * 3) + damageRandom;
			return operation === '-' ? people - randomNumber : people + randomNumber;
		},
		attack() {
			this.$emit('playerLostLife', this.automateActions(this.healthPlayer, '-', 17));
			this.$emit('monsterLostLife', this.automateActions(this.healthMonster, '-', 14));
		},
		specialAttack() {
			this.$emit('monsterLostLife', this.automateActions(this.healthMonster, '-', 20));
			this.$emit('playerLostLife',this.automateActions(this.healthPlayer, '-', 14));
		},
		healing() {
			this.$emit('healingPlayer',this.automateActions(this.healthPlayer, '+', 15));
		}
	},
}
</script>

<style scoped>
	.menu {
		box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.1); 
		width: 100%;
		height: 50px;
		margin-top: 10px;
		display: flex;
		justify-content: center;
		align-items: center; 
		flex-direction: column;
	}
	#attack {
		background-color: #2466ff;
		color:black ;
	}
	#specialAttack {
		background-color: rgb(255, 196, 0);
		color: black;
	}
	#giveUp {
		background-color: red;
		color:black ;
	}
	#healing {
		background-color: rgb(7, 189, 40);
		color:black ;
	}
	#startGameButton, #restartGame {
		background-color: #2466ff;
		color: black;
	}
	button {
		border-radius: 4px;
		color: rgb(235, 235, 235);
		margin: 30px;
	}
	.menuInGame {
		display: flex;
		justify-content: space-around; 
	}

</style>
