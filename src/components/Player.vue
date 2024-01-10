<template>
	<div class="container">
		<h1>Player</h1>
		<div class="health" 
			:class="{ danger: this.lifePlayer < 20 }"
			:style="{ width: this.lifePlayer + '%' }"
		>
		</div>
		<h4>{{ this.lifePlayer + '%' }}</h4>
	</div>
</template>

<script>
export default {
	name: 'Player',
	props: {
		healthPlayer: Number,
		statusGame: Boolean
	},
	computed: {
		lifePlayer() {
			if (this.healthPlayer <= 0) {
				this.messageYouWin();
				return 0;
			}
			else if (this.healthPlayer >= 100) {
				return 100;
			}
			return this.healthPlayer;
		}
	},
	methods: {
		messageYouWin() {
			this.$emit('messageYouLoss', true);
		}
	}
};
</script>

<style scoped>
.container {
	justify-content: center;
	align-items: center;
	flex-direction: column;
	width: 100%;
	height: 20px;
}

.health {
	display: flex;
	justify-content: flex-end;
	height: 100%;
	border: 1px solid black;
	background-color: rgb(7, 189, 40);
	transition: width 0.3s ease;
}

.health.danger {
	background-color: red;
}
</style>
