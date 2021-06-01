<template>
	<div class="backdrop" @click.self="closeModal">
		<div class="modal">
			<!-- <p>{{ msg }}</p> -->
			<slot>Default slot</slot>
			<div class="links">
				<p>Some additional content</p>
				<slot name="links"></slot>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	// props: ['msg'],
	props: [],
  data() {
    return {

    };
  },
	methods: {
		closeModal() {
			this.$emit('closeModal');
		}
	}
};
</script>

<style lang="sass" scoped>
.modal
	width: 400px
	padding: 20px
	margin: 100px auto
	background: white
	border-radius: 10px
.backdrop
	top: 0
	position: fixed
	background: rgba(#000, 0.5)
	width: 100%
	height: 100%
</style>