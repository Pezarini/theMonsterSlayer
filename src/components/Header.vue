<template>

	<div class="headerContainer">
		<div class="headerContent">
			<h1>The Monster Slayer</h1>
		</div>
	</div>

</template>

<script>
export default {
	name: 'Header'
}
</script>

<style scoped>

	.headerContainer {
		background-color: #800000;
		width: 100%;
		margin: 0px;
		display: flex;
		justify-content: center;
		border: 2px solid black;
		align-items: center;
	}

	.headerContent h1 {
		color: rgb(235, 235, 235);
	}
</style>
