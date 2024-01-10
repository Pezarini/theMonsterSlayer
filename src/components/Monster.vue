<template>
	<div class="container">
		<h1>Monster</h1>
		<div class="health" 
			:class="{ danger: this.lifeMonster < 20 }"
			:style="{ width: this.lifeMonster + '%' }"
		>
		</div>
		<h4>{{ this.lifeMonster + '%' }}</h4>
	</div>
</template>

<script>
export default {
	name: 'Player',
	props: {
		healthMonster: Number,
	},
	computed: {
		lifeMonster() {
			return this.healthMonster <= 0 ? this.messageYouWin() : this.healthMonster;
		}
	},
	methods: {
		messageYouWin() {
			this.$emit('messageYouWin', true);
			return 0;
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
