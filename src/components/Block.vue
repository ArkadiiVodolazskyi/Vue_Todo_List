<template>
	<div v-if="showBlock" class="block" @click="stopTimer">
		{{ textResult }}
	</div>
</template>

<script>
export default {
	props: [
		'delay'
	],
	data() {
		return {
			showBlock: false,
			timer: null,
			reactionTime: 0,
			textResult: 'Click Me'
		}
	},
	methods: {
		startTimer() {
			this.timer = setInterval(() => {
				this.reactionTime += 10;
			}, 10);
		},
		stopTimer() {
			clearInterval(this.timer);
			this.textResult = `Time is: ${this.reactionTime}`;
			this.$emit('end', this.reactionTime);
		}
	},
	mounted() {
		setTimeout(() => {
			this.showBlock = true;
			this.startTimer();
		}, this.delay);
	},
	updated() {
		console.log('Block updated. Delay: ' + this.delay);
	},
	unmounted() {
		console.log('Block unmounted');
	}
};
</script>

<style lang="sass">
.block
	width: 400px
	border-radius: 20px
	background: green
	color: white
	text-align: center
	padding: 100px 0
	margin: 40px auto
	cursor: pointer
	user-select: none
</style>