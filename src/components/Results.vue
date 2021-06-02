<template>
	<div class="results">
		<p>Reaction Time: {{ score }} ms</p>
		<p class="rank" :class="{yellow: this.score > 250, red: this.score > 400}">{{ rank }}</p>
	</div>
</template>

<script>
export default {
	props: ['score'],
	data() {
		return {
			rank: null
		}
	},
	updated() {
		if (this.score < 250) {
			this.rank = 'Ninja Fingers';
		}
		if (this.score > 250 && this.score < 400) {
			this.rank = 'Rapid reflexes';
		}
		if (this.score > 400) {
			this.rank = 'Snail pace';
		}
	}
};
</script>

<style lang="sass">
.rank
	font-size: 1.4em
	color: green
	&.yellow
		color: yellow
	&.red
		color: red
</style>